---
name: security-hackathon
description: "Run an internal security hackathon with competing specialist teams. Multiple red teams audit the codebase from different angles (auth, injection, data, infra, logic), cross-review each other's findings, and a blue team produces a final hardening plan. Generates scored reports with validated vulnerabilities and prioritized fixes."
argument-hint: "Scope (e.g., 'full app', 'auth + API only', 'firestore rules') or team count override"
---

# Security Hackathon

**Persona:** You are the **Hackathon Director** — an impartial judge orchestrating a competitive security audit between specialized red teams. You enforce rules, run each team's audit, manage cross-reviews, compute scores, and produce the final consolidated report. You are ruthlessly objective: only real, demonstrable flaws earn points.

## When to Use

- Before a major production release (more thorough than a single audit)
- When you want maximum vulnerability coverage with built-in validation
- After large feature additions that touch auth, data, or infrastructure
- For periodic deep-dive security reviews
- When a single audit might miss specialized attack vectors

## How It Works

This skill simulates a **competitive security hackathon** with 5 specialized Red Teams and 1 Blue Team:

| Team | Codename | Specialization |
|------|----------|---------------|
| 🔴 Red 1 | **Cerberus** | Authentication, sessions, identity |
| 🔴 Red 2 | **Hydra** | Input validation, injection, XSS |
| 🔴 Red 3 | **Phantom** | Data exposure, privacy, IDOR |
| 🔴 Red 4 | **Fortress** | Infrastructure, config, dependencies |
| 🔴 Red 5 | **Paradox** | Business logic, race conditions, state |
| 🔵 Blue | **Shield** | Defense synthesis, fix validation, hardening |

Each team has a detailed persona and checklist in [./references/team-personas.md](./references/team-personas.md).

## Procedure

### Phase 0 — Briefing (Director)

Before any team starts, the Director must:

1. **Map the target:**
   - Read the project structure, `package.json`, framework config
   - Identify: framework, auth system, database, hosting, API surface
   - List all entry points (API routes, server actions, forms, webhooks)
   - Read `.env*` files — note client-exposed vs server-only vars
   - Read database/storage rules files
   - Check `.gitignore` for sensitive file coverage

2. **Produce the Briefing:**

```
═══════════════════════════════════════════════════
  🏁 HACKATHON BRIEFING
═══════════════════════════════════════════════════

  Project:      [name]
  Stack:        [framework, db, auth, hosting]
  Commit:       [SHA]
  Scope:        [full | partial — what's in/out]
  Entry Points: [n] API routes, [n] server actions, [n] forms
  Teams:        5 Red + 1 Blue
  Scoring:      See rules below

═══════════════════════════════════════════════════
```

3. **Announce the rules** (summarize from [./references/scoring.md](./references/scoring.md))

### Phase 1 — Red Team Attacks (Sequential)

Run each Red Team **one at a time**. For each team:

1. Announce: `═══ TEAM [CODENAME] — ENGAGING ═══`
2. Adopt the team's persona from [./references/team-personas.md](./references/team-personas.md)
3. Systematically work through the team's checklist
4. Read all relevant source files — **no guessing**, only report what you can prove
5. For each vulnerability found, produce a **Finding Card:**

```
┌─────────────────────────────────────────────────┐
│  [TEAM]-[NNN]           [SEVERITY_EMOJI] [SEV]  │
│─────────────────────────────────────────────────│
│  Title:   [Short name]                          │
│  File:    [path:line]                           │
│  PoC:     [Step-by-step attack scenario]        │
│  Impact:  [What attacker gains]                 │
│  Fix:     [Exact code change / diff]            │
└─────────────────────────────────────────────────┘
```

6. At the end, produce a **Team Summary:**

```
═══ TEAM [CODENAME] — ATTACK COMPLETE ═══
Findings: [N] (🔴×[n]  🟠×[n]  🟡×[n]  🔵×[n])
Raw Score: [computed]
Files Analyzed: [list]
══════════════════════════════════════════
```

### Phase 2 — Cross-Review

After ALL Red Teams have reported, run **cross-reviews**. Each team reviews the findings of every other team (not their own).

For each finding under review, the reviewing team produces a **Review Verdict:**

```
┌─ REVIEW: [FINDING_ID] ← reviewed by [REVIEWER] ┐
│  Verdict:   ✅ CONFIRMED | ⚠️ PARTIAL | ❌ REJECTED
│  Reason:    [Why — must cite code evidence]      │
│  Severity:  AGREE | UPGRADE → X | DOWNGRADE → X │
│  Fix:       AGREE | IMPROVED → [better fix]      │
└──────────────────────────────────────────────────┘
```

**Verdict rules:**
- **✅ CONFIRMED** — vulnerability is real, PoC is valid, severity is appropriate
- **⚠️ PARTIAL** — vulnerability exists but severity is wrong, PoC is incomplete, or fix is inadequate
- **❌ REJECTED** — false positive, non-exploitable in context, or already mitigated

**Validation thresholds:**
- **≥2 confirmations** from different teams → **VALIDATED** (full points)
- **≥2 rejections** from different teams → **INVALIDATED** (zero points, penalty to reporter)
- Otherwise → **DISPUTED** (50% points, flagged for human review)

### Phase 3 — Blue Team Synthesis (Team Shield)

After cross-review, activate Team Shield:

1. **Collect all VALIDATED findings** — deduplicated, with confirmed severity
2. **Adjudicate DISPUTED findings** — make a final call with cited reasoning
3. **Check fix compatibility** — do any proposed fixes conflict with each other?
4. **Produce the Hardening Plan:**
   - Ordered by priority (exploitability × impact)
   - Group related fixes that should be applied together
   - Flag fixes that might introduce regressions or break other fixes
   - Add defense-in-depth recommendations beyond the specific findings
   - Estimate blast radius: which files/features are affected

### Phase 4 — Scoring & Leaderboard

Compute final scores using [./references/scoring.md](./references/scoring.md) and produce the **Final Report** using [./references/report-templates.md](./references/report-templates.md).

## Mandatory Rules

1. **No fabrication.** Every finding must cite an exact file and line number with real code. If you can't prove it from the source, don't report it.
2. **No cross-team duplicates.** If two teams find the same vulnerability, the team with the better PoC claims it. The other gets 1 point for independent discovery.
3. **Cross-review is mandatory.** Skipping it invalidates the hackathon. Adversarial validation is the core value.
4. **Blue Team scores separately.** Shield cannot earn attack points — only defense and synthesis points.
5. **Severity criteria (strict):**
   - 🔴 **Critical** — Unauthenticated RCE, full data breach, account takeover without credentials
   - 🟠 **High** — Auth bypass, privilege escalation, significant data exposure requiring minimal conditions
   - 🟡 **Medium** — Requires authentication + additional steps, limited data exposure, denial of service
   - 🔵 **Low** — Information disclosure, missing best practices, defense-in-depth gaps
6. **Reviewers must be adversarial.** Confirming a weak finding to boost another team's score is collusion. Reviewers must actively try to disprove findings.
