# Hackathon Scoring System

## Point Values

### Attack Points (Red Teams)

| Category | Points |
|----------|--------|
| 🔴 Critical vulnerability found | 10 |
| 🟠 High vulnerability found | 7 |
| 🟡 Medium vulnerability found | 4 |
| 🔵 Low vulnerability found | 1 |
| Fix provided with valid diff | ×1.5 multiplier on finding |
| Independent discovery (same vuln as another team) | 1 bonus |

### Review Points (Cross-Review)

| Category | Points |
|----------|--------|
| ✅ Correctly confirmed a real finding | +1 |
| ❌ Successfully rejected a false positive (agreed by ≥1 other reviewer) | +3 |
| ⚠️ Correct severity adjustment (confirmed by Blue Team) | +2 |
| Improved fix accepted by Blue Team | +2 |
| Incorrectly rejected a valid finding | -2 |
| Failed to spot an obvious false positive | -1 |

### Defense Points (Blue Team Only)

| Category | Points |
|----------|--------|
| Correct adjudication of disputed finding | +3 |
| Fix compatibility conflict identified | +3 |
| Regression risk identified | +2 |
| Defense-in-depth recommendation (novel, not from red teams) | +2 |
| Blind spot identified (area no red team covered) | +4 |

### Penalties

| Category | Points |
|----------|--------|
| Fabricated finding (no code evidence) | -10 |
| Severity inflation (≥2 reviewers downgrade) | -3 |
| Finding invalidated (≥2 rejections) | -5 |
| Duplicate of another team's finding (lower quality PoC) | 0 (no points) |

## Score Computation

### Per-Team Raw Attack Score

```
raw_attack = Σ (finding_severity_points × fix_multiplier)
           + independent_discovery_bonuses
           - penalties
```

### Per-Team Review Score

```
review_score = Σ review_points (from cross-reviewing other teams)
```

### Validation Adjustment

After cross-review:
- VALIDATED findings (≥2 confirmations): full points
- DISPUTED findings (<2 confirmations, <2 rejections): 50% points
- INVALIDATED findings (≥2 rejections): 0 points + penalty

### Final Score

```
final_score = validated_attack_points + (disputed_attack_points × 0.5) + review_score
```

## Leaderboard Format

```
═══════════════════════════════════════════════════════════
  🏆 FINAL SCOREBOARD
═══════════════════════════════════════════════════════════

  #  Team          Attack  Review  Penalty  TOTAL
  ── ──────────    ──────  ──────  ───────  ─────
  1. [Winner]      [pts]   [pts]   [pts]    [pts]
  2. [Runner-up]   [pts]   [pts]   [pts]    [pts]
  3. [Third]       [pts]   [pts]   [pts]    [pts]
  4. [Fourth]      [pts]   [pts]   [pts]    [pts]
  5. [Fifth]       [pts]   [pts]   [pts]    [pts]

  🔵 Shield       —       —       —        [defense pts]

═══════════════════════════════════════════════════════════
  MVP Finding:  [FINDING_ID] by [TEAM] — [title]
  Best Review:  [TEAM] — [reason]
═══════════════════════════════════════════════════════════
```

## Tiebreaker Rules

1. Higher attack score wins
2. If tied: fewer penalties wins
3. If still tied: first team to find the highest-severity finding wins
