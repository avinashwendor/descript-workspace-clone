---
name: descript-workflows
description: >-
  Orchestrate audio and video editing workflows in Descript using manual and deterministic MCP tools.
  Strictly avoids consuming AI credits unless explicitly instructed by the user.
---

# Descript Workflows Skill (Manual & Deterministic Mode)

This skill guides the agent in using the Descript Model Context Protocol (MCP) server for video production while **strictly avoiding unapproved AI credit consumption**.

## 🚨 Core Guardrail: No Black-Box AI Spend
- **`prompt_project_agent` is BLOCKED by default.** Do NOT invoke it unless the user explicitly requests AI-driven editing.
- Always use direct, deterministic MCP tools: `import_media`, `export_transcript`, `export_timeline`, `publish_project`, `get_project`.

## Allowed Deterministic Workflows

### 1. Ingestion & Composition Setup
- Use `import_media` to upload raw video/audio assets or remote links into Descript.
- Automatically initializes project compositions without spending AI credits.

### 2. Transcript & Cut Analysis
- Use `export_transcript` to extract time-coded transcripts (SRT, Markdown, TXT).
- Parse transcript deterministically to identify:
  - Dead air / silence gaps.
  - Repeated words, stutters, and false starts.
  - Topic beats and candidate editorial cuts.
- Stage all proposed cuts and visual cues in `staging/reviews/<project>_REVIEW.md` for human approval.

### 3. Resource Staging & Finishing
- Stage visual assets, stock clips, and B-roll in `staging/broll_and_visuals/`.
- Stage sound effects and background music in `staging/audio_sfx_music/`.
- Export timeline via `export_timeline` (FCPXML, DaVinci Resolve XML, Premiere XML) or render via `publish_project`.
