<p align="center">
  <img src="https://img.shields.io/badge/Copilot-Skill-8957e5?style=for-the-badge&logo=github" alt="Copilot Skill" />
  <img src="https://img.shields.io/badge/Security-Hackathon-e53e3e?style=for-the-badge&logo=hackthebox&logoColor=white" alt="Security Hackathon" />
  <img src="https://img.shields.io/github/license/claudiovsky/security-hackaton-skill?style=for-the-badge" alt="License" />
</p>

<h1 align="center">🏴‍☠️ Security Hackathon Skill</h1>

<p align="center">
  <strong>A competitive, multi-team security audit — powered by a single GitHub Copilot prompt.</strong>
  <br />
  <em>5 Red Teams attack. Cross-reviews validate. A Blue Team hardens. All scored.</em>
</p>

<p align="center">
  <a href="#quickstart">Quickstart</a> •
  <a href="#how-it-works">How it works</a> •
  <a href="#teams">Teams</a> •
  <a href="#scoring">Scoring</a> •
  <a href="#example-output">Example output</a> •
  <a href="#customization">Customization</a> •
  <a href="#faq">FAQ</a>
</p>

---

## The Problem

Traditional security audits rely on **one reviewer, one perspective**. Even the best auditor has blind spots — they specialize in certain areas and rush through others. Worse, there's no adversarial validation: findings go unchallenged, false positives slip through, and severity assessments are subjective.

**This skill fixes that** by simulating a competitive security hackathon where:

- **5 specialized Red Teams** attack from different angles (auth, injection, data, infra, logic)
- **Every finding gets cross-reviewed** by 4 other teams — adversarial validation is mandatory
- **A Blue Team synthesizes** validated findings into a prioritized hardening plan
- **Everything is scored** — fabricated findings get penalized, quality PoCs get rewarded

The result: **higher coverage, fewer false positives, and a battle-tested remediation plan.**

---

## Quickstart

### 1. Install the skill

```bash
# Clone or download into your Copilot skills directory

# macOS / Linux
mkdir -p ~/.copilot/skills
git clone https://github.com/claudiovsky/security-hackaton-skill.git \
  ~/.copilot/skills/security-hackathon

# Windows (PowerShell)
New-Item -ItemType Directory -Force "$env:USERPROFILE\.copilot\skills" | Out-Null
git clone https://github.com/claudiovsky/security-hackaton-skill.git `
  "$env:USERPROFILE\.copilot\skills\security-hackathon"
```

> **Alternative:** Copy the `SKILL.md` and `references/` folder manually into `~/.copilot/skills/security-hackathon/`.

### 2. Run the hackathon

Open your project in VS Code, start a Copilot Chat in **Agent** mode, and type:

```
/security-hackathon
```

That's it. The skill handles the rest — reconnaissance, all 5 red team attacks, 20 cross-reviews, blue team synthesis, scoring, and the final report.

### 3. (Optional) Scope it

You can pass a scope hint if you don't want a full audit:

```
/security-hackathon auth + API only
```

```
/security-hackathon firestore rules and server actions
```

---

## How It Works

The hackathon runs in **5 phases**, all in a single Copilot session:

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│   Phase 0   BRIEFING                                    │
│             Director maps the codebase, identifies      │
│             entry points, notes stack & config           │
│                                                         │
│   Phase 1   RED TEAM ATTACKS                            │
│             5 teams run sequentially, each with          │
│             unique persona + 12-14 item checklist        │
│                                                         │
│   Phase 2   CROSS-REVIEW                                │
│             Each team reviews all other teams'           │
│             findings — confirm, dispute, or reject       │
│                                                         │
│   Phase 3   BLUE TEAM SYNTHESIS                         │
│             Shield collects validated findings,          │
│             checks fix compatibility, builds plan        │
│                                                         │
│   Phase 4   SCORING & FINAL REPORT                      │
│             Points computed, leaderboard generated,      │
│             full report with executive summary           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Why Sequential + Cross-Review?

The magic is in the **adversarial validation**. Without it, AI-generated findings often include:
- Theoretical vulnerabilities that aren't exploitable in context
- Severity inflation ("Critical!" for a missing header)
- Fabricated PoCs that don't match the actual code

Cross-review forces each finding to survive scrutiny from 4 other specialist teams. The result is dramatically higher signal-to-noise ratio.

---

<h2 id="teams">Teams</h2>

| # | Codename | Specialty | Checks |
|---|----------|-----------|--------|
| 🔴 | **Cerberus** | Auth, sessions, identity | 12 |
| 🔴 | **Hydra** | Input validation, injection, XSS | 12 |
| 🔴 | **Phantom** | Data exposure, privacy, IDOR | 12 |
| 🔴 | **Fortress** | Infrastructure, config, dependencies | 14 |
| 🔴 | **Paradox** | Business logic, race conditions | 12 |
| 🔵 | **Shield** | Defense synthesis & hardening | 8 responsibilities |

Each team has a **full persona** (mindset, expertise, and motivation) and a **detailed checklist** (see [`references/team-personas.md`](references/team-personas.md)).

### Finding Cards

Every vulnerability is reported as a structured **Finding Card**:

```
┌─────────────────────────────────────────────────┐
│  HYDRA-001               🟡 Medium              │
│─────────────────────────────────────────────────│
│  Title:   Prompt injection via chat input        │
│  File:    src/api/chat/route.ts:42               │
│  PoC:     1. Send "ignore all instructions..."   │
│           2. Model leaks system prompt            │
│  Impact:  System prompt disclosure                │
│  Fix:     Wrap user input in boundary markers     │
└─────────────────────────────────────────────────┘
```

### Cross-Review Verdicts

Every finding receives 4 independent reviews:

```
┌─ REVIEW: HYDRA-001 ← reviewed by Cerberus ──────┐
│  Verdict:   ✅ CONFIRMED                          │
│  Reason:    Tested — no boundary markers exist     │
│  Severity:  AGREE                                  │
│  Fix:       IMPROVED → also add rule 7 to prompt   │
└──────────────────────────────────────────────────┘
```

---

<h2 id="scoring">Scoring</h2>

The scoring system rewards **quality over quantity** and **penalizes fabrication**.

### Attack Points

| Severity | Points | With fix | 
|----------|--------|----------|
| 🔴 Critical | 10 | 15 |
| 🟠 High | 7 | 10.5 |
| 🟡 Medium | 4 | 6 |
| 🔵 Low | 1 | 1.5 |

### Validation

| Outcome | Effect |
|---------|--------|
| ≥2 teams confirm | **Validated** — full points |
| Mixed reviews | **Disputed** — 50% points |
| ≥2 teams reject | **Invalidated** — 0 points, -5 penalty |
| Fabricated finding | **-10 penalty** |

### Review Points

| Action | Points |
|--------|--------|
| Correctly confirmed real finding | +1 |
| Successfully rejected false positive | +3 |
| Correct severity adjustment | +2 |
| Improved fix accepted by Blue Team | +2 |

Full scoring details: [`references/scoring.md`](references/scoring.md)

---

<h2 id="example-output">Example Output</h2>

Here's what a hackathon run looks like:

```
═══════════════════════════════════════════════════
  🏁 HACKATHON BRIEFING
═══════════════════════════════════════════════════

  Project:      Acme Web App
  Stack:        Next.js, Firestore, AI Chat
  Commit:       a1b2c3d
  Scope:        Full application
  Entry Points: 2 API routes, 5 server actions, 3 forms
  Teams:        5 Red + 1 Blue

═══════════════════════════════════════════════════
```

And the final scoreboard:

```
═══════════════════════════════════════════════════════════
  🏆 FINAL SCOREBOARD
═══════════════════════════════════════════════════════════

  #  Team          Attack  Review  Penalty  TOTAL
  ── ──────────    ──────  ──────  ───────  ─────
  1. Cerberus      10.5    11      0        21.5
  2. Phantom       9.0     8       0        17.0
  3. Hydra         9.0     6       0        15.0
  4. Paradox       5.0     7       -5       7.0
  5. Fortress      1.5     5       0        6.5

  🔵 Shield        —       —       —        14

═══════════════════════════════════════════════════════════
  10 validated findings · 1 invalidated · 0 disputed
  Risk Score: 22
═══════════════════════════════════════════════════════════
```

---

<h2 id="customization">Customization</h2>

### Different stack? No problem.

The checklists are **stack-agnostic** — they check for vulnerability patterns, not framework-specific code. The skill works out of the box with:

| Stack | Auth checks | DB checks | Injection checks |
|-------|------------|-----------|-----------------|
| **Next.js + Firebase** | Session cookies, Admin SDK | Firestore rules, transactions | Server Actions, API routes |
| **Express + PostgreSQL** | JWT, passport.js | SQL queries, ORM | req.body, req.params |
| **Django + SQLite** | Django sessions | ORM queries | Forms, views |
| **Rails + MySQL** | Devise, sessions | ActiveRecord | Strong params, views |
| **SvelteKit + Supabase** | RLS, JWT | Supabase policies | Form actions, endpoints |

### Adding custom teams

Edit `references/team-personas.md` — add a new team section following the same format. Then update the team table in `SKILL.md`.

### Adjusting severity thresholds

Edit `references/scoring.md` to change point values, validation thresholds, or add custom penalty rules.

### Reducing scope

Pass a scope hint when invoking:

```
/security-hackathon auth layer only
/security-hackathon focus on API routes and database rules
```

---

<h2 id="faq">FAQ</h2>

<details>
<summary><strong>How long does a full hackathon take?</strong></summary>

It depends on codebase size. For a typical web app (10-30 source files), expect Copilot to work through all 5 phases in a single long session. The cross-review phase is the most thorough — 20 individual reviews (5 teams × 4 reviews each).

</details>

<details>
<summary><strong>Does this replace a professional pen test?</strong></summary>

No. This is a **defense-in-depth layer** — it catches common vulnerabilities, logic bugs, and configuration issues that manual review might miss. A professional pen test includes network-level testing, social engineering, and custom tooling that this skill cannot replicate.

</details>

<details>
<summary><strong>Why not run all teams in parallel?</strong></summary>

Cross-review requires all teams to have completed their attacks first. Sequential execution also avoids duplicate findings across teams — each team can see what previous teams found and focus on their own specialty.

</details>

<details>
<summary><strong>Can I use this in CI/CD?</strong></summary>

Not directly — this is a Copilot Chat skill designed for interactive use. However, you can use the output (finding cards, fix diffs) to create GitHub Issues or merge the suggested fixes.

</details>

<details>
<summary><strong>What models work best?</strong></summary>

Any model with strong reasoning capabilities. Claude Opus/Sonnet, GPT-4o, and Gemini Pro all produce good results. Larger context windows help — the cross-review phase references all previous findings.

</details>

<details>
<summary><strong>Can I contribute new team personas or checklists?</strong></summary>

Absolutely! See <a href="CONTRIBUTING.md">CONTRIBUTING.md</a> for guidelines.

</details>

---

## File Structure

```
security-hackathon/
├── SKILL.md                          # Main skill — the hackathon protocol
├── references/
│   ├── team-personas.md              # Team personas & checklists (62 checks)
│   ├── scoring.md                    # Point system & leaderboard format
│   └── report-templates.md           # Structured output templates
├── README.md                         # This file
├── CONTRIBUTING.md                   # Contribution guidelines
└── LICENSE                           # MIT License
```

---

## Contributing

PRs welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for details. The most impactful contributions:

- **New team personas** for specialized domains (mobile, API gateway, GraphQL, etc.)
- **Checklist improvements** based on real-world findings
- **Report template refinements** for different output formats
- **Translations** of team personas and checklists

---

## License

[MIT](LICENSE) — use it, fork it, break it, fix it.

---

<p align="center">
  <strong>Built with 🏴‍☠️ by <a href="https://github.com/claudiovsky">@claudiovsky</a></strong>
  <br />
  <em>When one auditor isn't enough, deploy a hackathon.</em>
</p>
