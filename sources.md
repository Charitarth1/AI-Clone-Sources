# Sources — Weekly Signal Feed
*Version 1.1 · May 2026 · For use by Agent 6 (signal parser) and the Sunday/Wednesday managed agents*

---

## How this file is used

The Sunday and Wednesday managed agents read this file for signal criteria, pillar assignments, and what to ignore. They fetch stories using a hybrid approach:

- **RSS feeds** for web publications (compact, low token cost)
- **Gmail inbox** for newsletters you subscribe to (even lower cost — plain text, already in your inbox)
- **Direct WebFetch** for regulatory bodies with no RSS or newsletter (EU AI Office, OPC, OSFI)

Agent 6 (Daily Signal Parser) also reads this file when triggered manually with "Parse signals:" or "Daily brief:".

To add or remove a source: edit this file and push to GitHub. The next agent run picks it up automatically. When adding a newsletter source, also add its sender domain to the Gmail filter in the routine prompt at claude.ai/code/routines.

For the Mistral-first pipeline (Section 6e of Agents.md):
```bash
ollama run mistral "$(cat sources.md)" > tagged_items.json
```

---

## Source List

### Tier 1 — Check every week
*High signal-to-noise. Directly grounded in LinkedIn post history and subscriptions.*

| Source | URL | What to look for |
|---|---|---|
| WIRED | https://wired.com/tag/artificial-intelligence/ | AI governance, power concentration, tech policy (cited directly in archive) |
| MIT Technology Review | https://technologyreview.com/topic/artificial-intelligence/ | AI safety, foundation model developments, governance policy |
| The Verge | https://theverge.com/ai-artificial-intelligence | AI product and policy coverage, named company decisions |
| 404 Media | https://404media.co | Investigative tech journalism, algorithmic harm, surveillance |
| Axios — Technology | https://axios.com/technology | Fast-moving AI and tech policy news, regulatory developments |
| TechCrunch — AI | https://techcrunch.com/category/artificial-intelligence/ | AI company news, governance and regulatory developments |
| Fast Company — Technology | https://fastcompany.com/technology | AI and work, enterprise AI adoption, leadership perspective |
| IAPP (International Association of Privacy Professionals) | https://iapp.org/news/a/ | Privacy law, AI regulation, PIPEDA and GDPR enforcement updates |
| ICO (UK Information Commissioner) | https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/ | UK data protection and AI regulatory guidance (active subscription) |
| Michael Geist's blog | https://michaelgeist.ca | Canadian tech law, AI policy, digital sovereignty (cited by name in content) |
| Import AI (Jack Clark) | https://importai.substack.com | Weekly AI research digest, safety and capability developments |
| GZERO Media | https://gzeromedia.com/artificial-intelligence | AI geopolitics, US-China-EU power dynamics (active subscription) |
| Gary Marcus — The Road to AI We Can Trust | https://garymarcus.substack.com | AI hype debunking, specific wrong claims named (creator reference) |
| EU AI Office | https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai | EU AI Act guidance, implementation updates |
| arXiv — CS.AI + CS.CY | https://arxiv.org/list/cs.AI/recent and https://arxiv.org/list/cs.CY/recent | New AI research preprints: safety, governance, fairness, bias, surveillance. cs.AI = core AI research. cs.CY = computers and society (governance angle). |
| Collider | ⚠ URL TBD — confirm which publication | Flagged: the main "Collider" covers film/TV entertainment, which conflicts with persona constraints. Confirm the correct source and update this row. |
| Sci-Hub | ⚠ Not recommended as an agent source | Sci-Hub hosts paywalled papers without authorization — legal exposure for automated access. Not a discovery feed either (no "recent papers" to browse). arXiv covers most AI research as free preprints. Flag if you need a specific paywalled paper and we can find an alternative. |

---

### Tier 2 — Check most weeks
*High relevance, moderate posting frequency.*

| Source | URL | What to look for |
|---|---|---|
| Stanford HAI | https://hai.stanford.edu/news | Policy research, governance frameworks (active subscription: Stanford Tech Impact) |
| Columbia SIPA | https://sipa.columbia.edu/news | Policy analysis, international AI governance (active subscription) |
| Al Jazeera — Technology | https://aljazeera.com/tag/technology/ | Global South AI story, non-Western perspectives (active subscription) |
| Ethan Mollick — One Useful Thing | https://oneusefulthing.substack.com | Evidence-backed AI analysis, practical governance implications (creator reference) |
| CIGI | https://cigionline.org/topics/technology/ | Canadian and international AI governance, digital sovereignty |
| OPC (Office of the Privacy Commissioner of Canada) | https://priv.gc.ca/en/opc-news/ | PIPEDA enforcement, Bill C-27 updates |
| AI Now Institute | https://ainowinstitute.org | AI accountability, power concentration research |
| The Markup | https://themarkup.org | Algorithmic accountability investigations, named case studies |

---

### Tier 3 — Check when time allows
*Useful for specific pillars; lower weekly frequency.*

| Source | URL | Pillar focus |
|---|---|---|
| MediaNama | https://medianama.com | India AI and tech policy, Aadhaar, surveillance (Pillar 7) |
| The Wire — Science and Tech | https://science.thewire.in | India AI deployment, governance failures (Pillar 7) |
| newslaundry — Tech | https://newslaundry.com/technology | India AI accountability journalism (active subscription) |
| ThePrint — Technology | https://theprint.in/category/tech/ | India AI and politics intersection (active subscription) |
| NIST AI | https://nist.gov/artificial-intelligence | AI RMF updates, standards guidance (Pillar 2) |
| Future of Privacy Forum | https://fpf.org/blog/ | Privacy and AI governance intersection (Pillars 2, 7) |
| House Foreign Affairs Committee | https://foreignaffairs.house.gov/press-releases/ | US-China AI geopolitics, export controls (Pillar 6) (active subscription) |
| OSFI | https://osfi-bsif.gc.ca/en/news-events/news/ | Canadian financial sector AI regulation, B-13 updates (Pillar 2) |
| Hogan Lovells AI blog | https://hldataprotection.com | AI legal developments, EU and Canada regulatory commentary (active subscription) |
| Policy Options (IRPP) | https://policyoptions.irpp.org | Canadian policy debates, AI and digital rights |

---

## Fetch method reference

How each source is accessed by the managed agents. Update this table when adding new sources.

### RSS feeds (web sources)

These are fetched as RSS, not full web pages. Much lower token cost. Update the routine prompts if you change these URLs.

| Source | RSS URL |
|---|---|
| WIRED AI | https://www.wired.com/feed/tag/artificial-intelligence/latest/rss |
| MIT Technology Review | https://www.technologyreview.com/feed/ |
| The Verge AI | https://www.theverge.com/rss/ai-artificial-intelligence/index.xml |
| 404 Media | https://www.404media.co/rss/ |
| TechCrunch AI | https://techcrunch.com/category/artificial-intelligence/feed/ |
| Axios Tech | https://api.axios.com/feed/ |
| The Markup | https://themarkup.org/feeds/rss.xml |
| AI Now Institute | https://ainowinstitute.org/feed |
| arXiv cs.AI | https://arxiv.org/rss/cs.AI |
| arXiv cs.CY | https://arxiv.org/rss/cs.CY |

### Gmail newsletters (inbox read — sender-scoped only)

These are read directly from the Gmail inbox using `mcp__claude_ai_Gmail__search_threads` with an exact sender filter. The agent never reads emails outside this filter. Sunday run uses `newer_than:7d`; Wednesday run uses `newer_than:3d`.

| Newsletter | Gmail sender domain |
|---|---|
| Import AI (Jack Clark) | importai.substack.com |
| Gary Marcus — The Road to AI We Can Trust | garymarcus.substack.com |
| Ethan Mollick — One Useful Thing | oneusefulthing.substack.com |
| IAPP | iapp.org |
| ICO (UK) — news and blogs | ico.org.uk |
| Michael Geist's blog | michaelgeist.ca |
| GZERO Media | gzeromedia.com |
| Hogan Lovells AI blog | hldataprotection.com |

To add a newsletter to Gmail reads: add its sender domain to this table, then update the `from:(...)` filter in both routine prompts at https://claude.ai/code/routines.

### Direct WebFetch (no RSS or newsletter)

These sources have no reliable RSS feed and don't send newsletters. Fetched directly only when the RSS + Gmail scan has not yet found 3 qualifying stories (Sunday) or 2 HOT stories (Wednesday).

| Source | URL |
|---|---|
| EU AI Office | https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai |
| OPC (Canada) | https://priv.gc.ca/en/opc-news/ |
| OSFI | https://osfi-bsif.gc.ca/en/news-events/news/ |
| Fast Company — Technology | https://fastcompany.com/technology |
| Stanford HAI | https://hai.stanford.edu/news |
| Columbia SIPA | https://sipa.columbia.edu/news |

---

## Pillar-to-source mapping

| Pillar | Primary sources |
|---|---|
| 1 — AI Literacy as Power | MIT Tech Review, WIRED, Import AI, Fast Company, arXiv cs.CY |
| 2 — Responsible AI and Governance | ICO, EU AI Office, NIST AI, OPC, OSFI, Hogan Lovells, IAPP, arXiv cs.CY |
| 3 — Human-Centric Technology | AI Now Institute, The Markup, 404 Media, Stanford HAI, arXiv cs.CY |
| 4 — AI as Civilizational Inflection | Import AI, Gary Marcus, Stanford HAI, GZERO, arXiv cs.AI |
| 5 — The Entrepreneurship Wave | MIT Tech Review, WIRED, One Useful Thing, Fast Company |
| 6 — AI Democratization vs Concentration | GZERO, Al Jazeera, House Foreign Affairs, Import AI, Axios |
| 7 — State Surveillance and AI | The Markup, 404 Media, AI Now Institute, MediaNama, The Wire, ICO |
| 8 — AI, Jobs, and Creative Destruction | MIT Tech Review, WIRED, Fast Company, CIGI, Columbia SIPA |

---

## What to look for — signal criteria

This section tells the agent what kinds of stories are worth flagging. Scan each source for stories that match one or more of these criteria. Ignore everything else.

---

### Always flag — highest priority

These topics are core content territory. Any story touching them is a candidate:

**Regulatory and policy moves:**
- EU AI Act: new implementing rules, enforcement actions, exemption debates, member state interpretations
- Canadian AI legislation: Bill C-27, AIDA, OPC enforcement actions, government AI procurement decisions
- PIPEDA violations involving AI or automated decision-making
- OSFI guidance updates on AI in financial services
- ICO guidance on AI and data protection (UK)
- NIST AI RMF or ISO 42001 updates, new sector-specific guidance
- US executive orders, congressional bills, or regulatory agency guidance on AI
- Any G7 or OECD AI governance statement

**Named company decisions with governance implications:**
- OpenAI, Anthropic, Google DeepMind, Meta: infrastructure decisions, safety commitments, governance announcements
- Microsoft: cloud sovereignty claims, Copilot deployment scope, government contracts
- Any major cloud provider (AWS, Azure, GCP) making claims about data sovereignty or AI governance
- Enterprise AI deployments at scale — especially in healthcare, finance, hiring, or government
- AI vendor contracts with governments (any country)

**Accountability and failure:**
- Named AI system causing documented harm (bias, errors, discrimination)
- Whistleblower reports about AI safety or governance failures
- Investigative journalism into how a specific AI system actually works vs. how it is described
- Court cases, regulatory fines, or enforcement actions involving AI
- Research papers documenting specific performance gaps, bias, or safety failures

**Power concentration:**
- Compute infrastructure moves: data centres, chip supply, cloud dominance
- Foundation model market consolidation
- Any story about who controls AI infrastructure and what that means
- Open source vs. closed source AI governance debates
- AI export controls, international AI supply chain

**State surveillance:**
- Government deployment of facial recognition, predictive policing, or social scoring
- Aadhaar or India's national AI infrastructure developments
- Surveillance tools sold by named companies to named governments
- Biometric data collection by public institutions
- Any story about AI being used to monitor citizens, protestors, or minorities

---

### Flag if the angle is strong — secondary priority

These are worth flagging only if there is a specific, non-obvious angle beyond the surface story:

- AI and jobs: only if the story names a specific policy response, a company's actual displacement numbers, or a worker organizing angle — not generic "AI will replace X% of jobs" speculation
- AI literacy and public understanding: only if it names a specific gap, a specific misleading claim by a named actor, or a specific educational or policy initiative
- AI entrepreneurship: only if it names a structural shift in how individuals or small organizations can build with AI, not product launches
- Geopolitical AI dynamics: US-China AI race stories that name specific capability gaps, export control decisions, or diplomatic moves — not general commentary

---

### Ignore — do not flag

- AI product reviews, benchmark comparisons, or "which model is best" stories without a governance angle
- Speculative "AI will do X in 10 years" without evidence or named actor
- Celebrity or entertainment AI stories (AI in music, film, gaming) unless there is a rights or surveillance dimension
- AI art and image generation debates unless tied to IP law or named enforcement
- Company earnings calls and valuation stories without governance implications
- Press releases from AI vendors describing their own responsible AI initiatives (flag only if a named third party independently verifies or challenges the claim)

---

### What makes a story HOT vs WARM vs SHELF

**HOT** — all three are true:
- Published in the last 7 days
- Names a specific actor, decision, or finding (not vague)
- Has a non-obvious angle beyond the headline

**WARM** — one or two are true, or HOT but the angle needs development time

**SHELF** — worth noting because a pattern is building, but the right moment to post is 2-4 weeks away (e.g., a regulatory consultation that closes in a month, a trial verdict that is pending)

---

### Consulting signal tag

Flag separately any story that implies an organizational need — not a content angle, but a signal that organizations will need expert help:
- New regulation with a compliance deadline
- Named enforcement action that sets a precedent
- New standard published that requires policy updates
- High-profile AI failure that triggers board-level scrutiny

These are logged as consulting signals. Not used for content during brand-building phase.

---

## Update log

| Date | Change |
|---|---|
| May 2026 | Full rebuild from LinkedIn archive, YouTube subscriptions, and content pillar analysis |
| May 2026 | Added The Verge, 404 Media, Axios, TechCrunch, Fast Company, IAPP to Tier 1. Collider flagged pending clarification. |
| May 2026 | v1.1: Switched fetch architecture to RSS-first + Gmail newsletter reads. Added Fetch method reference section. Prompt-level fetch budget guardrails added to both routines. Gmail sender-scoped reads for 8 newsletter sources. |
