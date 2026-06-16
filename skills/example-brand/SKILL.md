---
name: example-brand
description: Template brand skill — voice, tokens, banned verbs, advisory stance, audiences. This is a placeholder, not a real brand. Copy it to skills/{your-brand}/SKILL.md and replace every value with your product's real details so pmstack's subagents speak in your brand voice.
---

# Example brand skill (template)

This file is a **template**, not a real brand. It documents the structure pmstack's subagents expect from a brand skill. To use it:

1. Copy this file to `skills/{your-brand}/SKILL.md`.
2. Replace every `{placeholder}` and example value with your product's real details.
3. Reference your brand skill from your repo's `.pmstack/positioning.md` so the subagents route to it.

The sharper and more honest this file is, the sharper the copy, audits, and critiques pmstack produces. Vague values produce vague output.

## Identity

- **Public name:** {the name you market as}.
- **Codebase name(s):** {repo/app names, if they differ from the public name}.
- **One-line positioning:** The {fastest/clearest/only} way for {audience} to {core outcome}.
- **Tagline:** {your locked tagline}.
- **Memorable thing:** the single sentence a customer would repeat to a friend.

## Aesthetic

- **Name:** {give your aesthetic a name — e.g. "Calm utility", "Editorial bold"}.
- **Signature device:** {the one visual motif that's unmistakably yours, if any}.
- **Anti-aesthetic:** {what you deliberately avoid — generic SaaS gradients, stock photography, etc.}.

## Typography

| Role | Family | Source |
|---|---|---|
| Display / headings | {Font} | {Google Fonts / self-hosted} |
| Body | {Font} | {…} |
| Data / labels / mono | {Font} | {…} |

*If you target a non-English language or diacritics, note any font that renders them incorrectly — this is load-bearing for the copywriter (e.g. some serifs mis-position macrons/accents at display size).*

## Color tokens

| Role | Hex | Notes |
|---|---|---|
| Primary | `#000000` | {where it's allowed — e.g. accents only, never full-bleed gradient} |
| Background | `#FFFFFF` | |
| Surface | `#FFFFFF` | cards, inputs |
| Ink (text) | `#111111` | |
| Muted text | `#666666` | must pass WCAG AA on background |
| Accent / signal | `#000000` | {success / warning / risk colors, if you use a scale} |

## Voice + advisory stance

- **Language:** {primary language, e.g. `lang="en"`}.
- **Stance:** {interpretive vs. advisory — how prescriptive is the brand allowed to be? Can it recommend, or only present?}.
- **Strategic line in copy:** {the one sentence that captures the stance, e.g. "Facts and signals — you decide."}.

### Banned verbs / phrases (load-bearing)

The conversion copywriter treats this list as **hard rules**. List every word/phrase your brand never uses:

- {off-brand or off-stance verbs — e.g. recommendatory verbs if your stance is non-advisory}.
- "comprehensive" / "all-in-one" / "complete" — only if your product genuinely covers everything; otherwise this is a false claim.
- "industry-leading" / "best-in-class" / "#1" — unprovable superlatives.
- "trusted by thousands" / any fabricated social proof.

### Allowed framing

- {how the brand IS allowed to make claims, with concrete examples}.
- {structured comparisons, cited data, decision-support framing, etc.}.

## Audiences

One block per first-class audience. Add or remove as needed.

### 1. {Segment name} ({B2C / B2B})
- **JTBD:** {the job they hire the product for}.
- **Proof available:** {testimonials / case studies you actually have — or "none yet"}.
- **Primary CTA:** {what the button says}. *If no proof exists yet, route to lead capture, not a purchase button.*
- **Pricing:** {quote the price, or "do not quote — route to contact"}.

### 2. {Segment name} ({B2C / B2B})
- **JTBD:** {…}
- **Proof available:** {…}
- **Primary CTA:** {…}
- **Pricing:** {…}

## Shipped capabilities

List only what is **real and live today**. The copywriter and trust auditor cite these as present-tense:

- {shipped feature}
- {shipped feature}

## NOT shipped (do not market as present-tense)

The trust auditor **blocks** copy that claims these as live:

- {roadmap feature not yet built}
- {real testimonials / case studies you don't have yet}
- {refund or guarantee policies not actually committed}

## Legal / honesty constraints

- {any regulatory exposure — claims you legally cannot make in your market/sector}.
- {data or coverage gaps that make a "comprehensive" / "all risks" claim false}.
- **No fabricated stats.** Any number in copy ("2,400+ users", "98% accuracy") must trace to a real, documented source or it does not ship.
