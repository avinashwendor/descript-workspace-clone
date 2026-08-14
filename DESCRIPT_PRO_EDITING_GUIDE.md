# Descript Pro Video Editing Guide & Token-Efficient Pipeline

This document defines the complete technical architecture and execution playbook for professional video editing using the **Descript MCP Server**, local deterministic utilities (`ffmpeg`, Python), and internal asset generators.

---

## 1. Executive Summary & Capabilities

### Can Antigravity Edit Raw Video to a Professional Finish?
**Yes.** Antigravity can take raw, unedited footage (talking head, screen recording, podcast, vlog, tutorial) and produce a polished, broadcast-grade video with:

- **Rough Cut & Flow:** Intelligent jump-cuts, false start removal, filler word elimination (`um`, `uh`, `you know`), and silence shortening.
- **Studio Audio Mastering:** Background noise removal, acoustic echo cancellation, voice EQ/leveling via **Descript Studio Sound**, auto-ducked background music, and synchronized sound effects (whooshes, pops, impacts).
- **Visual Pacing & Framing:** Automated scene detection, dynamic zoom punch-ins (1.15x - 1.25x on key emphasis points), aspect ratio formatting (16:9 for YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for LinkedIn/Instagram).
- **Kinetic Text & Motion Captions:** Animated word-by-word highlighted captions, speaker tags, custom fonts/colors/strokes, and lower-third title cards.
- **B-Roll & Visual Assets:** Insertion of native stock footage/GIFs/illustrations and custom asset creation via internal image generation.
- **Multi-Format Distribution:** Direct cloud publishing (MP4/MP3) with instant share/download URLs or timeline export (Premiere XML, DaVinci Resolve XML, FCPXML, EDL) for manual mastering.

---

## 2. Descript MCP Tool Reference

| MCP Tool | Purpose | Best Practices |
| :--- | :--- | :--- |
| `import_media` | Ingest local files or cloud URLs (Google Drive, Dropbox, direct link). Creates project and timeline. | Always include `add_compositions: true` when starting a new edit so media automatically populates the canvas. |
| `prompt_project_agent` | AI Project Agent (Underlord) to edit compositions via natural language instructions. | **Batch all editing instructions into one prompt** to conserve AI credits and tokens. |
| `publish_project` | Renders and publishes the composition to cloud video/audio formats. | Always display the returned `project_url` and final `download_url` / `share_url`. |
| `export_timeline` | Exports timeline files (EDL, AAF, FCPXML, Premiere XML, DaVinci Resolve XML). | Use when passing the edit to a secondary DAW or color grading suite. |
| `export_transcript` | Exports time-coded transcripts (SRT, VTT, Markdown, HTML, RTF, TXT). | Ideal for SEO, blog generation, or external closed captioning. |
| `get_project` / `list_projects` | Inspect project details, existing compositions, assets, and share links. | Check before creating duplicates or republishing existing renders. |
| `wait_for_job` / `list_jobs` | Polls background processing jobs with progress updates. | Displays real-time progress (`progress.label`) while rendering or importing. |

---

## 3. Token & Resource Optimization Strategy

To avoid burning unnecessary AI tokens, Descript AI credits, and monthly Media Minutes, follow this efficiency hierarchy:

```
[ Raw Video File ]
       │
       ▼
[ Local Pre-processing (ffmpeg) ] ──► (Trim dead lead-in/lead-out, compress if needed) ──► Saves Media Minutes
       │
       ▼
[ Descript Ingest (import_media) ] ──► Auto-transcribe + Canvas creation
       │
       ▼
[ Single Consolidated Underlord Batch ] ──► (Studio Sound + Filler Words + Scene Cuts + Captions + SFX) ──► 1 Single Job
       │
       ▼
[ Native Stock / Internal Assets ] ──► (Built-in stock media + Native Image Generator) ──► No 3rd-party API spend
       │
       ▼
[ Export / Publish (publish_project) ] ──► Instant High-Res Master
```

### Key Optimization Rules

1. **Pre-Trim Locally with `ffmpeg` Before Uploading:**
   - Eliminate dead time before the speaker starts or after they finish.
   - Example command:
     ```bash
     ffmpeg -ss 00:00:15 -to 00:12:45 -i raw_recording.mov -c copy trimmed_input.mp4
     ```
   - *Benefit:* Reduces uploaded file size and avoids consuming Descript Media Minutes on unusable dead air.

2. **Single-Pass Consolidated Underlord Prompting:**
   - **NEVER** run 5 separate `prompt_project_agent` calls for:
     1. Remove filler words
     2. Apply studio sound
     3. Add captions
     4. Cut silences
     5. Add scenes
   - **ALWAYS** combine them into a single, comprehensive batch prompt:
     ```text
     "Perform a full professional edit on this composition:
     1. Audio: Apply Studio Sound (intensity 80%) and remove all filler words and silences over 0.75s.
     2. Pacing: Split into scenes based on speaker topic changes and apply 1.15x punch-in zooms on key statements.
     3. Captions: Add dynamic kinetic captions styled with bold white text, yellow active word highlight, and dark stroke.
     4. B-roll: Add appropriate stock video b-roll overlays during abstract conceptual explanations.
     5. Music: Add subtle low-volume background ambient corporate track with auto-ducking under dialogue."
     ```

3. **Asset Generation Hierarchy:**
   - **Stock Visuals/Audio:** Use Descript's native stock library (included in plan).
   - **Custom Plates/Thumbnails:** Use the agent's built-in `generate_image` tool.
   - **No External Paid GenAI APIs:** Keep all asset generation inside the native toolset.

---

## 4. End-to-End Professional Editing Workflow

### Phase 1: Ingestion & Timeline Initialization
1. Inspect file metadata locally using `ffprobe`:
   ```bash
   ffprobe -v error -show_entries format=duration,size:stream=width,height,codec_name -of json raw_video.mp4
   ```
2. Request upload URL or cloud import via `import_media`:
   ```json
   {
     "project_name": "Pro_Edit_Episode_01",
     "files": [
       {
         "file_name": "raw_video.mp4",
         "file_size": 254819200,
         "content_type": "video/mp4"
       }
     ],
     "add_compositions": true
   }
   ```
3. Upload binary chunks directly to the returned `upload_url` and track completion with `wait_for_job`.

### Phase 2: Professional Multi-Pass AI Polish
Execute the consolidated prompt targeting the generated composition:
- **Aspect Ratio Format:** 16:9 (Landscape standard) or 9:16 (Vertical shorts).
- **Sound Design:** Studio Sound active + ducked background music + transitional SFX.
- **Visuals:** Auto-scene splits + kinetic captions + stock overlays.

### Phase 3: Review & Custom Touches
- Fetch project summary via `get_project`.
- Verify scene markers, transcript accuracy, and visual alignment.
- (Optional) Render custom graphics with `generate_image` and overlay if specialized charts/diagrams are needed.

### Phase 4: Publishing & Export
- Trigger high-bitrate render via `publish_project`:
  ```json
  {
    "project_id": "<PROJECT_UUID>",
    "composition_id": "<COMPOSITION_UUID>",
    "format": "video"
  }
  ```
- Receive shareable Descript link and direct high-speed CDN download URL.

---

## 5. Summary of Supported Editing Features

| Feature Category | Capabilities Supported |
| :--- | :--- |
| **Voice & Speech** | Studio Sound (AI noise removal/room reverb fix), Filler word cleanup, Silence shortening, Speaker identification/diarization, Voice leveling. |
| **Pacing & Cuts** | Script-based cuts, jump cuts, scene generation, multi-camera switching, ripple edits. |
| **Motion Graphics & Text** | Kinetic word-highlight captions, animated lower thirds, chapter title cards, text overlays. |
| **Sound Design** | Background music tracks, automatic speech ducking, transitional SFX (whoosh, pop, click, riser). |
| **Visual Framing** | Zoom punch-ins (camera emphasis), canvas resizing (16:9, 9:16, 1:1, 4:5), B-roll overlays, picture-in-picture. |
| **Export Formats** | MP4 Video (1080p, 4K), MP3/WAV Audio, SRT/VTT Captions, FCPXML, Premiere XML, DaVinci Resolve XML, EDL. |
