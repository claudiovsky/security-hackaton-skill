# Contributing to Security Hackathon Skill

Thanks for your interest! This skill is designed to be modular and extensible.

## What to contribute

### 🎯 High-impact contributions

- **New team personas** — Add a 6th red team (e.g., `GraphQL`, `Mobile`, `API Gateway`, `WebSocket`)
- **Checklist improvements** — Better detection criteria based on real-world findings
- **Severity examples** — Concrete examples of what constitutes Critical vs High vs Medium vs Low

### 📝 Documentation

- **Translations** — Translate team personas or the README into other languages
- **Example reports** — Share (sanitized) hackathon reports from real projects
- **Stack-specific tips** — Notes on how findings differ across frameworks

### 🐛 Fixes

- **False positive patterns** — If a checklist item consistently generates false positives, improve the wording
- **Scoring balance** — If point values feel off, propose adjustments with reasoning

## How to contribute

1. **Fork** this repository
2. **Create a branch** for your change (`git checkout -b add-graphql-team`)
3. **Make your changes** following the conventions below
4. **Open a PR** with a clear description of what changed and why

## Conventions

### Team personas

Follow the existing format in `references/team-personas.md`:

```markdown
## 🔴 Red Team N — CODENAME (Specialty)

**Persona:** [2-3 sentences describing expertise and background]

**Mindset:** "[A single quoted statement capturing how this specialist thinks]"

### Checklist

| # | Check | What to look for |
|---|-------|-----------------|
| XX-01 | [Check name] | [What to look for — specific and actionable] |
```

Rules:
- **Prefix convention:** Use a unique 1-2 letter prefix (C=Cerberus, H=Hydra, P=Phantom, F=Fortress, X=Paradox)
- **12-14 checks per team** — enough to be thorough, not so many it becomes a checkbox exercise
- **Actionable language** — "Are X validated?" not "X should be validated"
- **Framework-agnostic** — Check for vulnerability patterns, not specific function names

### Scoring changes

If proposing scoring changes, include:
- **Rationale** — Why the current value is wrong
- **Example** — A real scenario where the current scoring produces a bad outcome
- **Proposed value** — The new number and why it's better

## Code of conduct

Be respectful, constructive, and specific. This is a security tool — accuracy matters more than volume.
