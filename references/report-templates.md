# Report Templates

## Individual Team Report

Each Red Team produces this at the end of Phase 1:

```
╔═══════════════════════════════════════════════════════════╗
║  TEAM [CODENAME] — ATTACK REPORT                        ║
║  Hackathon: [Project Name]                               ║
║  Date: [Date]                                            ║
╠═══════════════════════════════════════════════════════════╣

  Files Analyzed:
  - [file1]
  - [file2]
  ...

  ─── FINDINGS ────────────────────────────────────────────

  [Finding Cards — see SKILL.md Phase 1 format]

  ─── SUMMARY ─────────────────────────────────────────────

  Total Findings: [N]
  🔴 Critical: [n]    🟠 High: [n]
  🟡 Medium:   [n]    🔵 Low:  [n]
  Raw Attack Score: [computed]

  Areas NOT in scope for this team:
  - [list what was deliberately skipped / out of specialty]

╚═══════════════════════════════════════════════════════════╝
```

## Cross-Review Summary

Each team produces this for every other team's report:

```
╔═══════════════════════════════════════════════════════════╗
║  CROSS-REVIEW: [REVIEWER] → [REVIEWED TEAM]             ║
╠═══════════════════════════════════════════════════════════╣

  [Review Verdicts — see SKILL.md Phase 2 format]

  ─── REVIEW SUMMARY ─────────────────────────────────────

  Findings Reviewed: [N]
  ✅ Confirmed: [n]
  ⚠️ Partial:   [n]
  ❌ Rejected:  [n]
  Severity Adjustments: [n]
  Improved Fixes Proposed: [n]

╚═══════════════════════════════════════════════════════════╝
```

## Final Hackathon Report

The Director produces this after all phases:

```
╔═══════════════════════════════════════════════════════════════╗
║                                                               ║
║   🏆  SECURITY HACKATHON — FINAL REPORT                      ║
║                                                               ║
║   Project:  [name]                                            ║
║   Date:     [date]                                            ║
║   Commit:   [SHA]                                             ║
║   Director: GitHub Copilot (security-hackathon skill)         ║
║                                                               ║
╠═══════════════════════════════════════════════════════════════╣

  ══ 1. SCOREBOARD ════════════════════════════════════════════

  [Leaderboard — see scoring.md format]

  ══ 2. EXECUTIVE SUMMARY ════════════════════════════════════

  Total unique vulnerabilities: [N]
  Validated (cross-review confirmed): [n]
  Disputed (under debate):            [n]
  Invalidated (false positives):      [n]

  | Severity      | Validated | Disputed | Invalidated |
  |---------------|-----------|----------|-------------|
  | 🔴 Critical   | [n]       | [n]      | [n]         |
  | 🟠 High       | [n]       | [n]      | [n]         |
  | 🟡 Medium     | [n]       | [n]      | [n]         |
  | 🔵 Low        | [n]       | [n]      | [n]         |

  Risk Score (validated only): [Critical×10 + High×7 + Medium×4 + Low×1]

  ══ 3. VALIDATED VULNERABILITIES ════════════════════════════

  Ordered by severity, then by exploitability.

  ### [FINDING_ID] — [Title]
  - **Severity:** [emoji] [level] (confirmed by [Team A], [Team B])
  - **Found by:** [Team]
  - **File:** [path:line]
  - **PoC:** [summary]
  - **Impact:** [what's at risk]
  - **Accepted Fix:**
    ```diff
    - [old code]
    + [new code]
    ```
  - **Fix Notes:** [any caveats from Blue Team]

  [... repeat for each validated finding ...]

  ══ 4. DISPUTED FINDINGS ════════════════════════════════════

  These findings had mixed reviews. Human judgment recommended.

  ### [FINDING_ID] — [Title]
  - **Found by:** [Team]
  - **Confirmed by:** [Teams]
  - **Rejected by:** [Teams]
  - **Blue Team verdict:** [ACCEPT | REJECT | NEEDS INVESTIGATION]
  - **Reasoning:** [explanation]

  [... repeat ...]

  ══ 5. INVALIDATED FINDINGS ═════════════════════════════════

  Listed for transparency. These were rejected by ≥2 teams.

  | ID | Title | Reporter | Reason for Rejection |
  |----|-------|----------|---------------------|
  | [id] | [title] | [team] | [reason] |

  ══ 6. BLUE TEAM HARDENING PLAN ═════════════════════════════

  ### Priority 1 — Immediate (exploitable now)
  1. [Fix description] — [files affected]
  2. ...

  ### Priority 2 — Short-term (requires specific conditions)
  1. ...

  ### Priority 3 — Defense-in-depth (not exploitable but reduces surface)
  1. ...

  ### Fix Compatibility Notes
  - [Any conflicts between proposed fixes]
  - [Fixes that must be applied together]
  - [Regression risks]

  ### Blind Spots
  Areas not covered by any Red Team:
  - [area 1]
  - [area 2]

  ══ 7. STATISTICS ═══════════════════════════════════════════

  | Metric | Value |
  |--------|-------|
  | Total files analyzed | [n] |
  | Total findings reported | [n] |
  | Validation rate | [validated/total]% |
  | False positive rate | [invalidated/total]% |
  | Cross-reviews performed | [n] |
  | Average reviews per finding | [n] |
  | MVP Finding | [FINDING_ID] by [Team] |
  | Best Reviewer | [Team] — [reason] |

╚═══════════════════════════════════════════════════════════════╝
```
