<!-- Last verified against EUR-Lex: 2026-03-28 -->

# CI/CD — Automate Your Compliance Checks

Manual compliance checks are like manual deployments: they work until someone forgets.
Let your CI pipeline be the one who never forgets. Here are GitHub Actions, GitLab CI,
pre-commit hooks, and Makefile targets that catch compliance drift before it reaches production.

## GitHub Actions Workflow

```yaml
# .github/workflows/ai-act-compliance.yml
name: AI Act Compliance Checks

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  compliance-doc-check:
    name: Check compliance documentation
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Verify AI_ACT_COMPLIANCE.md exists
        run: |
          if [ ! -f AI_ACT_COMPLIANCE.md ]; then
            echo "::error::AI_ACT_COMPLIANCE.md not found in repository root"
            echo "Create this file documenting your AI Act compliance measures."
            exit 1
          fi

      - name: Check documentation freshness (90-day max staleness)
        run: |
          LAST_MODIFIED=$(git log -1 --format="%at" -- AI_ACT_COMPLIANCE.md)
          NOW=$(date +%s)
          DAYS_OLD=$(( (NOW - LAST_MODIFIED) / 86400 ))
          echo "AI_ACT_COMPLIANCE.md last updated $DAYS_OLD days ago"
          if [ "$DAYS_OLD" -gt 90 ]; then
            echo "::warning::AI_ACT_COMPLIANCE.md is $DAYS_OLD days old (max 90)"
            echo "::error::Compliance documentation is stale. Please review and update."
            exit 1
          fi

  compliance-headers-check:
    name: Check AI API compliance headers
    runs-on: ubuntu-latest
    needs: [compliance-doc-check]
    services:
      app:
        image: ${{ vars.APP_IMAGE || 'app:test' }}
        ports:
          - 3000:3000
    steps:
      - uses: actions/checkout@v4

      - name: Wait for app to be ready
        run: |
          for i in $(seq 1 30); do
            if curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/health | grep -q "200"; then
              echo "App is ready"
              break
            fi
            sleep 2
          done

      - name: Verify compliance headers on AI endpoints
        run: |
          ENDPOINTS="/api/ai/chat /api/ai/generate"
          REQUIRED_HEADERS="X-AI-Generated X-AI-Provider X-AI-System"
          FAILED=0

          for endpoint in $ENDPOINTS; do
            echo "Checking $endpoint..."
            HEADERS=$(curl -s -D - -o /dev/null -X POST \
              -H "Content-Type: application/json" \
              -d '{"message":"compliance test"}' \
              "http://localhost:3000${endpoint}")

            for header in $REQUIRED_HEADERS; do
              if echo "$HEADERS" | grep -qi "^${header}:"; then
                echo "  ✓ $header present"
              else
                echo "::error::$endpoint missing required header: $header"
                FAILED=1
              fi
            done
          done

          exit $FAILED

  compliance-frontend-check:
    name: Check AI disclosure component
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Search for AI disclosure component
        run: |
          PATTERNS="ai-disclosure AIDisclosure ai_disclosure data-ai-disclosure"
          FOUND=0

          for pattern in $PATTERNS; do
            if grep -r "$pattern" --include="*.tsx" --include="*.jsx" \
               --include="*.vue" --include="*.html" --include="*.razor" \
               src/ app/ components/ pages/ 2>/dev/null; then
              FOUND=1
              echo "Found AI disclosure pattern: $pattern"
            fi
          done

          if [ "$FOUND" -eq 0 ]; then
            echo "::error::No AI disclosure component found in frontend code"
            echo "Ensure your UI includes an AI disclosure banner (Art. 50)."
            exit 1
          fi

  compliance-tests:
    name: Run compliance test suite
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - name: Run compliance-specific tests
        run: npm test -- --testPathPattern='compliance|ai-act' --passWithNoTests
```

## Pre-Commit Hook

```bash
#!/usr/bin/env bash
# .git/hooks/pre-commit (or use with pre-commit framework)
# Save as: scripts/pre-commit-compliance.sh
# Install: ln -sf ../../scripts/pre-commit-compliance.sh .git/hooks/pre-commit

set -euo pipefail

RED='\033[0;31m'
YELLOW='\033[1;33m'
GREEN='\033[0;32m'
NC='\033[0m'

FAILED=0

echo "Running AI Act compliance pre-commit checks..."

# 1. Check for hardcoded AI model names (should be in config/env)
HARDCODED_MODELS=$(git diff --cached --diff-filter=ACM -U0 -- '*.ts' '*.js' '*.py' '*.go' '*.java' '*.cs' |
  grep -E '^\+.*["'"'"'](gpt-4|gpt-3\.5|claude-[0-9]|gemini-|llama-[0-9])' |
  grep -v '\.env' | grep -v 'config' | grep -v '\.yml' | grep -v 'test' || true)

if [ -n "$HARDCODED_MODELS" ]; then
  echo -e "${YELLOW}WARNING: Possible hardcoded AI model names found:${NC}"
  echo "$HARDCODED_MODELS"
  echo -e "${YELLOW}Consider using environment variables or config files.${NC}"
  # Warning only, not blocking
fi

# 2. Check new API route files have compliance middleware
NEW_ROUTE_FILES=$(git diff --cached --name-only --diff-filter=A |
  grep -E '(route|controller|handler|endpoint)\.(ts|js|py|go|java|cs)$' || true)

for file in $NEW_ROUTE_FILES; do
  if ! git diff --cached -- "$file" | grep -qiE '(compliance|ai.header|ai.middleware|AICompliance)'; then
    echo -e "${RED}ERROR: New route file '$file' may be missing compliance middleware.${NC}"
    echo "Ensure AI-related endpoints include compliance headers."
    FAILED=1
  fi
done

# 3. Check AI_ACT_COMPLIANCE.md wasn't deleted
if git diff --cached --name-only --diff-filter=D | grep -q 'AI_ACT_COMPLIANCE.md'; then
  echo -e "${RED}ERROR: AI_ACT_COMPLIANCE.md is being deleted.${NC}"
  FAILED=1
fi

if [ "$FAILED" -eq 1 ]; then
  echo -e "${RED}Pre-commit compliance checks failed.${NC}"
  exit 1
fi

echo -e "${GREEN}All compliance pre-commit checks passed.${NC}"
```

## GitLab CI

```yaml
# .gitlab-ci.yml (compliance stages)
stages:
  - compliance
  - test
  - deploy

compliance:doc-check:
  stage: compliance
  image: alpine/git:latest
  script:
    - |
      if [ ! -f AI_ACT_COMPLIANCE.md ]; then
        echo "ERROR: AI_ACT_COMPLIANCE.md not found"
        exit 1
      fi
    - |
      LAST_MODIFIED=$(git log -1 --format="%at" -- AI_ACT_COMPLIANCE.md)
      NOW=$(date +%s)
      DAYS_OLD=$(( (NOW - LAST_MODIFIED) / 86400 ))
      echo "AI_ACT_COMPLIANCE.md last updated $DAYS_OLD days ago"
      if [ "$DAYS_OLD" -gt 90 ]; then
        echo "ERROR: Documentation is stale ($DAYS_OLD days)"
        exit 1
      fi
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

compliance:header-check:
  stage: compliance
  image: curlimages/curl:latest
  services:
    - name: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
      alias: app
  script:
    - |
      REQUIRED_HEADERS="X-AI-Generated X-AI-Provider X-AI-System"
      HEADERS=$(curl -s -D - -o /dev/null -X POST \
        -H "Content-Type: application/json" \
        -d '{"message":"test"}' "http://app:3000/api/ai/chat")
      for header in $REQUIRED_HEADERS; do
        echo "$HEADERS" | grep -qi "^${header}:" || { echo "Missing: $header"; exit 1; }
      done
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
```

## Makefile Targets

```makefile
# Makefile
.PHONY: compliance-check compliance-report compliance-headers compliance-docs

compliance-check: compliance-docs compliance-headers ## Run all compliance checks
	@echo "All compliance checks passed"

compliance-docs: ## Check compliance documentation exists and is fresh
	@test -f AI_ACT_COMPLIANCE.md || (echo "ERROR: AI_ACT_COMPLIANCE.md missing" && exit 1)
	@DAYS=$$(( ($$(date +%s) - $$(git log -1 --format="%at" -- AI_ACT_COMPLIANCE.md)) / 86400 )); \
	if [ "$$DAYS" -gt 90 ]; then \
		echo "WARNING: AI_ACT_COMPLIANCE.md is $$DAYS days old (max 90)"; \
		exit 1; \
	else \
		echo "AI_ACT_COMPLIANCE.md is $$DAYS days old (OK)"; \
	fi

compliance-headers: ## Test that AI endpoints return required headers
	@echo "Starting app for header check..."
	@curl -sf http://localhost:3000/health > /dev/null 2>&1 || \
		(echo "ERROR: App not running on :3000. Start it first." && exit 1)
	@for endpoint in /api/ai/chat /api/ai/generate; do \
		echo "Checking $$endpoint..."; \
		curl -s -D - -o /dev/null -X POST \
			-H "Content-Type: application/json" \
			-d '{"message":"test"}' \
			"http://localhost:3000$$endpoint" | \
			grep -qi "X-AI-Generated" || \
			(echo "FAIL: $$endpoint missing X-AI-Generated header" && exit 1); \
	done
	@echo "All headers present"

compliance-report: ## Generate compliance status report
	@echo "=== AI Act Compliance Report ==="
	@echo "Date: $$(date -u +%Y-%m-%dT%H:%M:%SZ)"
	@echo ""
	@echo "Documentation:"
	@test -f AI_ACT_COMPLIANCE.md && echo "  AI_ACT_COMPLIANCE.md: EXISTS" || echo "  AI_ACT_COMPLIANCE.md: MISSING"
	@echo ""
	@echo "Disclosure components:"
	@grep -rl "ai-disclosure\|AIDisclosure\|data-ai-disclosure" \
		--include="*.tsx" --include="*.jsx" --include="*.vue" --include="*.html" \
		src/ app/ components/ 2>/dev/null | sed 's/^/  /' || echo "  None found"
	@echo ""
	@echo "Compliance middleware:"
	@grep -rl "AICompliance\|ai_compliance\|X-AI-Generated" \
		--include="*.ts" --include="*.py" --include="*.go" --include="*.java" --include="*.cs" \
		src/ app/ lib/ 2>/dev/null | sed 's/^/  /' || echo "  None found"
```
