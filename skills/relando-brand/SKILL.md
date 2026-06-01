---
name: relando-brand
description: The Relando brand — voice, tokens, banned verbs, advisory stance, audiences. Use when working on the Relando site (reportus-web.vercel.app, relando.com). Replace with your own brand skill for other projects.
---

# Relando brand skill

Example brand skill packaged with pmstack to demonstrate the pattern. If you're working on a different brand, copy this file to `skills/{your-brand}/SKILL.md` and override the values.

## Identity

- **Public name:** Relando.
- **Codebase names:** Reportus (backend app), Reportus_Web (marketing site repo).
- **Legacy PRD name:** EstateReport (deprecated — do not use in copy).
- **Site:** [relando.com](https://relando.com) (currently reportus-web.vercel.app).
- **Tagline (locked 2026-05-29):** *Vienas objektas. Viena aiški ataskaita.*
- **Memorable thing:** *We catch the hidden problem the seller won't tell you, before you buy.*

## Aesthetic

- **Name:** Forensic Clarity (light warm-paper intelligence dossier).
- **Hybrid layer (REDESIGN-PLAN.md 2026-05-29):** Oversized type + full-bleed deep-purple bands for credibility/CTA moments + a "reveal / redaction" signature motif (▮▮▮▮ resolving to a real datum in amber).
- **Anti-aesthetic:** marketplace red (Aruodas), bright SaaS purple gradients, generic cool-gray dashboards.

## Typography

| Role | Family | Source |
|---|---|---|
| Display / headings | **Newsreader** (variable, optical sizing) | Google Fonts |
| Body | **DM Sans** | Google Fonts |
| Data / labels / cadastral | **IBM Plex Mono** (tabular-nums) | Google Fonts |

**Lithuanian diacritic note (load-bearing):** Newsreader renders the ū macron correctly. Fraunces does NOT (it mis-positions the macron in "Manufaktūrų", "būtina"). Inter is fine for body but the editorial register calls for Newsreader. Never propose Fraunces, Playfair without diacritic verification, or any serif without LT testing.

## Color tokens

| Role | Hex | Notes |
|---|---|---|
| Primary purple (anchor) | `#7C5CFF` | Seal/accent only. **Never** a full-bleed gradient. |
| Primary hover | `#6B4FE0` | |
| Deep purple (intelligence surfaces) | `#2B1B5A` | AI summary header, footer, full-bleed credibility band. |
| Paper (background) | `#F6F4EF` | Warm off-white. |
| Surface | `#FFFFFF` | Cards, inputs. |
| Surface-2 (alt sections) | `#FBF9F3` | Section alternation. |
| Ink (text) | `#191510` | Warm near-black. |
| Muted text | `#6E6555` | Passes WCAG AA on paper. |
| Hairline / border | `#E6E0D4` | |
| Amber (risk found) | `#E8A33D` chip, `#B5650F` text, `#FBEBD2` bg | Signal: hidden issue. |
| Lime (verified) | `#A6FF4D` fill, `#16320A` text on lime | Signal: clear / safe. |

**Risk scale:** critical `#EF4444` → warning `#F97316` → caution `#FACC15` → good `#A6FF4D` → safe `#22C55E`.

## Voice + advisory stance

- **Language:** Lithuanian (`lang="lt"`).
- **Stance:** Interpretive, NEVER advisory. The product gives facts, signals, and structured pros/cons/unknowns; the user decides.
- **Strategic line in copy:** *"Faktai ir signalai — tu sprendi."*

### Banned verbs / phrases (load-bearing)

Never use these in copy:
- `rekomenduojama` / `rekomenduojame`
- `verta` / `vertėtų`
- `geriau būtų` / `geriausia`
- `tinkamas` / `netinkamas` (when implying purchase-fit verdict)
- `siūlome` (in advisory sense — fine in "what we offer" sense)
- `patartina`
- "comprehensive" / "all-in-one" / "complete" (in English versions) — Relando does NOT comprehensively cover encumbrances per the LEGAL TODO; RC API lacks mortgage/arrest/servitude data.
- "industry-leading", "best-in-class", "#1" — banned brand-wide.
- "Trusted by thousands" / similar fabricated proof.

### Allowed framing

- Present data: *"Sklypo paskirties grupė leidžia mažaaukštės gyvenamosios paskirties statybą."*
- Surface risks: *"Dalis sklypo patenka į apsaugos zoną — patikrinkite konkrečias sąlygas."*
- Structured pros/cons/unknowns: *"Pliusai: … · Minusai: … · Neištirta: …"*
- Decision-support: *"Štai ką žinome. Štai ko nežinome. Sprendimą priimi tu."*

## Audiences (locked per REDESIGN-PLAN.md 2026-05-29)

Three audiences, all first-class from launch:

### 1. Pirkėjai ir pardavėjai (B2C)
- **JTBD:** Avoid overpaying / hidden problems before signing.
- **Sub-angle (sellers):** *Parduodi? Nustatyk teisingą kainą ir atsakyk į pirkėjo klausimus iš anksto — su ta pačia ataskaita.*
- **Proof available:** B2C testimonials in `lib/data.ts` (currently placeholder per REDESIGN-PLAN flag).
- **Primary CTA:** *Patikrinti objektą / Gauti ataskaitą.*
- **Pricing:** €49 single, €86 double, €124 triple (per `lib/data.ts`; REDESIGN-PLAN flags as stale).

### 2. Brokeriai / agentūros (B2B pro)
- **JTBD:** Close faster, look credible, reduce liability, do client due diligence without manual digging.
- **Proof available:** None yet. CTA must route to lead capture.
- **Primary CTA:** *Brokeriams →* (route to `/brokeriams` or contact form). Do NOT use purchase CTA.
- **Pricing:** Do not quote. *"Susisiekime"* / *"Pakalbėkime apie komandos planą."*

### 3. Vystytojai (B2B pro)
- **JTBD:** Assess parcel potential + constraints before acquisition.
- **Proof available:** None yet. CTA = lead capture.
- **Primary CTA:** *Vystytojams →*
- **Pricing:** Do not quote.

## Shipped capabilities (Q2 2026)

These are real and citable in copy:
- Sklypas / Namas / Butas V2 reports (sample-data state, not live RC API yet).
- Mokesčiai calculator (live, with 2026 LT tax formulas — notaras, RC registracija, hipoteka, NTM, žemės mokestis, GPM).
- AI chat ("NT Asistentas") — report-grounded, citation-chip linked.
- Parcel map (locked satellite + cadastral PMTiles overlay).
- Distance dial map (POIs, 250/500/1000m rings).
- Market-value zone map (regia.lt-style zone polygon + sandoriai dots — Phase 1 mocked, Phase 2 will use real RC sandorių feed).

## NOT shipped (do not market as present-tense)

- Live RC API for ownership/encumbrances (encumbrance data, mortgages, arrests, servitudes are not available from the RC public API per LEGAL TODO).
- Email-report-link delivery after Stripe checkout (planned).
- Multi-report credit redemption (paid for, not deliverable yet — `lib/data.ts` 2/3-report packages have no redemption UX).
- Real broker / developer testimonials.
- Agency dashboard / white-label portal (mentioned aspirationally; do not present as live).
- Refund guarantee (no policy committed).

## Competitive landscape

- **Direct competitors in LT:** none.
- **Indirect alternatives:** lawyers/notaries (€200-500+ per transaction), real estate agents (limited due diligence), manual research.
- **Marketplace competitors (NOT direct):** Aruodas, Domoplius — they sell listings, not due diligence.
- **International comparables:** PropertyLens (US), Cotality (B2B-focused).
- **Closest LT analog by UX:** dp-market.com (the reason the hero map exists per the validation-waived decision).

## Critical legal / honesty constraints

1. **Encumbrance gap (LEGAL TODO in `/Users/darius/Reportus/TODOS.md`):** RC API does NOT return mortgage, arrest, servitude, or SŽNS data. Any "comprehensive due diligence" / "all risks revealed" claim is potentially misleading under EU Directive 2005/29/EC.

2. **Advisory contradiction:** REDESIGN-PLAN.md 2026-05-29 explicitly resolves this — site adopts the product's interpretive stance ("faktai ir signalai — tu sprendi"). Drop "rekomendacijos / išvados" language from the site.

3. **Placeholder content:** Current B2C testimonials in `lib/data.ts` are flagged as placeholders. Must be replaced with real ones OR removed before paid acquisition.

4. **No fabricated stats:** Anything like "2,400+ reports", "98% accuracy", "10,000 satisfied buyers" is forbidden until real numbers exist.

## When in doubt

Read these files in order:
1. `/Users/darius/Reportus_Web/REDESIGN-PLAN.md` — most current positioning.
2. `/Users/darius/Reportus_Web/DESIGN.md` — visual system.
3. `/Users/darius/Reportus_Web/CLAUDE.md` — site spec.
4. `/Users/darius/Reportus/TODOS.md` — what's actually broken / risky.
5. `/Users/darius/Reportus/docs/PRD.md` — product reference (legacy "EstateReport" naming; treat as background, not source of truth).
