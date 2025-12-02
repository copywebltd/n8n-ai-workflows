# Case Study: AI Content Pipeline

*A multi-model video generation system with human approval checkpoints*

---

## The Client

**Industry:** Marketing Agency / Internal Tool

**Team size:** Marketing team managing multiple client campaigns

**Their situation:** Needed a reliable system to generate AI videos at scale while maintaining quality control. Different content types required different AI models, and there was no room for wasted API credits on bad outputs.

---

## The Challenge

AI video generation is powerful but unpredictable. Without oversight, you end up with:
- Wasted credits on videos that don't match the brief
- Inconsistent quality across campaigns
- No way to preview results before committing to expensive video generation
- Manual copy-pasting between different AI tools

**Pain points:**
- Each AI model has different strengths — no single model works for everything
- Video generation costs $2-5 per attempt — mistakes add up fast
- No preview system meant generating videos blind
- Tracking what's done vs. pending was a spreadsheet nightmare

**What they tried before:**
- **Direct API calls:** Too technical, no oversight
- **Individual AI platforms:** Switching between tools constantly
- **Manual tracking:** Lost track of what was processed

---

## The Solution

A two-phase content pipeline controlled entirely from Google Sheets. Phase 1 generates an AI-enhanced preview image for human approval. Only approved images proceed to Phase 2: video generation. Every step is tracked, and results are written back to the sheet automatically.

**System architecture:**

```
PHASE 1: IMAGE PREVIEW
┌─────────────────────────────────────────────────┐
│  Google Sheets (production_status = "pending")  │
│              ↓                                  │
│  Image Preview Orchestrator                     │
│  ├─→ Direct (use original image)               │
│  ├─→ Seedream V4 (AI generation/editing)       │
│  ├─→ Nanobanana (enhancement)                  │
│  └─→ Nanobanana Pro (multi-image compositing)  │
│              ↓                                  │
│  Write preview URL → status = "awaiting_approval" │
└─────────────────────────────────────────────────┘
              ↓
        [HUMAN REVIEWS]
        Sets image_approval = "approve" or "reject"
              ↓
PHASE 2: VIDEO GENERATION
┌─────────────────────────────────────────────────┐
│  Google Sheets (image_approval = "approve")     │
│              ↓                                  │
│  Video Generation Orchestrator                  │
│  ├─→ VEO 3 (talking heads, keyframes)          │
│  ├─→ Sora 2 Pro (cinematic motion)             │
│  ├─→ Kling v2.5 Turbo (product shots)          │
│  └─→ Wan 2.5 (general purpose)                 │
│              ↓                                  │
│  Write video URL → status = "done" → Cloud Backup │
└─────────────────────────────────────────────────┘
```

**The human checkpoint:**

This is the key innovation. Between image preview and video generation, a human reviews the AI-generated image and either approves or rejects it. This simple gate prevents expensive video generation on images that aren't right.

**Model selection guide:**

| Use Case | Image Model | Video Model |
|----------|-------------|-------------|
| Product on plain background | Nanobanana Pro | Kling v2.5 |
| Person with product | Seedream V4 | VEO 3 |
| Style transfer | Nanobanana | Sora 2 Pro |
| Use original image | Direct | Any |
| Keyframe animation | Direct | VEO 3 |

**Status tracking:**

| Status | Meaning |
|--------|---------|
| `pending` | Ready for image preview |
| `processing` | Currently generating |
| `awaiting_approval` | Preview ready for human review |
| `approved` | Ready for video generation |
| `done` | Video complete |
| `error` | Something failed (check error_message) |

**Technologies used:**
- N8N (workflow automation)
- Google Sheets (user interface + database)
- Kie.ai (API aggregator for all AI models)
- Cloudinary / Google Drive (video backup)

---

## The Implementation

**Phase 1: Sub-workflow Architecture** *(Week 1)*
Built individual sub-workflows for each AI model. Each follows the same pattern: receive input → call API → poll for completion → extract result → return. This modularity means adding a new model takes hours, not days.

**Phase 2: Orchestration Layer** *(Week 2)*
Built the main orchestrators that read from Google Sheets, route to the correct sub-workflow based on model selection, and write results back. Added status tracking so nothing gets lost.

**Phase 3: Human Approval Flow** *(Week 3)*
Implemented the checkpoint between image and video. The system pauses after image generation, waits for human approval in the sheet, then a separate trigger picks up approved rows for video generation.

**Phase 4: Error Handling & Backup** *(Week 4)*
Added comprehensive error capture — every failure writes the error message back to the sheet. Added automatic cloud backup for all generated videos (AI hosting URLs expire).

**Challenges overcome:**

- **Different API response formats:** VEO returns results directly; Kling/Sora require JSON.parse(). Built model-specific extraction logic in each sub-workflow.

- **Polling reliability:** AI generation takes 30-180 seconds. Built a Wait → Poll → Check loop that retries until success or failure.

- **Keyframe support:** VEO can use start/end frame images for animation. Added dynamic detection of `use_keyframes` flag and multi-image handling.

---

## The Results

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Wasted API credits | ~30% of generations | <5% | 85% reduction in waste |
| Time to generate content | 2-3 hours (manual) | 15-20 min (automated) | 90% time saved |
| Models available | 1-2 (switching tools) | 8 (one interface) | 4x capability |
| Error visibility | None (silent failures) | 100% (logged to sheet) | Complete visibility |

**Qualitative wins:**
- One interface for all AI models
- Human approval prevents expensive mistakes
- Full audit trail in Google Sheets
- Non-technical team members can use it

---

## Key Technical Details

**Sub-workflow pattern (every model follows this):**

```
Start → Build Request → POST to API → Wait → 
Poll Status → Check Result → 
  [Success] → Extract URL → Return
  [In Progress] → Wait Again (loop)
  [Error] → Capture Message → Return Error
```

**Model-specific extraction:**

```javascript
// VEO (direct response)
video_result = $json.data.response.resultUrls[0]

// Kling, Sora, Nanobanana (nested JSON string)
video_result = JSON.parse($json.data.resultJson).resultUrls[0]
```

**Error handling (captures all possible error locations):**

```javascript
error_message = $json.data.errorMessage || 
                $json.data.failMsg ||
                $json.errorMessage || 
                $json.error || 
                'Unknown error'
```

---

## Key Takeaways

1. **Human checkpoints save money:** A 10-second review of a preview image prevents a $3-5 wasted video generation. At scale, this adds up to thousands in savings.

2. **Modularity enables flexibility:** Each AI model is its own sub-workflow. Adding a new model doesn't touch existing code. Removing a deprecated model is just disconnecting one path.

3. **Google Sheets is underrated:** For teams that already live in spreadsheets, making automation that reads/writes to Sheets means zero learning curve. They fill in columns, magic happens.

4. **Status tracking is non-negotiable:** Without explicit status columns, you lose track of what's processing, what's waiting, and what's done. Build it in from day one.

---

## Want Something Similar?

If your team needs AI content generation with quality control, let's talk.

- 🌐 Website: [copyweb.io](https://copyweb.io)
- 📧 Email: [liam@copyweb.io](mailto:liam@copyweb.io)

---

*December 2024 · Built by Copyweb*
