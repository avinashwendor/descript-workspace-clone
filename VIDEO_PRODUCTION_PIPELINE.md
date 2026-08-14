# Professional Video Production Pipeline

This document defines the standard operating procedure for end-to-end video creation. It prioritizes **planning, transcript analysis, resource staging, user review, and zero-friction execution** directly inside Descript without low-level manual CLI tools.

---

## 🎬 The 5-Stage Production Protocol

```
┌─────────────────────────────────────────────────────────────────────────┐
│ Stage 1: Ingest & Transcript Analysis                                   │
│ • Direct upload to Descript (`import_media`) for auto-transcription     │
│ • Detect silent gaps, filler words, duplicate phrases, and stutters     │
│ • Identify low-value tangents and candidate editorial cuts              │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Stage 2: Narrative Pacing & Resource Staging                            │
│ • Structure 5–15s Hook and pattern interrupts every 15–20s              │
│ • Stage Descript native stock (B-roll, ambient tracks, SFX)             │
│ • Generate custom diagrams/visual plates via `generate_image`           │
│ • Escalate if custom 3D/cinematic AI video is required                  │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Stage 3: User Review & Editorial Cut Approval                           │
│ • Present `staging/reviews/<project>_REVIEW.md` review board            │
│ • User reviews and approves:                                            │
│   1. Proposed transcript cuts (tangents, false starts, weak takes)      │
│   2. Gap and duplicate word pruning                                     │
│   3. Scene storyboard, B-roll, music track, and caption design          │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Stage 4: Direct Descript AI Execution                                   │
│ • Single consolidated Underlord batch execution                         │
│ • Applies Studio Sound, Eye Contact, approved cuts, punch-ins,          │
│   kinetic captions, B-roll overlays, and auto-ducked audio              │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Stage 5: Final Master & Delivery                                        │
│ • Cloud render (1080p / 4K MP4) with instant download link              │
│ • Optional NLE Timeline Export (Premiere XML, DaVinci Resolve, FCPXML)  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## ✂️ Stage 1: Transcript Analysis & Cut Detection

Once uploaded to Descript, the transcript is parsed for three categories of cleanup:

1. **Automatic Low-Level Polish:**
   - **Filler Words:** Removes `um`, `uh`, `ah`, `you know`, repeated filler sounds.
   - **Silent Gaps:** Detects awkward dead-air pauses (e.g. pauses > 0.75s) and shortens them to natural breathing room (0.25s).
   - **Stutters & Duplicate Words:** Prunes immediate accidental word repetitions (*"I think I think"* ➔ *"I think"*).

2. **Editorial Cut Proposals (Flagged for User Approval):**
   - **False Starts:** Where the speaker stumbled on the first attempt and restarted the sentence immediately after with a better delivery.
   - **Rambling & Side Tangents:** Digressions that break topic flow and harm viewer retention.
   - **Redundant Explanations:** Where a concept is repeated twice unnecessarily.

---

## 📐 Stage 2: Narrative Pacing & Resource Staging

1. **The 5–15 Second Hook:** Drop the viewer directly into the payoff or curiosity gap.
2. **Variable Pacing (The Heartbeat Method):** Fast 0.5s–1s cuts during high-energy bursts, 3s–5s on core takeaways.
3. **Pattern Interrupts (Every 15–20s):** Zooms (1.15x), visual overlays, sound effects, or kinetic caption bursts.
4. **Staging Hierarchy:**
   - **Descript Native Stock:** Royalty-free B-roll clips, ambient background music, transitional SFX.
   - **Web Search & Public Graphics:** Logos, icons, references.
   - **Internal Image Generator (`generate_image`):** Custom workflow diagrams, infographics, and visual plates.
   - **Escalation Protocol:** Flag to user if specialized AI cinematic footage or 3D renders are needed.

---

## 📋 Stage 3: User Review & Sign-Off

The review brief is generated in `staging/reviews/<project_name>_REVIEW.md` using [RESOURCE_STAGING_TEMPLATE.md](file:///Users/apple/.gemini/antigravity-ide/scratch/descript-workspace/RESOURCE_STAGING_TEMPLATE.md).

The user reviews:
- [x] **Proposed Editorial Cuts Table:** Mark each candidate cut as `[Approve]` or `[Keep]`.
- [x] **Gap & Duplicate Word Pruning:** Confirm timing thresholds.
- [x] **Storyboard & Visuals:** Check planned scene punch-ins, B-roll overlays, and graphic plates.
- [x] **Audio & Music:** Confirm background track vibe and sound effects.

---

## ⚡ Stage 4 & 5: Direct Execution & Cloud Delivery

- **Single-Pass Batch Underlord Execution:** Run consolidated prompt in Descript applying all approved cuts, Studio Sound, Eye Contact, kinetic captions, and sound design.
- **Export:** High-resolution 1080p/4K MP4 cloud render + download links + optional DaVinci/Premiere XML timeline export.
