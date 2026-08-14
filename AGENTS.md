# AGENTS.md — Strict Editing & AI Credits Guardrail

## 🚨 CRITICAL DIRECTIVE: ZERO UNAPPROVED AI CREDIT SPEND

### 1. Hard Prohibition on `prompt_project_agent`
- **DO NOT CALL `prompt_project_agent` (Underlord AI)** under any circumstances unless the user explicitly types the exact words: *"use prompt_project_agent"* or *"use Descript AI agent"*.
- `prompt_project_agent` consumes paid Descript AI credits. The user wants **manual, deterministic, and resource-controlled editing**.
- Treat `prompt_project_agent` as **BLOCKED by default**.

---

## 🛠️ Allowed Deterministic MCP Tools

The agent is ONLY permitted to use the following deterministic, non-credit-consuming Descript MCP tools:

1. `import_media` — Ingest raw media files or URLs and create project compositions.
2. `get_project` & `list_projects` — Inspect project assets, duration, compositions, and existing publish links.
3. `export_transcript` — Pull transcripts (SRT, VTT, Markdown, TXT) with timestamps for analysis.
4. `export_timeline` — Export timelines (FCPXML, Premiere XML, DaVinci Resolve XML, EDL, AAF).
5. `publish_project` — Render and publish existing compositions (Video / Audio).
6. `list_folders` & `get_drive_info` — Browse folder structure and workspace info.
7. `wait_for_job` / `list_jobs` / `cancel_job` — Monitor asynchronous deterministic jobs (e.g. import, export, publish).

---

## 📋 Manual & Deterministic Editing Workflow

Instead of delegating edits to black-box AI tools, follow this manual, transparent pipeline:

### Step 1: Ingest & Pull Transcript
- Call `import_media` to upload the raw video into Descript.
- Call `export_transcript` with format `markdown` or `srt` to retrieve the exact word-level timecodes.

### Step 2: Deterministic Transcript & Cut Analysis
- Manually parse the transcript text:
  - Identify silent gaps (time gaps between words).
  - Identify duplicate words and stuttered phrases (*"I think I think"*).
  - Identify candidate editorial cuts (tangents, false starts, retakes).
- Draft the **Review Board** in `staging/reviews/<project_name>_REVIEW.md` using [RESOURCE_STAGING_TEMPLATE.md](file:///Users/apple/.gemini/antigravity-ide/scratch/descript-workspace/RESOURCE_STAGING_TEMPLATE.md).

### Step 3: Resource Staging
- Curate assets in `staging/`:
  - Visual B-roll, diagrams, and illustrations in `staging/broll_and_visuals/`.
  - Audio tracks, whooshes, and SFX in `staging/audio_sfx_music/`.
  - Custom graphic plates generated via local/built-in tools.

### Step 4: User Approval & Execution
- Present the review board to the user with exact timestamps and cut decisions.
- Wait for user approval before making permanent modifications or triggering renders.
- Deliver final output via `publish_project` or `export_timeline` (Premiere / DaVinci XML).
