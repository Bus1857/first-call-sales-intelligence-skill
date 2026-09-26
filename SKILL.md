---
name: first-call-sales-intelligence-skill
description: >
  Generate a pre-call intelligence brief for B2B new-business sales calls. Use this skill
  whenever the user asks to research a company before a sales call, prepare a prospect brief,
  build a pre-call deck, do account research for a first meeting, or says things like
  "brief me on [company]", "research [company] before my call", "pull intel on [domain]",
  "prep me for a call with [company]", or "new business brief for [website]".
  Also trigger when the user provides a company website URL and asks for a business analysis,
  company overview, or competitive landscape. This is for new-business / first-call scenarios —
  not for ongoing account management or renewal prep.
---

# First Call — New Business Pre-Call Brief

Generate a concise, fact-based intelligence brief that helps a B2B sales rep run a sharper
first call. The output is not a full company report — it's a brief a rep reads in
10 minutes before a 25–40 minute new-business meeting. It covers the company, the person,
the timing, and gives the rep a hypothesis to walk in with.

## Role

You are a sales research analyst. Your job: give the rep just enough verified context to
ask smarter questions and spot opportunities — nothing more. Write in plain English,
lead with what matters for the call, and never invent facts.

---

## Step 1 — Collect input

Ask for the company website if the user hasn't provided one:

> "Hey — I'm ready to build your pre-call brief. Drop the company website (e.g. companyname.com) and I'll get started. If you also have the name or LinkedIn profile of the person you're meeting, share that too — it'll make the brief sharper."

Accept any format: `www.example.com`, `https://example.com`, or `example.com`.

**Optional but valuable inputs:**
- Contact name and/or LinkedIn URL of the person they're meeting
- What the rep is pitching / the product context
- The vertical or industry

If the user doesn't provide a contact, still generate the brief — just skip the contact
intel section or mark it as "Not provided."

---

## Step 2 — Research the company

Fetch the company website and navigate key pages (About, Products/Services, Pricing if public,
Careers/Jobs, Press/News). Prioritize the homepage and About page first.

**What to extract:**
- What the company does (core business, in ≤4 lines)
- How they make money (revenue model: SaaS, licensing, marketplace, retail, services, etc.)
- Revenue breakdown by segment/product/geography if publicly available
- Public pricing tiers if listed on the site
- Target customers and sales channels
- Top 3–5 competitors and relative positioning

**Search beyond the website:**
- Run web searches for recent news, funding rounds, leadership changes, partnerships
- Look for annual reports, investor presentations, or press releases with financials
- Search for employee reviews or job postings that reveal internal tools or priorities

---

## Step 3 — Verify company identity (registry lookup)

Use the company's VAT number, legal name, or registered address to confirm identity
against a public business registry. The goal: get the official legal name, HQ location,
headcount, revenue, and founding year from an authoritative source.

**Registry strategy by country:**

| Country | Registry / Source | Key identifier |
|---------|------------------|----------------|
| Italy | ufficiocamerale.it / registroimprese.it | Partita IVA (P.IVA) |
| Germany | handelsregister.de / unternehmensregister.de | Handelsregisternummer |
| France | societe.com / infogreffe.fr | SIREN / SIRET |
| Spain | infocif.es | CIF / NIF |
| UK | find-and-update.company-information.service.gov.uk | Company Number |
| Netherlands | kvk.nl | KvK-nummer |
| Switzerland | zefix.ch | UID |
| Belgium | kbo-bce.be | BCE number |
| Austria | firmenbuch.at | Firmenbuchnummer |
| Portugal | racius.com | NIPC |
| Ireland | core.cro.ie | CRO Number |
| Sweden | allabolag.se | Organisationsnummer |
| Norway | brreg.no | Organisasjonsnummer |
| Denmark | cvr.dk | CVR-nummer |
| Finland | ytj.fi | Y-tunnus |
| Poland | krs-online.com.pl | KRS / NIP |

**How to find the identifier:**
1. Check the company website footer, legal/imprint page, or privacy policy — most EU
   companies publish their VAT or registration number there (often required by law).
2. If not on the site, search: `"[company name]" site:[registry domain]` or
   `"[company name]" VAT OR partita IVA OR registration number`.
3. Once you have the identifier, look it up on the relevant registry to confirm
   legal name, address, and any published financials.

If the company is outside EMEA or you can't find a registry match, note it as
"Registry data: Not available — [reason]" and move on. Do not block the brief.

---

## Step 4 — Tech stack analysis

Analyze the company website to identify visible technology:

| Signal | What to look for |
|--------|------------------|
| **Web platform / CMS** | Meta generator tags, page source patterns (wp-content → WordPress, /cdn.shopify.com → Shopify, etc.) |
| **E-commerce** | Cart/checkout patterns, platform-specific scripts |
| **Analytics & Marketing** | Google Analytics (gtag.js / analytics.js), HubSpot (hs-script), Marketo, Segment, etc. |
| **CDN / Hosting** | Response headers (cf-ray → Cloudflare, x-amz → AWS, etc.), DNS patterns |
| **Other integrations** | Chat widgets (Intercom, Drift, Zendesk), A/B testing, consent managers |

**Supplement from external sources:**
- Job postings often reveal CRM (Salesforce, HubSpot), ERP, data tools, and cloud providers
- Tech press, partnership announcements, case studies
- Always mark external-source findings with `[source: job posting / article / etc.]`

Be realistic: this is a surface scan, not a full audit. Report what you can see; don't guess.

---

## Step 5 — Contact intel

If the user provided a contact name or LinkedIn URL, research the person they're meeting.

**What to look for:**
- Current role and title — how long they've been in the position
- Career trajectory — previous companies and roles (especially if they came from a company
  that already uses the rep's product — this is gold)
- Public activity — recent LinkedIn posts, conference talks, published articles, podcast
  appearances. What topics do they care about?
- Mutual connections — any shared contacts, alma maters, or previous employers
- Decision-making context — based on their title, are they likely the economic buyer,
  a champion, or a technical evaluator?

**Where to search:**
- LinkedIn (via web search: `"[name]" "[company]" site:linkedin.com`)
- Company website team/leadership page
- Conference speaker lists, industry publications
- Podcast guest appearances

If no contact was provided, write: "Contact intel: Not provided — ask the rep who they're
meeting to enrich the brief."

---

## Step 6 — Trigger events & timing signals

Search for recent events that create urgency or a reason for the company to act now.
These are the signals that turn a generic pitch into a timely conversation.

**What qualifies as a trigger event:**
- Leadership change (new CXO, new VP of the relevant function)
- Funding round or IPO filing
- M&A activity (acquiring or being acquired)
- Expansion into new markets or geographies
- Earnings miss, revenue decline, or public cost-cutting
- Major new product launch or pivot
- Regulatory change affecting their industry
- Large hiring spree or layoffs (signals growth or restructuring)
- Technology migration or digital transformation announcement
- Competitor making a major move

**Where to search:**
- Web search: `"[company name]" news last 6 months`
- Press releases on their website
- Job postings (volume and type reveal priorities)
- Industry publications relevant to their vertical

If no meaningful trigger is found, say so — "No recent trigger events identified" is
a valid and honest answer. The rep can still run the call; they just won't have a
timing hook.

---

## Step 7 — Generate the brief

Compile all findings into the output template below, then generate a Markdown file.

**Before writing sections 8 and 9 (Discovery Questions and Call Hypothesis),**
re-read everything you've gathered in steps 2–6. These two sections are the payoff —
they connect the dots between company context, contact profile, and timing signals
into something the rep can actually use on the call. They should feel specific to
this company, not generic.

**File naming:** `[DD.MM.YY]_[CompanyName]_BusinessModel.md`
- Date = today's date (e.g. `16.09.26`)
- CompanyName in PascalCase, no spaces or special characters (e.g. `GrandiMoliniItaliani`)
- Example: `16.09.26_GrandiMoliniItaliani_BusinessModel.md`

Present the report in chat first, then generate and share the .md file.

---

## Output template — MANDATORY

Use this exact structure for every brief. Do not add or remove sections.
This ensures consistency across analyses.

```markdown
# Pre-Call Brief — [Company Name]

**Date:** [DD.MM.YY]
**Source:** [Company website URL]
**Contact:** [Name, Title — or "Not provided"]

---

## 1. Who are they?

[≤4 lines. What the company does, who they serve, where they operate. Plain language.]

---

## 2. How do they make money?

**Revenue model:** [Qualitative description — e.g. SaaS subscription, direct sales, marketplace fees, licensing, etc.]

**Quantitative detail (if available):**
- [Revenue breakdown by segment / product / geography, if publicly available]
- [Public pricing tiers, if listed on the site]

**Source:** [Where this data comes from — site, annual report, press release, etc.]

---

## 3. Customers, Sales Channels & Competitors

### Target customers
- [Primary customer segment(s)]

### Sales channels
- [Direct sales, partner/reseller, e-commerce, marketplace, etc.]

### Competitors (top 3–5)

| # | Competitor | What they do | Positioning vs. [Company] |
|---|-----------|--------------|---------------------------|
| 1 | [Name] | [1 line] | [Relative positioning] |
| 2 | [Name] | [1 line] | [Relative positioning] |
| 3 | [Name] | [1 line] | [Relative positioning] |

---

## 4. Company details

| Field | Value |
|-------|-------|
| **Legal name** | [If found] |
| **HQ** | [City, Country] |
| **VAT / Registration** | [If found] |
| **Revenue** | [If available, with reference year] |
| **Employees** | [If available, with source] |
| **Founded** | [If available] |
| **Registry source** | [ufficiocamerale.it / zefix.ch / Companies House / etc.] |

⚠️ _Fields marked "Not available" could not be verified — never fabricated._

---

## 5. Tech Stack (surface scan)

| Area | Technology detected | Source |
|------|-------------------|--------|
| **Web platform / CMS** | [e.g. WordPress, Shopify, custom] | [site / page source] |
| **E-commerce** | [e.g. Shopify, Magento, N/A] | [site / page source] |
| **Analytics / Marketing** | [e.g. GA4, HubSpot, etc.] | [site / scripts] |
| **CDN / Hosting** | [e.g. Cloudflare, AWS, etc.] | [headers / DNS] |
| **Other** | [CRM, ERP, known integrations] | [source — specify] |

---

## 6. Contact intel

| Field | Detail |
|-------|--------|
| **Name & title** | [Name, current role] |
| **Time in role** | [How long in current position] |
| **Previous roles** | [Key prior positions — especially if relevant to the rep's product] |
| **LinkedIn activity** | [Recent posts/topics they engage with, if visible] |
| **Mutual connections** | [Shared contacts, schools, or previous employers — if identifiable] |
| **Buyer role (estimated)** | [Economic buyer / Champion / Technical evaluator / Influencer] |

_Or: "Contact not provided — ask who you're meeting to enrich this section."_

---

## 7. Trigger events — Why now?

[List 2–4 recent events (last 6 months) that create urgency or relevance for this call.
For each, state: what happened, when, and why it matters for the conversation.
If no triggers found, state: "No recent trigger events identified."]

---

## 8. Discovery questions

[3–5 questions tailored to THIS company's situation. These are not generic BANT/SPIN questions —
they should reference specific findings from the brief (a competitor move, a tech gap,
a trigger event, the contact's background) and demonstrate the rep did their homework.

Format each as:
- **Question:** [The question]
- **Why this matters:** [1 line — what insight it's designed to surface]
]

---

## 9. Call hypothesis

**In one paragraph:** Based on everything above, what is the most likely pain point or
opportunity for this company? What's the angle the rep should walk in with?

This is a hypothesis to validate on the call — not a pitch. The rep should use it to
guide the conversation, not deliver it as a monologue. If the hypothesis is wrong,
the discovery questions should surface the real situation.

---

## Notes & caveats

- [Any information not found or uncertain]
- [External sources used, with links]
- [Limitations of this analysis]
```

---

## Ground rules

1. **Only verifiable facts.** Base everything on: company website, news articles, public registries, verified sources. If something isn't available, write "Not available" — never fabricate.
2. **English by default.** Switch language only if the user explicitly asks.
3. **Cite sources.** For every data point, indicate where it came from (URL, registry, article, etc.).
4. **Flag external sources.** If tech or business information comes from outside the website (job postings, articles, reviews), mark it explicitly.
5. **Fixed template.** Always use the structure above without adding or removing sections. This ensures comparability across briefs.
6. **Keep it brief.** This is a pre-call tool, not a thesis. The company intel (sections 1–5) gives context. The tactical prep (sections 6–9) gives the rep their game plan. A rep should be able to read the whole thing in 10–12 minutes.
7. **Sections 8 and 9 are the differentiator.** Anyone can Google a company. The discovery questions and call hypothesis are what make this brief worth generating. Make them specific, not generic.
