---
name: info-filter
description: >
  Information credibility filter for AI research workflows.
  Detects marketing fluff, survivorship bias, fabricated data, and AI-generated SEO spam
  in search results. Outputs findings with confidence ratings.
  信息过滤 — 识别营销软文、幸存者偏差、虚假数据和低质信息源。
version: 1.1.0
author: yxb
tags: [research, fact-check, information-filter, source-credibility, anti-marketing, misinformation]
trigger:
  keywords:
    # English
    - fact check
    - source credibility
    - misinformation filter
    - fake news detection
    - survivorship bias
    - marketing spam
    - information verification
    - trustworthiness
    # 中文
    - 信息过滤
    - 假信息
    - 虚假资料
    - 事实核查
    - 可信度
    - 信息来源
    - 软文识别
    - 幸存者偏差
  patterns:
    - "help me.*research"
    - "is this.*reliable"
    - "check if.*true"
    - "verify.*claim"
    - "帮我.*调研"
    - "搜索.*信息"
    - "查一下.*靠不靠谱"
    - "这个.*是真的吗"
---

# Information Credibility Filter

## 🎯 Problem Statement

When AI agents search for information, they frequently encounter three categories of unreliable content:

1. **Marketing disguised as information** — Advertorials and sponsored content posing as objective reviews or tutorials
2. **Survivorship bias** — Only extreme success stories get reported; failure rates and typical outcomes are invisible
3. **Inflated or fabricated data** — Unsourced statistics, exaggerated numbers, and misleading comparisons

This skill provides a systematic framework to filter, evaluate, and rate the credibility of information found during research.

## 📐 When to Activate

### MUST activate when:
- Using WebSearch / WebFetch to find information that will be cited in output
- Evaluating or comparing products/tools for the user
- Researching technical solutions and making recommendations
- Any search result will directly influence user decisions

### Skip when:
- User explicitly says casual/informal search is fine
- Pure conversation with no factual claims involved

## 🔍 Step 1: Source Tier Classification

Classify every search result into one of four trust tiers:

### Tier A — Direct Citation
- Official documentation (product docs, API references, pricing pages)
- Authoritative engineering blogs (Google AI Blog, Meta Engineering, etc.)
- Primary data sources (Statista, Gartner, IDC original reports)
- Government / regulatory body public data

### Tier B — Reference with Cross-Verification
- Independent reviews with explicit methodology and raw data shown
- Reputable tech community discussions (high-karma HN posts, Reddit r/xxx threads)
- Established tech media originals (The Verge, Ars Technica, 36Kr original, 少数派 original)
- High-karma Zhihu answers (check for conflicts of interest)

### Tier C — Leads Only, Never Cite Directly
- Personal blog / WeChat articles with no test data, pure opinion
- SEO content farms (clickbait titles, keyword stuffing, no author info)
- Baidu Jingyan / CSDN reposts
- Xiaohongshu / Douyin recommendation posts

### Tier D — Discard Immediately
- Anonymous content with unverifiable authorship
- Obvious advertorials (see red flag detection below)
- AI mass-generated SEO spam (see pattern recognition below)
- Rewritten/duplicated content with no new information

## 🚩 Step 2: Advertorial Red Flag Detection

If **≥ 2 red flags** are triggered, classify as marketing content → downgrade to Tier D.

### Language Red Flags
- [ ] Only praises, zero cons (or "the only downside is it's TOO good")
- [ ] Uses extreme comparison words ("crushes", "destroys", "miles better") without supporting data
- [ ] Ends with CTA to join WeChat group / get coupon / follow account / claim offer
- [ ] Refers to competitors vaguely ("some tools", "traditional solutions") instead of naming them
- [ ] Heavy use of low-barrier language ("anyone can do it", "zero experience needed", "learn in 3 minutes")
- [ ] "Free" appears ≥ 3 times without disclosing limitations

### Structure Red Flags
- [ ] Follows the classic ad funnel: pain point → product → results → act now
- [ ] Screenshots are all polished "before/after" — no actual UI screenshots
- [ ] No author info, or author is employee/partner of the product
- [ ] Comments are uniformly positive with vague content ("amazing", "thanks for sharing")

### Technical Red Flags
- [ ] Performance claims without methodology ("300% faster" but no test setup described)
- [ ] Comparison test conditions are clearly unequal (high-end vs. low-end)
- [ ] Cited "studies" or "reports" are unsourced or originate from the product itself

## 📊 Step 3: Survivorship Bias Detection

When search results present "success stories", you MUST ask:

### The Three Critical Questions
1. **What's the denominator?** — "100 people made $1M with XX" → How many total people tried? What's the failure rate?
2. **Where are the failures?** — If you can't find any failure/complaint/pitfall content, the information has been filtered
3. **What's special about this case?** — Were the subject's starting point, resources, and timing reproducible?

### Common Traps
- "XX tool helped me earn $10K/month" → omits their follower base, industry, time invested
- "This strategy has 50% conversion rate" → omits sample size and baseline comparison
- "Using XX made me 10x more efficient" → omits how low the original baseline was

### Counter-Strategy
Proactively search with negative keywords:
- `"<product> cons"` / `"<product> problems"`
- `"<product> vs <competitor>"` (look for comparative reviews)
- `"<product> failed"` / `"<product> doesn't work"`

If the ratio of positive to negative results is severely imbalanced (>5:1), explicitly flag in output: "Search results may exhibit survivorship bias."

## 🔢 Step 4: Data Credibility Scoring

Rate every key data point you plan to cite:

### 🟢 High Confidence — Cite Directly
- Tier A source + primary data origin + cross-verifiable
- Format: `claim (source: XX official docs/report)`

### 🟡 Medium Confidence — Must Flag Uncertainty
- Tier B source, or Tier A but data is indirect
- Format: `claim (source: XX, unverified)`

### 🔴 Low Confidence — Reference Only or Skip
- Tier C source, or cannot be cross-verified
- Format: `claim (source unclear / single source, for reference only)`

### ⚫ Unreliable — Discard
- Tier D source, or internally contradictory / defies common sense
- Do not cite; exclude from output

## 🤖 Step 5: AI-Generated Spam Detection

The following patterns suggest AI mass-produced SEO content:

- [ ] Article is very long (>3000 words) but low information density, repetitive
- [ ] Logical breaks between paragraphs, internal contradictions
- [ ] Keyword stuffing with unnatural sentence structure
- [ ] Images are generic AI illustrations unrelated to content
- [ ] Website has many articles with identical structure (template-based production)
- [ ] Domain is very new (<1 year) or WHOIS info is hidden

## 📝 Output Format

After research, clearly annotate sources and confidence levels:

```markdown
## Research Findings

### Key Discoveries
- Finding 1: XXX [🟢 High confidence — source: official docs]
- Finding 2: XXX [🟡 Medium confidence — source: independent review, small sample]
- Finding 3: XXX [⚠️ Survivorship bias risk — only success cases, no failure data found]

### Source Inventory
| # | Source | Tier | Confidence | Note |
|---|--------|------|------------|------|
| 1 | https://... | A | 🟢 | Official pricing page |
| 2 | https://... | B | 🟡 | Independent review |
| 3 | https://... | D | ⚫ | Discarded: advertorial |

### Information Gaps (honest disclosure of unknowns)
- XXX data — no primary source found
- XXX claim — could not be verified
```

## ⚡ Quick Decision Flowchart

```
Search result arrives
    │
    ▼
Tier A source? ──yes──→ Has primary data origin? ──yes──→ 🟢 Cite directly
    │                              │
    no                             no
    │                              │
    ▼                              ▼
Run red flag checks         🟡 Flag as "unverified"
    │
    ▼
≥ 2 red flags? ──yes──→ ⚫ Discard (marketing content)
    │
    no
    │
    ▼
Tier B source? ──yes──→ Cross-verifiable? ──yes──→ 🟢 High confidence
    │                              │
    no                             no
    │                              │
    ▼                              ▼
Tier C source?              🟡 Flag uncertainty
    │
    ▼
⚠️ Lead only — cite only if nothing better exists, must annotate
```

## 🛠 Search Techniques for Higher Signal-to-Noise

### Universal
- `site:github.com` — find primary technical docs
- `site:reddit.com` — find real user discussions
- `"review"` — find review content
- `-"sponsored"` `-"ad"` — exclude obvious ads
- `"alternative to"` — find comparison perspectives
- `"problem"` `"issue"` `"bug"` — find negative info for balance

### Chinese-Language Specific
- `site:zhihu.com` — Zhihu discussions (watch for conflicts of interest)
- `site:v2ex.com` — tech community real feedback
- `"<product> 踩坑"` / `"<product> 劝退"` — proactively find negatives
- `"<product> 替代品"` — find comparisons

## 📎 Integration with Other Skills

- **deep-research**: Embed this filter during the "fetch sources" phase
- **content-research-writer**: Use during pre-writing fact-checking
- **Xiaohongshu note workflow**: Auto-apply during "Step 2: verify information"

## 💡 Core Principles

1. **Better to under-cite than mis-cite** — If no reliable source exists, say "no reliable data found"; never fabricate or guess
2. **Flag uncertainty explicitly** — Medium/low confidence info must be labeled so users can judge for themselves
3. **Actively seek counter-evidence** — Every positive claim should be checked against negative evidence
4. **Honest about unknowns** — An "information gap" section is more valuable than a deceptively complete but wrong answer
5. **Denominator matters more than numerator** — Success stories without failure rates are meaningless
