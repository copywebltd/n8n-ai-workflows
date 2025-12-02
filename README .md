# N8N AI Workflows

Production-ready automation systems for AI-powered video and image generation. Built by [Copyweb](https://copyweb.io).

---

## What This Is

A collection of N8N workflow architectures that connect AI generation models into production-ready content pipelines. These systems turn simple spreadsheet inputs into finished AI videos and images — with human approval checkpoints, error handling, and cloud backup built in.

**This repo documents the systems I've built.** The actual workflow JSON files are not included (this is a portfolio, not a template store). If you want these built for your team, [get in touch](#contact).

---

## Systems Overview

### 🎬 AI Video Generation Engine

A multi-model video generation system controlled entirely from Google Sheets.

**What it does:**
- Takes an approved image + video prompt
- Routes to the right AI model based on your selection
- Polls until complete, handles errors gracefully
- Writes results back to the sheet
- Backs up finished videos to cloud storage

**Models supported:**
- VEO 3 / VEO 3.1 (Google) — with keyframe animation support
- Sora 2 / Sora 2 Pro (OpenAI)
- Kling v2.5 Turbo (Kuaishou)
- Wan 2.5 (Alibaba)

**Architecture:**
```
Google Sheets (control hub)
    ↓
Video Generation Orchestrator
    ├─→ VEO 3 Sub-workflow
    ├─→ Sora 2 Pro Sub-workflow
    ├─→ Kling Sub-workflow
    └─→ Wan 2.5 Sub-workflow
          ↓
    Merge Results → Error Check → Update Sheet → Cloud Backup
```

---

### 🖼️ AI Image Preview System

Generate and approve AI images before committing to video generation. No wasted credits on bad inputs.

**What it does:**
- Takes a reference image + prompt
- Routes to the selected image model
- Generates a preview image
- Waits for human approval
- Only then triggers video generation

**Models supported:**
- Seedream V4 (ByteDance) — text-to-image and image editing
- Nanobanana / Nanobanana Pro (Google) — multi-image compositing
- Direct passthrough (skip enhancement, use original)

**Architecture:**
```
Google Sheets (control hub)
    ↓
Image Preview Orchestrator
    ├─→ Direct (passthrough)
    ├─→ Seedream V4 Sub-workflow
    ├─→ Nanobanana Sub-workflow
    └─→ Nanobanana Pro Sub-workflow
          ↓
    Merge Results → Update Sheet → [Human Approval] → Video Generation
```

---

## Key Features

**🎯 Google Sheets as the Control Hub**
No complex UI needed. Your team works in a spreadsheet they already know. Fill in the columns, the automation handles the rest.

**👁️ Human-in-the-Loop**
AI generates a preview image. A human approves or rejects. Only approved images proceed to video generation. This prevents wasted API credits and ensures quality.

**🔀 Multi-Model Routing**
One system, multiple AI models. Choose VEO for talking heads, Kling for product shots, Sora for cinematic motion. The orchestrator routes to the right sub-workflow automatically.

**📊 Status Tracking**
Every row shows its current state: `pending` → `processing` → `awaiting_approval` → `done` or `error`. Know exactly where every piece of content is in the pipeline.

**🛡️ Error Handling**
When things fail (and they will), errors are captured and written back to the sheet with details. No silent failures. No lost work.

**☁️ Automatic Backup**
Finished videos are automatically uploaded to cloud storage. The temporary AI URLs expire — your backups don't.

---

## How It Works (Conceptual)

### The Two-Phase Content Pipeline

**Phase 1: Image Generation**
1. User fills in a row: reference image, prompt, aspect ratio, image model
2. System marks row as "processing"
3. Orchestrator routes to the correct image sub-workflow
4. Sub-workflow calls the API, polls for completion, extracts result
5. Preview URL is written to the sheet
6. Status changes to "awaiting_approval"
7. Human reviews and sets approval to "approve" or "reject"

**Phase 2: Video Generation**
1. Approved rows are picked up by the video workflow
2. Status changes to "processing"
3. Orchestrator routes to the selected video model
4. Sub-workflow handles API call, polling, result extraction
5. Video URL is written to the sheet
6. Video is downloaded and backed up to cloud storage
7. Status changes to "done"

### Sub-Workflow Pattern

Every AI model follows the same pattern:

```
Trigger → Build Request → POST to API → Wait → Poll Status → 
Check Result → [Success: Extract URL] or [In Progress: Wait Again] or [Error: Capture Message] → Return
```

This consistency means adding a new model is straightforward — copy the pattern, adjust the API details.

---

## Tech Stack

- **N8N** — Workflow automation (self-hosted)
- **Google Sheets** — User interface and data storage
- **Kie.ai** — API aggregator for AI models
- **Cloudinary / Google Drive** — Media backup

---

## Results

These systems have been used to generate hundreds of AI videos for marketing campaigns, with:

- **90%+ success rate** on first-attempt generations
- **Zero lost outputs** thanks to automatic backup
- **Hours saved** per campaign vs. manual generation

---

## Case Studies

### AI Content Pipeline
*A multi-model video generation system with human approval checkpoints*

A two-phase content system where AI generates preview images for human approval before committing to expensive video generation. Supports 4 image models and 4 video models, all controlled from Google Sheets.

**Key features:**
- Human-in-the-loop prevents wasted API credits
- 8 AI models accessible from one interface
- Full status tracking and error logging
- Automatic cloud backup

[Read the full case study →](case-studies/ai-content-pipeline.md)

---

### Motion Ads Content System
*Turning static product photos into 9 video variations automatically*

A subscription box company needed motion ads for social media. Instead of manually creating each variation, we built a system that takes one product image and generates nine different motion styles — all with a single click.

**Key features:**
- "All" mode generates 9 variations from one input
- Each motion type writes to its own column
- Batch processing for efficiency
- VEO3 for human motion, Kling for product shots

[Read the full case study →](case-studies/motion-ads-system.md)

---

## What's NOT Included

This is a portfolio repo, not a template library. You won't find:

- ❌ Importable JSON workflow files
- ❌ API keys or credentials
- ❌ Step-by-step setup guides
- ❌ Copy-paste solutions

**Why?** These systems represent significant R&D investment. The patterns, error handling, and edge case solutions took months to develop. I'm happy to show you what's possible — and build it for you if it fits your needs.

---

## Contact

**Want systems like these built for your team?**

- 🌐 Website: [copyweb.io](https://copyweb.io)
- 📧 Email: [liam@copyweb.io](mailto:liam@copyweb.io)

I work with marketing teams who need AI automation that actually works in production — not demos that break when you look at them wrong.

---

## About Copyweb

We build AI automation for marketing teams. Our specialty is turning cutting-edge AI models into reliable, team-ready systems that non-technical people can actually use.

No prompt engineering courses. No vague "AI strategy" consulting. Just working systems that make your team faster.

---

*Built with N8N, caffeine, and an unreasonable number of API calls.*
