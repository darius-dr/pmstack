# ICP: Pirkėjai ir pardavėjai (B2C)

*Worked example produced by `/pm:audience buyers-sellers` against Relando. Demonstrates the audience-researcher output contract.*

## Snapshot

Lithuanian residents aged 25–55, mid-purchase decision on a single property worth €30k–€500k (sklypas / namas / butas), often first-time or once-a-decade buyers with limited domain knowledge. Sellers are the symmetric case: owners pricing a property and trying to pre-empt buyer objections.

## Job-to-be-done

> When I've found a property I might buy in Lithuania, I want to verify what could go wrong with it before I sign, so I can either negotiate the price down or walk away without losing my deposit.

## Top 3 functional needs

1. **Surface what the seller didn't mention** — easements, restrictions, encumbrances, stalled construction, planning-zone limits.
2. **Translate registry data into plain Lithuanian** — RC fields, BP/TPDR codes, paskirties grupė names are opaque without help.
3. **Quantify the financial picture** — annual NT mokestis, žemės mokestis, notaro atlygis, hipotekos lakštas, GPM if reselling. Calculator-grade, not estimates.

## Top 3 emotional needs

1. **Permission to walk away.** Buyers need explicit reasons (named restrictions, dated court cases) — vague "feels risky" isn't enough.
2. **Authority to negotiate.** A cited document beats a gut feeling at the table.
3. **Relief, not anxiety.** The product surfaces risk to resolve it, not amplify it. Tone matters.

## Top 5 objections + disarmers

| Objection | Disarmer | Evidence | Status |
|---|---|---|---|
| "€49 is a lot — I'd rather just ask the realtor." | Lawyers charge €200-500+ for the same scope; realtor is the seller's agent, not the buyer's. | `Reportus/claude.md §Value Proposition`, `Reportus/docs/PRD.md` | proof-backed |
| "How do I know the data is real?" | Every fact cites an official source (Registrų centras, Geoportal, Regia). Source attributions appear next to each section. | `Reportus_Web/DESIGN.md §Landing Page IA pillar 8`, V2 sample reports | proof-backed |
| "Will I understand the report?" | AI santrauka explains every field in plain Lithuanian; the NT Asistentas chat answers follow-up questions. | `Reportus/claude.md §Konsultantas chat` | proof-backed |
| "What if it tells me to buy when I shouldn't?" | The report doesn't recommend — it presents facts and structured pros/cons/unknowns. You decide. | `Reportus_Web/REDESIGN-PLAN.md §0` (advisory stance lock), `Reportus/.planning/notes/chat-with-report-design.md §2` | proof-backed |
| "I'm a seller — why would I pay to find problems with my own property?" | The same report flags the buyer's likely concerns BEFORE they ask, so you can price accurately and answer objections preemptively. | `Reportus_Web/REDESIGN-PLAN.md §2` (seller sub-angle) | needs-interview *(seller stories not yet captured)* |

## Proof available today

- Three live sample reports (`/ataskaitos/sklypas/1-37196`, `/namas/5-12345`, `/butas/2-58104`) — anonymous visitors can chat with NT Asistentas on them.
- 14+ documented official data sources in `Reportus/docs/PRD.md §Data Sources Reference`.
- 100+ data-point taxonomy per property type in the same file.

**B2C testimonials currently in `lib/data.ts` are flagged as placeholders.** Until real ones are captured, do not anchor copy on testimonial quotes.

## Primary CTA

**Patikrinti objektą** (2 words, verb + object, Lithuanian).

## Secondary CTA

**Naršyti žemėlapį →** (existing in hero per `Reportus_Web/CLAUDE.md §Key Patterns`).

## Banned framing for this segment

- **No anxiety amplification.** "Don't make a €200,000 mistake" reads as anxiety-bait. Acknowledge stakes; don't dramatize them.
- **No fake urgency.** "Limited time", "act now", countdown timers — forbidden.
- **No condescension.** Buyers may not know RC field codes; they're not children. Explain without "easy enough for anyone".
- **No "everyone uses it".** Until real numbers are documented, popularity claims are out.

## Tone + voice notes

- **Register:** warm professional. Closer to "investigative journalist" than "SaaS landing page".
- **Vocabulary:** plain Lithuanian. When a technical term has to appear (paskirties grupė, BP, TPDR), define it once in context.
- **Sentence length:** medium. Hero subs ≤20 words; body sentences average 12-18.
- **Pronouns:** address the buyer in second-person singular informal (*tu*) — matches the "you decide" stance. The chat already uses this register.
- **Confidence:** declarative. *"Štai ką žinome. Štai ko nežinome."* — not *"galbūt"* / *"galima"*.

## Open research questions

- What % of LT property buyers have actually walked away from a deal due to discovered restrictions? (validates the "permission to walk away" frame)
- Do sellers actually pre-buy due-diligence reports anywhere? (validates the seller sub-angle)
- What does the average buyer currently do BEFORE finding Relando? (informs the "before" leg of BAB)
- How long after first hearing about Relando do buyers actually purchase a report? (informs CTA timing + remarketing)
- Trust ranking: do buyers trust "AI summary" or "official source citation" more? (informs hero proof order)

---
*Source MDs consulted: `Reportus/claude.md`, `Reportus/docs/PRD.md`, `Reportus/.planning/notes/chat-with-report-design.md`, `Reportus_Web/CLAUDE.md`, `Reportus_Web/DESIGN.md`, `Reportus_Web/REDESIGN-PLAN.md`, `Reportus_Web/TODOS.md`, `Reportus/TODOS.md`.*
