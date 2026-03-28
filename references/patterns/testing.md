<!-- Last verified against EUR-Lex: 2026-03-28 -->

# Testing — Because "Trust Me, It's Compliant" Won't Work in an Audit

Compliance without tests is like a safety net without ropes — it looks good from a distance.
Here are concrete, runnable tests for every layer: unit, integration, E2E, and even a SQL
query for catching compliance drift in your database. Copy, paste, adapt, ship.

## Jest/Vitest: AI Disclosure Component Renders

```typescript
// __tests__/ai-disclosure.test.tsx
import { describe, it, expect } from "vitest";
import { render, screen } from "@testing-library/react";
import { AIDisclosureBanner } from "../components/ai-disclosure-banner";

describe("AIDisclosureBanner", () => {
  it("renders before any user interaction", () => {
    render(
      <AIDisclosureBanner systemName="TestAI" providerName="TestCorp" />
    );

    expect(screen.getByRole("status")).toBeInTheDocument();
    expect(screen.getByText(/AI-Powered Interaction/)).toBeInTheDocument();
    expect(screen.getByText(/TestAI/)).toBeInTheDocument();
    expect(screen.getByText(/TestCorp/)).toBeInTheDocument();
    expect(screen.getByText(/Article 50/)).toBeInTheDocument();
  });

  it("includes data-ai-disclosure attribute for automated checks", () => {
    render(
      <AIDisclosureBanner systemName="TestAI" providerName="TestCorp" />
    );

    const banner = screen.getByRole("status");
    expect(banner).toHaveAttribute("data-ai-disclosure", "true");
  });

  it("has accessible aria-label", () => {
    render(
      <AIDisclosureBanner systemName="TestAI" providerName="TestCorp" />
    );

    expect(
      screen.getByLabelText("AI disclosure notice")
    ).toBeInTheDocument();
  });
});
```

## Jest/Vitest: AI Content Marking

```typescript
// __tests__/ai-content-marking.test.tsx
import { describe, it, expect } from "vitest";
import { render } from "@testing-library/react";

// Generic component that renders AI-generated content
function AIContent({ content }: { content: string }) {
  return (
    <div data-ai-generated="true" data-testid="ai-content">
      {content}
    </div>
  );
}

describe("AI content marking", () => {
  it("includes data-ai-generated attribute on AI content", () => {
    const { getByTestId } = render(<AIContent content="Hello from AI" />);
    const element = getByTestId("ai-content");
    expect(element).toHaveAttribute("data-ai-generated", "true");
  });

  it("all AI response elements have the marking attribute", () => {
    const { container } = render(
      <div>
        <AIContent content="Response 1" />
        <AIContent content="Response 2" />
        <AIContent content="Response 3" />
      </div>
    );

    const aiElements = container.querySelectorAll("[data-ai-generated]");
    expect(aiElements.length).toBe(3);
    aiElements.forEach((el) => {
      expect(el.getAttribute("data-ai-generated")).toBe("true");
    });
  });
});
```

## Pytest: API Compliance Headers

```python
# tests/test_compliance_headers.py
import pytest
from fastapi.testclient import TestClient
from main import app  # Your FastAPI app

client = TestClient(app)

REQUIRED_HEADERS = [
    "X-AI-Generated",
    "X-AI-Provider",
    "X-AI-System",
    "X-AI-Act-Disclosure",
    "X-AI-Timestamp",
]

AI_ENDPOINTS = [
    ("/api/ai/chat", "POST", {"message": "test"}),
    ("/api/ai/disclosure", "GET", None),
]


@pytest.mark.parametrize("endpoint,method,body", AI_ENDPOINTS)
def test_ai_endpoints_return_compliance_headers(endpoint, method, body):
    if method == "POST":
        response = client.post(endpoint, json=body)
    else:
        response = client.get(endpoint)

    for header in REQUIRED_HEADERS:
        assert header.lower() in {
            k.lower() for k in response.headers.keys()
        }, f"Missing required header '{header}' on {method} {endpoint}"


def test_ai_generated_header_is_true():
    response = client.post("/api/ai/chat", json={"message": "test"})
    assert response.headers.get("X-AI-Generated") == "true"


def test_ai_timestamp_is_valid_iso_format():
    from datetime import datetime

    response = client.post("/api/ai/chat", json={"message": "test"})
    timestamp = response.headers.get("X-AI-Timestamp")
    assert timestamp is not None
    # Should not raise ValueError
    datetime.fromisoformat(timestamp)


def test_non_ai_endpoints_do_not_have_ai_headers():
    response = client.get("/health")
    assert "X-AI-Generated" not in response.headers
```

## Pytest: Database AI Metadata Completeness

```python
# tests/test_compliance_database.py
import pytest
from django.test import TestCase
from myapp.models import BlogPost  # Your model using AIContentMixin


class TestAIMetadataCompleteness(TestCase):
    def setUp(self):
        from datetime import datetime, timezone

        BlogPost.objects.create(
            title="Human post",
            body="Written by a human",
            ai_generated=False,
        )
        BlogPost.objects.create(
            title="AI post with metadata",
            body="Written by AI",
            ai_generated=True,
            ai_model="gpt-4o",
            ai_system="Content Generator",
            ai_timestamp=datetime.now(timezone.utc),
        )

    def test_all_ai_content_has_model(self):
        missing = BlogPost.objects.filter(ai_generated=True, ai_model="").count()
        assert missing == 0, f"{missing} AI records missing ai_model"

    def test_all_ai_content_has_system(self):
        missing = BlogPost.objects.filter(ai_generated=True, ai_system="").count()
        assert missing == 0, f"{missing} AI records missing ai_system"

    def test_all_ai_content_has_timestamp(self):
        missing = BlogPost.objects.filter(
            ai_generated=True, ai_timestamp__isnull=True
        ).count()
        assert missing == 0, f"{missing} AI records missing ai_timestamp"

    def test_non_ai_content_is_not_flagged(self):
        human_posts = BlogPost.objects.filter(ai_generated=False)
        for post in human_posts:
            assert post.ai_model == "", "Non-AI content should not have ai_model set"
```

## Playwright: E2E Disclosure Visibility

```typescript
// e2e/compliance-disclosure.spec.ts
import { test, expect } from "@playwright/test";

const AI_PAGES = ["/chat", "/ai-assistant", "/generate"];

for (const page of AI_PAGES) {
  test(`AI disclosure is visible on ${page}`, async ({ page: browserPage }) => {
    await browserPage.goto(page);

    const disclosure = browserPage.locator("[data-ai-disclosure]");
    await expect(disclosure).toBeVisible();

    const text = await disclosure.textContent();
    expect(text).toContain("AI");
    expect(text).toMatch(/Article 50|AI Act|artificial intelligence/i);
  });
}

test("AI disclosure appears before first AI interaction", async ({ page }) => {
  await page.goto("/chat");

  // Disclosure should be visible BEFORE the user sends any message
  const disclosure = page.locator("[data-ai-disclosure]");
  await expect(disclosure).toBeVisible();

  // User has not interacted yet — no messages sent
  const messages = page.locator("[data-testid='chat-message']");
  await expect(messages).toHaveCount(0);
});

test("AI-generated responses show visible label", async ({ page }) => {
  await page.goto("/chat");

  // Send a message to trigger AI response
  await page.fill("[data-testid='chat-input']", "Hello AI");
  await page.click("[data-testid='send-button']");

  // Wait for AI response
  const aiMessage = page.locator("[data-ai-generated='true']");
  await expect(aiMessage.first()).toBeVisible({ timeout: 10000 });

  // Every AI message should be marked
  const allAiMessages = await aiMessage.count();
  expect(allAiMessages).toBeGreaterThan(0);
});
```

## Go: Middleware Header Test

```go
// compliance_test.go
package compliance_test

import (
	"net/http"
	"net/http/httptest"
	"testing"

	"yourapp/compliance"
)

func TestMiddlewareAddsHeadersOnAIRoutes(t *testing.T) {
	cfg := compliance.Config{AIProvider: "TestProvider", AISystem: "TestSystem"}

	handler := compliance.Middleware(cfg)(http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		w.WriteHeader(http.StatusOK)
	}))

	tests := []struct {
		path        string
		wantHeaders bool
	}{
		{"/api/ai/chat", true},
		{"/api/chat/stream", true},
		{"/api/generate/text", true},
		{"/api/users", false},
		{"/health", false},
	}

	for _, tt := range tests {
		t.Run(tt.path, func(t *testing.T) {
			req := httptest.NewRequest("POST", tt.path, nil)
			rec := httptest.NewRecorder()
			handler.ServeHTTP(rec, req)

			hasHeader := rec.Header().Get("X-AI-Generated") != ""
			if hasHeader != tt.wantHeaders {
				t.Errorf("path %s: wantHeaders=%v, got=%v", tt.path, tt.wantHeaders, hasHeader)
			}

			if tt.wantHeaders {
				if v := rec.Header().Get("X-AI-Provider"); v != "TestProvider" {
					t.Errorf("X-AI-Provider = %q, want %q", v, "TestProvider")
				}
				if v := rec.Header().Get("X-AI-System"); v != "TestSystem" {
					t.Errorf("X-AI-System = %q, want %q", v, "TestSystem")
				}
				if v := rec.Header().Get("X-AI-Act-Disclosure"); v == "" {
					t.Error("X-AI-Act-Disclosure header missing")
				}
			}
		})
	}
}
```

## SQL: Compliance Drift Detection

```sql
-- compliance_drift_check.sql
-- Run periodically (cron, scheduled job) to find AI content missing metadata.
-- Adapt table/column names to your schema.

-- 1. Find AI-generated records missing required metadata
SELECT
    'articles' AS table_name,
    id,
    'missing ai_model' AS issue,
    created_at
FROM articles
WHERE ai_generated = TRUE AND (ai_model IS NULL OR ai_model = '')

UNION ALL

SELECT
    'articles' AS table_name,
    id,
    'missing ai_system' AS issue,
    created_at
FROM articles
WHERE ai_generated = TRUE AND (ai_system IS NULL OR ai_system = '')

UNION ALL

SELECT
    'articles' AS table_name,
    id,
    'missing ai_timestamp' AS issue,
    created_at
FROM articles
WHERE ai_generated = TRUE AND ai_timestamp IS NULL

ORDER BY created_at DESC;

-- 2. Summary: compliance coverage percentage
SELECT
    COUNT(*) AS total_ai_records,
    COUNT(*) FILTER (
        WHERE ai_model != '' AND ai_system != '' AND ai_timestamp IS NOT NULL
    ) AS fully_compliant,
    ROUND(
        100.0 * COUNT(*) FILTER (
            WHERE ai_model != '' AND ai_system != '' AND ai_timestamp IS NOT NULL
        ) / NULLIF(COUNT(*), 0),
        1
    ) AS compliance_percentage
FROM articles
WHERE ai_generated = TRUE;
```
