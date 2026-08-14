# descript-workspace-clone

This workspace is pre-configured with the **Descript MCP Server**, **AI Video Production Pipeline**, and **Staging Architecture** for Google Antigravity.

---

## 📁 Repository Structure

```text
descript-workspace-clone/
├── .agents/
│   ├── mcp_config.json                 # Direct MCP server configuration
│   └── plugins/
│       └── descript/
│           ├── plugin.json             # Descript plugin manifest
│           ├── mcp_config.json         # Plugin-scoped MCP server config
│           └── skills/
│               └── descript-workflows/
│                   └── SKILL.md        # Skill definition
├── staging/
│   ├── raw/                            # Raw video footage & links
│   ├── broll_and_visuals/              # Stock clips, visual plates, diagrams
│   ├── audio_sfx_music/                # Auto-ducked tracks, whooshes, SFX
│   ├── storyboards/                    # Scene-by-scene script breakdowns
│   └── reviews/                        # Review briefs & cut approvals
├── FUTURISTIC_PRODUCTION_STANDARD.md   # 6-Layer visual/sound design architecture
├── VIDEO_PRODUCTION_PIPELINE.md        # 5-Stage production standard
├── RESOURCE_STAGING_TEMPLATE.md        # Staging & cut approval template
├── ADVANCED_DESCRIPT_CAPABILITIES.md   # Eye Contact, Background Removal, Overdub
├── DESCRIPT_PRO_EDITING_GUIDE.md       # Token-efficient editing reference
└── README.md                           # Overview
```

---

## 🚀 How to Use

1. **Activate Workspace**: Open `/Users/apple/.gemini/antigravity-ide/scratch/descript-workspace` in Antigravity IDE.
2. **Authenticate with Descript**: Complete the Descript OAuth authorization when prompted.
3. **Workflow**:
   - Provide a raw video link/file $\rightarrow$ Ingest to Descript for transcription.
   - Antigravity builds the **Storyboard + Resource Plan + Editorial Cuts Table** in `staging/reviews/`.
   - Review and approve the plan.
   - Descript executes the single-pass master edit and delivers a 4K render / timeline export.
