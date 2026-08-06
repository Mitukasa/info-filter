# Examples

This folder contains real conversation comparisons showing the difference Info Filter makes.

## Files

- **baseline-without-filter.txt** — Agent research output WITHOUT Info Filter
  - Topic: "Is it true that AI side hustles can earn 10,000+ RMB per month?"
  - Issues: No source credibility ratings, survivorship bias undetected, marketing content not filtered
  
- **results-with-filter.txt** — Agent research output WITH Info Filter enabled
  - Same topic, same search
  - Improvements: Source tier classification (A/B/C/D), credibility ratings (🟢🟡🔴⚫), survivorship bias detection, marketing red flags identified

## Key Differences

| Aspect | Without Filter | With Filter |
|--------|---------------|-------------|
| Core conclusion | "Some people achieved it" (implies replicable) | "Most earn <1000 RMB, 90% of claims are survivorship bias" |
| Source handling | Mixed citations, no credibility check | Tiered ratings with confidence levels |
| Survivorship bias | Not detected | Actively questioned: denominator? failures? special conditions? |
| Marketing content | Not identified | Red flag detection, D-tier content discarded |
| User impact | Potentially misleading | Helps set realistic expectations |

## How to Reproduce

1. Ask your AI agent: "AI副业月入过万是真的吗？" (or "Is it true that AI side hustles can earn $1500+/month?")
2. Compare the output with and without Info Filter installed
3. Notice the difference in source handling, bias detection, and conclusion quality

Tested and verified by Claude Code on 2026-08-06
