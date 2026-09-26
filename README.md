# First Call Sales Intelligence Skill

AI skill for generating fact-based B2B pre-call intelligence briefs, including company research, tech stack, contact intel, trigger events and tailored discovery questions.

The skill prepares a concise, evidence-led briefing for a first meeting with a potential customer. It combines public company information and user-provided context into a practical call hypothesis and tailored discovery questions.

## What you provide

Required:
- The company website or domain.

Optional:
- The contact's name or LinkedIn profile.
- The product or solution being discussed.
- The company's vertical or industry.

If no contact is provided, the skill still prepares the company brief and marks contact intelligence as not provided.

## Workflow

The skill asks for missing company input, then researches the company's website and other public sources. It checks company identity against an appropriate public registry when possible, scans public website signals for visible technologies, researches a named contact when provided, and looks for recent events that may affect timing. It then connects the findings into discovery questions and a call hypothesis.

Research follows the fixed nine-section brief template in `SKILL.md`. Facts should be cited, outside sources identified, and unavailable details labeled as unavailable. The registry lookup and technology scan are best-effort research steps; they do not block the brief when evidence cannot be found.

## Output

A Markdown pre-call brief with:

1. Company overview
2. Revenue model and public pricing or financial details
3. Customers, sales channels and competitors
4. Company and registry details
5. A surface scan of visible technology
6. Contact intelligence, when a contact is supplied
7. Recent trigger events
8. Tailored discovery questions
9. A call hypothesis to validate in the meeting

The skill instructs the assistant to present the report in chat and generate a Markdown file named `[DD.MM.YY]_[CompanyName]_BusinessModel.md`.

## Limitations

- The brief relies on publicly accessible information and the research tools available in the AI environment running the skill. Coverage and freshness can vary.
- A website technology scan is a surface scan, not a security or infrastructure audit. Detected tools may be incomplete or ambiguous.
- Registry coverage and published financial or headcount data vary by country and company. Unverified fields must remain marked unavailable.
- Contact details, LinkedIn activity, mutual connections and inferred buyer roles may not be publicly visible. The skill should not infer private facts.
- Trigger events are time-sensitive; the skill looks for recent events, but the research date and source links should be reviewed before the call.
- Competitor positioning and the call hypothesis are research-based starting points, not confirmed internal knowledge. Validate them with the prospect.

## Use

Copy `SKILL.md` into the skills directory supported by your AI assistant, or provide it as the assistant's instructions for a research task. Supply the company's website and any optional context, such as the contact and product being discussed. The skill is written in English and uses a fixed report structure.

See [`examples/example-brief.md`](examples/example-brief.md) for a short, explicitly fictional illustration of the output format.

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE).
