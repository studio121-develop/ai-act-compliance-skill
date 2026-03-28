# Contributing

First off — thank you. The AI Act is 144 pages of dense EU regulation, and no single team can keep a compliance skill perfectly accurate across 27 member states, dozens of frameworks, and an evolving regulatory landscape. Community contributions make the difference between "useful" and "authoritative."

## The Golden Rule

**Accuracy over speed.** This is a compliance tool. If it says something wrong, someone might deploy a non-compliant system. So please: cite your sources, double-check article numbers, and verify dates.

## How to Contribute

### Report a Regulatory Inaccuracy (highest priority)

Found something wrong? An article number that doesn't match, a deadline that shifted, a requirement that's been clarified by new guidance?

1. Open an issue using the **Inaccuracy Report** template
2. Include: what's wrong, what it should say, source link (EUR-Lex, official guidance, etc.)
3. We'll fix it within 48 hours

These reports are treated as P0. No discussion needed — if you're right, we merge the fix immediately.

### Add a National Context

The AI Act applies across the EU, but implementation is national. If your country isn't covered yet:

1. Copy `references/national/TEMPLATE.md`
2. Fill in the sections for your country
3. Name it `references/national/{country}.md` (lowercase English name)
4. Open a PR

**What we need**: competent authorities (name + URL), national implementation law status, sandbox availability, related local regulations, useful links. What we don't need: a summary of the AI Act itself (that's what SKILL.md is for).

### Add Code Patterns for a Framework

Building compliance into a framework we don't cover yet? Amazing.

1. Create `references/patterns/{framework}.md`
2. Follow the structure of existing pattern files (nextjs.md, fastapi.md, etc.)
3. Include: middleware/interceptor for disclosure headers, model/entity patterns for AI metadata, component/template patterns for UI disclosure, test examples
4. Code must be runnable — no pseudocode, no "implement your logic here"

### Add a Sector Guide

Working in a specific industry? Your domain knowledge is incredibly valuable.

1. Create `references/sectors/{sector}.md`
2. Cover: when AI in this sector becomes high-risk, intersection with sector-specific regulations, specific code patterns or data handling requirements, practical examples
3. Cite specific Annex III categories and related EU/national regulations

### Report Bugs or Suggest Improvements

For anything else — structural suggestions, new features, better explanations:

1. Open an issue (or use the relevant template)
2. Describe what you'd change and why
3. If you're proposing a significant change, open an issue first to discuss before writing a PR

## Style Guide

### Tone

We write about EU regulation, not poetry. But that doesn't mean it has to be painful. Keep it:

- **Clear**: a developer should understand what to do after reading, not just what the law says
- **Direct**: lead with the action, not the legal context
- **Light**: humor welcome, bureaucratic language not. If you can explain Art. 50(2) without making someone fall asleep, you're doing it right
- **Accurate**: jokes are fine, wrong article numbers are not

### Formatting

- Use markdown headers consistently (## for main sections, ### for subsections)
- Code blocks must specify the language (`python`, `typescript`, `go`, etc.)
- Checklists use `- [ ]` format
- Article references: `Art. 50(1)` not `Article fifty, paragraph one`
- Date format: `Aug 2, 2026` in English content, `2 agosto 2026` in Italian

### Source Citations

When adding or modifying regulatory content:

- Reference specific articles: `(Art. 50(2))` or `(Annex III, Category 4)`
- For recitals: `(Recital 132)`
- For external guidance: include URL and access date
- For national sources: include authority name and document title

## Pull Request Checklist

Before submitting your PR:

- [ ] All regulatory claims cite specific articles or official sources
- [ ] No broken links
- [ ] Code examples are syntactically correct and runnable
- [ ] New files follow the existing directory structure
- [ ] English is the primary language (national content is the exception)
- [ ] You've read the existing content to avoid duplication

## Code of Conduct

Be constructive, be accurate, be kind. We're all trying to navigate the same regulation. Regulatory disagreements should reference sources, not volume.

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0, the same license that covers this project.
