---
description: Refine the ICP brief for a specific audience segment using the Audience Researcher subagent.
argument-hint: "<segment-name> (e.g. buyers, brokers, developers)"
allowed-tools: Read, Glob, Grep, Write, Task
---

# /pm:audience

You are dispatching the Audience Researcher subagent for the segment named in `$ARGUMENTS`.

## Procedure

1. **Verify ingest has been run**. Read `.pmstack/positioning.md`. If it doesn't exist, tell the user to run `/pm:ingest` first and stop.

2. **Locate the segment**. Check `.pmstack/icp/{segment}.md`. If the file doesn't exist but the segment appears in `.pmstack/positioning.md`, scaffold it. If the segment isn't in the positioning brief at all, ask the user to confirm before proceeding.

3. **Dispatch the Audience Researcher subagent** (Task tool, `subagent_type: audience-researcher`) with this brief:

   ```
   Refine the ICP for segment "{segment}" using the existing positioning brief at .pmstack/positioning.md and the scaffold at .pmstack/icp/{segment}.md.

   You may also read the source MDs cited in positioning.md.

   Output to .pmstack/icp/{segment}.md, replacing the scaffold. Required sections:
   - Demographic + firmographic snapshot
   - Job-to-be-done (one sentence)
   - Top 3 functional needs (what they need to accomplish)
   - Top 3 emotional needs (how they need to feel)
   - Top 5 objections + how to disarm each (only if evidence supports the disarmer — otherwise "needs interview")
   - Concrete proof available today (real testimonials, real numbers, real partners — or "none yet")
   - Primary CTA + secondary CTA for this segment
   - Banned framing for this segment (specific tone/voice constraints; if pro audience, no anxiety-bait)
   - Open research questions

   Hard rules:
   - Do not invent demographics, testimonials, or pain points. Cite source MDs for every claim.
   - If the segment has no real proof in the repo, the primary CTA must be lead-capture ("Susisiekime", "Pakalbėkime", "Schedule a call"), NOT a purchase CTA.
   - Keep the file under 600 words.
   ```

4. **Report a one-paragraph summary** to the user when the subagent returns: what's locked in, what still needs interview validation, and one suggested next command.
