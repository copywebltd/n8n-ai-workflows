# Supported AI Models

Quick reference for the AI models integrated into these workflow systems.

---

## Video Generation Models

### VEO 3 / VEO 3.1 (Google DeepMind)

**Best for:** Talking heads, human movement, keyframe animation

**Capabilities:**
- Text-to-video generation
- Image-to-video (start frame)
- Keyframe animation (start + end frames)
- Style reference

**Aspect ratios:** 16:9, 9:16, 1:1

**Typical generation time:** 30-90 seconds

---

### Sora 2 / Sora 2 Pro (OpenAI)

**Best for:** Cinematic motion, smooth camera work

**Capabilities:**
- Text-to-video generation
- Image-to-video

**Aspect ratios:** 16:9, 9:16, 1:1

**Typical generation time:** 60-120 seconds

**Note:** Does not support photorealistic human faces in uploaded images.

---

### Kling v2.5 Turbo (Kuaishou)

**Best for:** Product shots, object animation, commercial content

**Capabilities:**
- Text-to-video generation
- Image-to-video
- 5 or 10 second outputs

**Aspect ratios:** 16:9, 9:16, 1:1

**Typical generation time:** 60-180 seconds

---

### Wan 2.5 (Alibaba)

**Best for:** General purpose, cost-effective generation

**Capabilities:**
- Text-to-video generation
- Image-to-video
- 1080p resolution

**Aspect ratios:** 16:9, 9:16, 1:1

**Typical generation time:** 90-180 seconds

---

## Image Generation Models

### Seedream V4 (ByteDance)

**Best for:** High-quality image generation, image editing

**Capabilities:**
- Text-to-image generation
- Image editing with multiple reference images
- 4K resolution output

**Aspect ratios:** 16:9, 9:16, 1:1, 4:3, 3:4, 3:2, 2:3, 21:9

**Typical generation time:** 30-60 seconds

---

### Nanobanana / Nanobanana Pro (Google)

**Best for:** Image enhancement, multi-image compositing

**Capabilities:**
- Image enhancement
- Style transfer
- Multiple image inputs (up to 3-4 images)

**Aspect ratios:** 16:9, 9:16, 1:1

**Typical generation time:** 20-40 seconds

---

## Model Selection Guide

| Use Case | Recommended Model |
|----------|-------------------|
| Person talking to camera | VEO 3.1 |
| Product showcase | Kling v2.5 |
| Cinematic/artistic | Sora 2 Pro |
| Cost-sensitive projects | Wan 2.5 |
| Image enhancement | Nanobanana Pro |
| Image generation | Seedream V4 |
| Keyframe animation | VEO 3.1 |

---

## API Provider

All models are accessed through **Kie.ai** as the API aggregator. This provides:

- Unified authentication
- Consistent response formats
- Simplified billing
- Model availability monitoring

---

*Last updated: December 2024*
