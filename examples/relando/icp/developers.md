# ICP: Vystytojai (B2B pro — real-estate developers)

*Worked example produced by `/pm:audience developers`.*

## Snapshot

LT real-estate developers — small to mid-sized firms acquiring sklypai for residential or mixed-use projects, doing constant parcel-evaluation work to find sites that pencil out. Numerate, planning-savvy, allergic to surprises post-acquisition.

## Job-to-be-done

> When I'm evaluating a parcel for potential acquisition, I want to know fast whether the planning indicators, infrastructure availability, and legal constraints support the project we'd want to build, so I can stop wasting time on parcels that don't pencil and move faster on the ones that do.

## Top 3 functional needs

1. **Užstatymo galimybės at a glance** — G1/G2 codes, Uₜ/Uᵢ indicators, max height, min green-space, paskirties grupė restrictions.
2. **Infrastructure feasibility** — elektros galia, dujų prieinamumas, vandentiekio + nuotekų atstumai, prisijungimo kaštai. The numbers that decide if a project is buildable.
3. **Legal-constraint inventory** — SŽNS, servitutai, saugomos teritorijos, kultūros paveldas, apribojimai disponuoti. Anything that limits what can be built or sold.

## Top 3 emotional needs

1. **Speed.** A developer evaluating 20 parcels a quarter cannot afford a 2-day due-diligence pass per parcel.
2. **Confidence in completeness.** Missing a SŽNS overlay after acquisition is a project-killer.
3. **Plausibility check.** Before committing legal/architect/financing resources, a fast yes/no on whether the parcel is worth deeper investigation.

## Top 5 objections + disarmers

| Objection | Disarmer | Evidence | Status |
|---|---|---|---|
| "We already have an in-house process for this." | The product compresses the routine pulls (RC, Geoportal, Regia, Planuoju Statau, ESO, Ambergrid) into one fetch + standardized output. Use it as the first-pass filter; your in-house process kicks in on shortlisted parcels. | shipped data sources | needs-interview *(adoption pattern not yet validated)* |
| "Per-object €49 doesn't scale for portfolio screening." | Volume pricing is a separate conversation — talk to us. | REDESIGN-PLAN §0 (B2B = Susisiekime) | proof-backed (positioning) |
| "Will the data go stale by the time we close?" | Sources are pulled fresh per request from the official portals. Each section cites the source and the pull timestamp. (Cadastral data in tile assets refreshes quarterly per `Reportus_Web/.planning/intel/decisions.md D13`.) | shipped + D13 | proof-backed |
| "Encumbrance data — mortgages, arrests — does this catch all of it?" | **Be honest:** RC public API does NOT return mortgage, arrest, or servitude data today. The product covers what's publicly available; for full encumbrance review, a notary or full RC paid extract is still needed. The product surfaces planning constraints, infrastructure, market value zone, and tax exposure — that's the load-bearing pre-acquisition work. | `Reportus/TODOS.md` (LEGAL TODO) | proof-backed (and load-bearing for honesty) |
| "What format is the output? Can our analysts work with it?" | Web report + PDF export (PDF planned, not shipped — flag honestly). The data points are also exposed as structured fields if API access is needed downstream — also separate conversation. | PRD FR4.7 (PDF planned), API access listed B2B-future | needs-interview *(PDF export status)* |

## Proof available today

- Live Užstatymo galimybės + Infrastruktūra cards on the Sklypas sample report (`/ataskaitos/sklypas/1-37196`).
- Distance-dial map showing proximity to amenities (Phase 1 hardcoded; Phase 2 will derive from OSM + city anchors).
- Market-value zone evidence (regia.lt-style zone polygon + comparable sandoriai).

**No developer testimonials, pilots, or case studies yet.** Lead-capture CTA only.

## Primary CTA

**Vystytojams →** (routes to `/vystytojams` or a contact form: "Tell us about your pipeline.")

## Secondary CTA

**Pavyzdys: Stirnų g. 35 sklypas →** (deep-link to the sklypas sample report — the most relevant artifact for this audience).

## Banned framing for this segment

- **No "comprehensive risk".** The encumbrance gap is real; do not overpromise.
- **No "AI-powered insights" as a value prop.** Developers care about the underlying data sources and pulls — the AI is a presentation layer, not the value.
- **No B2C anxiety framing.** Developers are not "anxious buyers"; they're operators.
- **No "modern" / "transformative" / "next-generation" language.** Pros tune it out instantly.

## Tone + voice notes

- **Register:** operator-to-operator. Cite specific data points + sources, not marketing claims.
- **Vocabulary:** dense with domain terms — Uₜ, Uᵢ, G1/G2, SŽNS, TPDR, detalusis planas. No definitions; assume fluency.
- **Sentence length:** short, declarative. Show numbers.
- **Pronouns:** formal plural (*Jūs / Jūsų komandai*) or business-collective (*komandoms*).
- **Confidence:** quantitative. Where you can cite a specific data field, do.

## Open research questions

- What's a developer's current pipeline-screening cost per parcel (time + analyst hours)? Validates the time-savings claim.
- How many parcels does a typical small-to-mid LT developer screen per year? Sets ceiling on annual usage.
- What integrations matter (Excel export, API, BIM-tool plug-ins)? Could shape B2B product surface.
- Are developers more sensitive to encumbrance-data completeness OR to planning-data freshness? Drives roadmap priority.
- Which competitor (HNIT-Baltic, GeoBaltica, hand-rolled in-house) is the displacement target?

---
*Source MDs consulted: `Reportus_Web/REDESIGN-PLAN.md §2`, `Reportus/docs/PRD.md §Report Data Specification — Užstatymo galimybės + Infrastruktūra`, `Reportus/claude.md §V2 Report Architecture`, `Reportus_Web/.planning/intel/decisions.md`, `Reportus/TODOS.md` (LEGAL TODO).*
