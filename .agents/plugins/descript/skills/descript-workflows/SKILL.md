---
name: descript-workflows
description: >-
  Orchestrate audio and video editing workflows in Descript using the Descript MCP server.
  Use when creating projects, importing media, applying Studio Sound, removing filler words,
  generating subtitles/captions, creating highlight clips, or managing Descript compositions.
---

# Descript Workflows Skill

This skill guides the agent in using the Descript Model Context Protocol (MCP) server to automate audio/video production pipelines while optimizing for resource consumption (Media Minutes and AI Credits).

## Core Capabilities

### 1. Media Import & Composition Creation
- Import local audio/video assets or remote URLs directly into a Descript Drive.
- Initialize new compositions with targeted canvas aspect ratios (16:9 landscape, 9:16 vertical reels, 1:1 square).

### 2. Underlord AI Editing
- **Cleanup**: Remove filler words (`um`, `uh`, repeated phrases) and dead air / silences.
- **Audio Enhancement**: Apply **Studio Sound** to eliminate background noise, room reverb, and level voices.
- **Visuals & Layout**: Auto-generate scenes, add dynamic captions, eye-contact correction, and chapter markers.
- **Repurposing**: Generate viral highlight clips, summaries, and social media cutdowns.

### 3. Cost-Optimization Best Practices
- **Media Minutes**: Check duration before uploading duplicate media to avoid wasting monthly media minutes.
- **AI Credits**: Group editing commands into single Underlord requests where possible instead of running repetitive single-action queries.
- **Pre-Validation**: Verify transcript corrections before generating voice clones or AI overdub passes.
