🇺🇸 English | 🇨🇳 [中文](README.zh.md)

# Info Filter — Information Credibility Filter

> Transform your AI Agent's research output from "search engine copy-paste" to "credible information analyst"

## 🚀 Quick Install

### Method 1: Ask Your AI Agent (Recommended)

In Claude Code, Cursor, Codex, or any AI agent that supports skills, just say:

```text
Please help me install this skill:
https://github.com/Mitukasa/info-filter
```

### Method 2: One-Line Command

```bash
npx skills add Mitukasa/info-filter -g

# Or clone directly
git clone https://github.com/Mitukasa/info-filter.git ~/.claude/skills/info-filter
```

### Method 3: Manual

```bash
git clone https://github.com/Mitukasa/info-filter.git
cp -r info-filter ~/.claude/skills/
```

After installation, trigger with `/info-filter` or naturally: `"Help me research if XXX is reliable"`.

---

## 🎯 The Problem

When you ask an AI Agent to research a question, is the answer trustworthy?

We ran a controlled experiment: asked the same Agent the same question — **"Can you really earn $1,500+/month with AI side hustles?"**

### Without Info Filter:

```
Conclusion: Some people did achieve it, but it's not "easy" or "zero barrier"

Real income data:
- Zhihu user: $2,000+/month (15+ orders at $140 each)
- SMZDM user: $600/month initially, scalable to $1,500+
- Regular users: $700-800/month (4-6 orders)

✅ Viable directions: AI art commissions, AI video production, AI writing...

One-line summary: AI side hustle $1,500+/month is not a myth, but not magically easy either.
```

**Looks objective? But it has fatal problems:**

1. ❌ **Treats extreme cases as normal** — "$2,000/month" and "$600/month" presented side by side, implying this is common
2. ❌ **No denominator** — How many people tried? What's the success rate? Never mentioned
3. ❌ **No source credibility check** — Zhihu personal stories, platform data, and marketing spam mixed together
4. ❌ **No negative evidence search** — No failure cases, scam reports, or statistical data
5. ❌ **Overly optimistic conclusion** — "Some people did it" implies it's replicable, when it's actually extremely rare

### With Info Filter:

```
Bottom line: Very few people achieve this. Most earn under $140/month.
90%+ of "$1,500+/month" content is marketing or survivorship bias.

📊 Real income data (cross-verified from multiple sources)
┌────────────────────────┬─────────────────────────┬──────────────────────────┐
│      Data Source       │      Income Level       │      Credibility         │
├────────────────────────┼─────────────────────────┼──────────────────────────┤
│ SMZDM platform data    │ Avg $125/month, 60%+    │ 🟢 High (platform stats) │
│                        │ under $110              │                          │
├────────────────────────┼─────────────────────────┼──────────────────────────┤
│ Zhihu author 1-year    │ $640/month ($7,700/yr)  │ 🟢 High (monthly detail) │
│ record                 │                         │                          │
├────────────────────────┼─────────────────────────┼──────────────────────────┤
│ Blogger 8-month track  │ $110→$480→$1,650→$4,800 │ 🟡 Medium (survivorship  │
│                        │                         │ bias possible)           │
├────────────────────────┼─────────────────────────┼──────────────────────────┤
│ YouTube - $20K/month   │ (DISCARDED)             │ ⚫ Tier D: obvious click- │
│                        │                         │ bait, no data            │
└────────────────────────┴─────────────────────────┴──────────────────────────┘

🚩 Survivorship bias detection:
1. What's the denominator? → SMZDM data: avg $125/month, most earn very little
2. Where are the failures? → CCTV report: AI training camp scam victims
3. What's special about success cases? → $4,800/month blogger didn't disclose follower base

📌 Information gaps (honest disclosure):
- Specific failure rate: No large-scale statistics found
- Long-term income curve: No 2+ year tracking data available
```

**Key differences:**

| Dimension | Without Filter | With Filter |
|-----------|---------------|-------------|
| **Core conclusion** | "Some people did it" (implies replicable) | "Very few people, most earn <$140/month" |
| **Data sources** | Mixed, no credibility check | Tiered ratings (A/B/C/D + 🟢🟡🔴⚫) |
| **Survivorship bias** | Not detected | Actively questions: denominator? failures? special conditions? |
| **Marketing content** | Not identified | Red flag detection, Tier D content discarded |
| **Negative evidence** | Not searched | Searched scam reports, failure cases |
| **Information gaps** | Not disclosed | Honestly states "what we don't know" |
| **Impact on user** | Potentially misleading | Helps set realistic expectations |

---

## 🔥 6 Fatal Flaws in Agent Information Search

### 1️⃣ Polluted by Marketing Spam

Search engine first 3 pages are full of:
- SEO content farm mass-produced low-quality articles
- Advertorials disguised as reviews
- Clickbait for traffic

**If agents quote without discrimination, they treat marketing copy as facts.**

---

### 2️⃣ Information Quoted Without Verification

Agents tend to "quote whatever they find", lacking:
- Multi-source cross-verification
- Primary data tracing
- Data credibility assessment

**Case:** A blog claims "300% efficiency improvement", agent quotes directly without asking: What's the test method? Sample size? Baseline comparison?

---

### 3️⃣ Survivorship Bias is Pervasive

Search results show far more "success stories" than "failure stories" because:
- Successful people are more willing to share
- Failures stay silent
- Media loves dramatic stories

**If agents don't proactively search for counter-evidence, they reach overly optimistic conclusions.**

---

### 4️⃣ No Source Credibility Differentiation

Agents treat these equally:
- Official documentation (Tier A)
- Independent reviews (Tier B)
- Personal blogs (Tier C)
- Anonymous posts (Tier D)

**Without grading, users can't tell which information is trustworthy.**

---

### 5️⃣ No Negative Evidence Search

Agents typically do "confirmation search" — stop once they find evidence supporting a viewpoint, never:
- Proactively search "XX cons"
- Search "XX failure cases"
- Search "XX vs competitor" comparisons

**Result: Information asymmetry, conclusions biased to single perspective.**

---

### 6️⃣ Information Gaps Not Transparent

Agents tend to give "seemingly complete" answers, even when:
- Some data has no primary source
- Some claims are unverifiable
- Some areas lack research

**An honest "I don't know" is more valuable than a "seemingly complete but wrong" answer.**

---

## 💡 How Info Filter Works

### 📐 Source Tier System

| Tier | Description | Usage |
|------|-------------|-------|
| **A** | Official docs, authoritative media, primary data | Cite directly |
| **B** | Independent reviews, reputable community discussions | Cross-verify first |
| **C** | Personal blogs, content farms | Lead only |
| **D** | Anonymous content, obvious ads | Discard immediately |

### 🚩 Advertorial Red Flag Detection

12 specific red flags (language/structure/technical), ≥2 triggers = classified as marketing:
- Only praises, zero cons
- Extreme comparison words without data
- CTA to join WeChat / get coupons at the end
- Performance claims without methodology
- ...

### 📊 Survivorship Bias Detection

Three mandatory questions:
1. **What's the denominator?** — Success rate = successes / total attempts
2. **Where are the failures?** — Can't find failure content = information has been filtered
3. **What's special about this case?** — Is the starting point, resources, timing reproducible?

### 🔢 Data Credibility Scoring

- 🟢 **High confidence** — Tier A source + primary data + cross-verifiable
- 🟡 **Medium confidence** — Tier B source or indirect data
- 🔴 **Low confidence** — Tier C source or unverifiable
- ⚫ **Unreliable** — Tier D source, discard

### 📝 Transparent Output Format

```markdown
## Research Findings

### Key Discoveries
- Finding 1 [🟢 High confidence — source: official docs]
- Finding 2 [🟡 Medium confidence — source: independent review, small sample]
- Finding 3 [⚠️ Survivorship bias risk — only success cases]

### Source Inventory
| # | Source | Tier | Confidence | Note |
|---|--------|------|------------|------|
| 1 | ...    | A    | 🟢         | ...  |
| 2 | ...    | D    | ⚫         | Discarded: advertorial |

### Information Gaps (honest disclosure)
- XXX data — no primary source found
- XXX claim — could not be verified
```

---

## 🤔 Who Needs This?

**Regular users:** Avoid being misled by marketing, get more truthful research conclusions, make more rational decisions

**Content creators:** More credible content, avoid citing fake data, build professional image

**Enterprises:** More accurate market research, more objective competitor analysis, more reliable decision basis

---

## 📖 Full Documentation

Detailed rules, decision flowchart, search techniques: [SKILL.md](./SKILL.md)

---

## 📄 License

MIT

---

## 🤝 Contributing

Issues and PRs welcome! Especially:
- New red flag detection rules
- Trigger keywords in more languages
- Real-world use case sharing
- Translations

---

## 💬 Feedback

- Submit an [Issue](https://github.com/Mitukasa/info-filter/issues)
- Join the [Discussion](https://github.com/Mitukasa/info-filter/discussions)

---

**Make every AI Agent search more credible.**
