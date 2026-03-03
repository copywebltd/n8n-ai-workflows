# n8n AI Workflows

> Production-ready n8n workflows for AI video and image generation. VEO 3, Sora 2, Kling, Seedream, NanoBanana. Built by Copyweb.io

---

## What's Inside

A collection of battle-tested n8n workflows powering AI content generation across multiple providers. These workflows handle image generation, video generation, content repurposing, and multi-platform distribution.

### Case Studies

| System | Description |
|--------|-------------|
| AI Content Pipeline | Google Sheets to image preview to human approval to video generation |
| Content Repurposing Engine | Telegram-based pipeline turning existing content into new formats |
| Motion Ads System | Single product image to 9 motion video variations |

### Supported Models

**Video Generation:**
- VEO 3 / VEO 3.1 (Google DeepMind) : talking heads, human movement, keyframe animation
- Sora 2 / Sora 2 Pro (OpenAI) : cinematic motion, smooth camera work
- Kling 2.5 / 3.0 (Kuaishou) : product motion, lip sync
- Wan 2.5 (Alibaba) : fast generation, good for drafts

**Image Generation:**
- Seedream v4 (ByteDance) : photorealistic product shots
- NanoBanana / NanoBanana Pro : multi-image compositing, enhancement
- Imagen 3 (Google) : high quality, free tier

## How to Use

1. Download the `.json` workflow file
2. In n8n: **Workflows** > **Import from File**
3. Select the downloaded file
4. Update credentials (they are not included for security)

## Architecture Pattern

All workflows follow the same pattern:

```
Trigger (webhook/schedule)
  → AI Provider API call
  → Poll for completion
  → Process result
  → Deliver (Airtable / Google Sheets / Telegram / email)
```

Human review gates are built into every production workflow. Nothing auto-publishes without approval.

---

*Built by Copyweb — architecting how marketing teams operate in an AI-first world.*
