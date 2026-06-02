---
name: intake-questionnaire
description: Forcing-questions catalog + pushback rules for the /pm:office-hours intake interview. Used when MD context is missing or sparse and positioning has to come from a live conversation.
---

# Intake questionnaire

A sharp positioning brief comes from a sharp conversation. This skill provides the question catalog and pushback rules for `/pm:office-hours`.

## Structure

Seven forcing questions + four context questions. Run them in order; skip a question only if its answer is already documented in the repo (pre-flight read).

## The seven forcing questions

### Q1 — The party test (north-star + product clarity)

> "If a stranger asked you at a party 'so what do you do?', what's the ONE sentence you'd say? Don't give me a tagline. Tell me what you'd actually say."

**Why this works:** strips marketing speak. People defending a tagline write differently than people explaining a product to a friend.

**Pushback triggers:**
- Answer contains "platform", "solution", "enable", "empower", "leverage" → pushback: "That sounds like a press release. What would you say if your mom asked?"
- Answer is >25 words → pushback: "Shorter. One sentence."
- Answer is a feature list → pushback: "Not features. The job it does for someone."

**Accept when:** the answer names a specific user + a specific outcome. Example accept: *"It tells Lithuanian property buyers what's wrong with a parcel before they sign."*

---

### Q2 — Three names (audience specificity)

> "Name THREE specific people (real or composite) who would buy this in the next 30 days. For each: what's their job? what triggered them to start looking? what did they do BEFORE finding you?"

**Why this works:** "everyone" can't survive this question. Composites are fine; vague archetypes ("SMB owners", "millennials") are not.

**Pushback triggers:**
- Answer names a category, not a person → pushback: "Categories don't buy. Name one specific person."
- "Everyone" / "anyone who…" → pushback: "If it's for everyone, it's for no one. Pick the three who'd buy in the next 30 days."
- Person named without a trigger or before-state → pushback: "What did they do yesterday that made them open your site today?"

**Accept when:** each of three names has (a) a job, (b) a trigger, (c) a before-state.

---

### Q3 — The unfair advantage (differentiation)

> "If a buyer had to pick between you and the closest competitor, why would they pick you? Don't list features. Tell me the ONE thing the competitor can't do or won't do."

**Why this works:** features are commodities. Real differentiation is structural — something the competitor can't replicate without burning their own business.

**Pushback triggers:**
- "We're cheaper/faster/better" → pushback: "That's a feature, not an unfair advantage. What's structural?"
- "We have more data / better AI / cleaner UI" → pushback: "They'd say the same. What's the thing they STRUCTURALLY can't say?"
- "Nothing yet" → pushback: "Then what's the bet you're making? What WILL be unfair once you ship X?"

**Accept when:** the answer names a structural moat (regulatory access, exclusive partnership, founder background, network effect) OR honestly says "no moat yet, betting on speed + brand".

---

### Q4 — The last feature (value pillar)

> "If you had to remove every feature except ONE, which would you keep? Why is that the last one?"

**Why this works:** reveals the actual value pillar. Founders often think their product is feature X; the answer is usually a different feature Y.

**Pushback triggers:**
- "I can't pick one, they all matter" → pushback: "Pick the one. Even if it's painful."
- Picks a generic infrastructure piece (auth, payments) → pushback: "Those aren't the product. What does the user actually pay for?"

**Accept when:** the answer is a specific user-facing capability tied to the JTBD from Q1.

---

### Q5 — The honesty test (what NOT to claim)

> "What does your product NOT do well today, that you'd never put on the landing page? Who's a bad fit for it right now?"

**Why this works:** flushes out the dishonest claims a marketing site is tempted to make. Also surfaces the audience exclusions — who should NOT buy this today.

**Pushback triggers:**
- "Nothing comes to mind" → pushback: "Every product has gaps. What did a customer last complain about?"
- "Just speed/scale issues" → pushback: "Operational, not strategic. What CAPABILITY is missing?"

**Accept when:** the answer names ≥1 specific capability gap AND ≥1 audience-fit exclusion. Document both in the positioning brief under "NOT shipped" and "Banned framing for audience X".

---

### Q6 — The proof test (trust posture)

> "What's the most credible piece of proof you have RIGHT NOW that buying this isn't a mistake? Real customer name, real number, real partner. Not aspirational — what's signed and real today?"

**Why this works:** sets the floor for the trust-objection-auditor. If the answer is "we have nothing yet", the audit will block any testimonial-anchored copy.

**Pushback triggers:**
- "We have lots of interest" / "lots of conversations" → pushback: "Interest isn't proof. Name something signed or live."
- Generic numbers without source → pushback: "Where does that number come from? A measurement or an estimate?"

**Accept when:** the answer names specifics (real names, real numbers with their measurement source, real partners with permission) OR honestly says "no real proof yet, treat all segments as lead-capture-only".

---

### Q7 — The conversion test (CTA + delivery realism)

> "If a visitor takes ONE action on your site, what is it? And what happens 60 seconds after they click? Are you ready to deliver that today?"

**Why this works:** forces alignment between the marketing site's CTA and what the product actually delivers next. A common gap: site says "Get instant access", product takes 24 hours.

**Pushback triggers:**
- "Get started" / "Learn more" → pushback: "Those aren't actions. What does the user actually do?"
- The 60-second after-state is aspirational ("we'll have onboarding by Q3") → pushback: "Today. What ACTUALLY happens after they click today?"

**Accept when:** the answer is a specific verb + object + a realistic after-state that matches shipped product.

---

## Four context questions

These are bounded — use `AskUserQuestion` for each.

### C1 — Language + region

```
Question: "What language and primary market does this serve?"
Options:
- Lithuanian (LT)
- English (multi-region)
- English (US-only)
- Other
```

### C2 — Pricing posture

```
Question: "What's the current pricing posture?"
Options:
- B2C with public prices
- B2B with public prices
- B2B "Susisiekime" / contact-sales only
- Freemium / free tier + paid
- Pre-revenue, no pricing yet
```

### C3 — Advisory stance

```
Question: "Should the site take a position ('recommended for X') or stay interpretive ('here are the facts, you decide')?"
Options:
- Recommendatory (we advise)
- Interpretive (we present, user decides)
- Mixed (interpretive on the product, recommendatory on the value)
```

### C4 — Honesty default

```
Question: "Default honesty stance for marketing copy?"
Options:
- Honest-now (only ship-able capabilities; no aspirational claims) — Recommended
- Full-vision (market the roadmap; user accepts regulatory exposure)
- Hybrid (full vision but every claim cites a real source)
```

---

## Pushback rules

1. **Push back exactly TWICE per question.** First pushback is gentle ("tell me more / be specific"). Second pushback names the specific problem ("'platform' is a category, not a product description"). After the second pushback, accept whatever answer comes + flag as `needs-interview` in the brief.

2. **Never push back on context questions** (C1-C4). They have bounded answers; pick or pass.

3. **Acknowledge sharp answers explicitly.** "That's specific — going to use it verbatim" beats silent acceptance.

4. **Pre-fill from the repo, but always verify.** Pre-filled answers are a question, not a fact. Phrase as "I see X in the repo — is that what you actually market as?"

5. **Never combine questions.** "What's your audience AND their pain?" is a form, not an interview. One question, one beat.

6. **Capture verbatim when the answer is sharp.** Direct quotes anchor the positioning brief. Paraphrase only when the answer is too long.

---

## Output integration

After all questions answered, the command writes `.pmstack/positioning.md` with the standard structure. The mapping:

| Question | Brief section |
|---|---|
| Q1 (party test) | North-star + tagline anchor |
| Q2 (three names) | Audiences (one section per name, becomes seed for `/pm:audience`) |
| Q3 (unfair advantage) | Differentiation / competitive landscape |
| Q4 (last feature) | Value pillars (anchor pillar = the kept feature) |
| Q5 (honesty test) | NOT-shipped section + banned framing per audience |
| Q6 (proof test) | Proof available today + audit floor |
| Q7 (conversion test) | Primary CTA + delivery realism |
| C1 | Geography + language |
| C2 | Pricing direction |
| C3 | Advisory stance + banned-verb defaults |
| C4 | Honesty stance |

Where a question was flagged `needs-interview` in the conversation, the corresponding section gets a `**[needs-interview]**` marker with a one-line description of what's still unknown.

---

## Interview length expectations

- Greenfield: 15-25 minutes for the seven forcing questions + four context questions.
- Augment: 5-10 minutes for the specific gaps in an existing brief.
- Anything > 35 minutes signals the conversation drifted into product roadmap territory — pull back, surface the drift, and complete the remaining positioning questions.
