# Case Study: Motion Ads Content System

*Turning static product photos into 9 video variations automatically*

---

## The Client

**Industry:** Subscription Box / E-commerce

**Team size:** Small marketing team (5-10 people)

**Their situation:** A subscription box company creating monthly motion ads for social media. Each product needed multiple video variations for A/B testing across platforms.

---

## The Challenge

Creating motion ads manually was eating up the marketing team's time. For every product, they needed to create multiple video variations: someone holding the product, unboxing shots, camera movements, process videos, reaction shots, and product-focused clips.

**Pain points:**
- 2-3 hours of manual work per product, per variation
- 50+ products per month meant hundreds of hours on video creation
- Inconsistent quality when rushing to meet deadlines
- Creative team stuck doing repetitive work instead of strategy

**What they tried before:**
- **Manual video editing:** Too slow, couldn't scale
- **Generic templates:** Didn't match their brand aesthetic
- **Freelancers:** Expensive and inconsistent quality

---

## The Solution

A batch processing system that generates all nine motion variations from a single product image. The user fills in one row in Google Sheets with the product image, sets `motion_type` to "all", and the system spawns nine parallel AI video generation jobs — each writing to its own dedicated output column.

**System architecture:**

```
Google Sheets (motion_type = "all")
    ↓
Check Motion Type
    ├─→ "all" → Create 9 Motion Items
    └─→ single → Use specified type
           ↓
Detect Batch vs Single
    ├─→ Batch (9 items) → Route Batch by Model
    │                         ├─→ Batch VEO3 Generator
    │                         └─→ Batch Kling Generator
    └─→ Single → Route by Model
           ↓
Merge Results → Write to Dedicated Columns → Cloud Backup
```

**The 9 motion types:**

| Motion Type | Output Column | Best For |
|-------------|---------------|----------|
| `person_holding` | person_holding_output | Product showcase with human element |
| `pov_unboxing` | pov_unboxing_output | First-person unboxing experience |
| `camera_zoom` | camera_zoom_output | Cinematic product focus |
| `hands_crafting` | hands_crafting_output | DIY/maker aesthetic |
| `reaction_discovery` | reaction_discovery_output | Authentic discovery moment |
| `person_using` | person_using_output | Product in action |
| `person_facing_unboxing` | person_facing_unboxing_output | Traditional unboxing angle |
| `dolly_pan` | dolly_pan_output | Professional camera movement |
| `flipping_instructions` | flipping_instructions_output | How-to/tutorial style |

Plus `custom` for user-defined prompts when none of the presets fit.

**Key components:**
- **Motion Type Router:** Detects "all" mode and splits into 9 items, or processes single type
- **Batch Generator:** Submits all jobs to the API at once, then polls in parallel
- **Dynamic Column Writer:** Each motion type writes to its own dedicated column
- **Model Routing:** VEO3 for human movement, Kling for product shots

**Technologies used:**
- N8N (workflow automation)
- Google Sheets (user interface)
- VEO 3 Fast / Kling v2.5 Turbo (AI video generation)
- Cloud storage (video backup)

---

## The Implementation

**Phase 1: Single Generation** *(Week 1)*
Built the core video generation sub-workflows. One image in, one video out. Established the polling pattern, error handling, and result extraction.

**Phase 2: Motion Templates** *(Week 2)*
Created prompt templates for each motion type. Each template maintains the product appearance while adding motion-specific instructions.

**Phase 3: Batch Processing** *(Week 3)*
Built the "all" mode that creates 9 items from one input row. Implemented parallel batch submission with Code nodes that handle API calls efficiently.

**Challenges overcome:**
- **Dynamic column writing:** Each motion type needed to write to its own column. Solved with a Code node that dynamically builds the column name from the motion type.
- **Batch efficiency:** Instead of 9 sequential workflows, built batch generators that submit all jobs first, then poll in parallel — cutting total time significantly.

---

## The Results

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Time per product | 2-3 hours | 10 minutes (review only) | 90%+ time saved |
| Variations per product | 1-2 manual | 9 automatic | 4-9x output |
| Cost per video | $15-25 (freelancer) | $2-3 (API costs) | 85% cost reduction |

**Qualitative wins:**
- One row = 9 variations in dedicated columns
- A/B test different motion styles instantly
- Consistent quality across all variations
- Creative team freed up for strategy

---

## Key Takeaways

1. **Batch submission beats sequential:** Submit all jobs first, then poll in parallel. Much faster than waiting for each to complete.

2. **Dedicated columns > merged results:** Each motion type has its own output column. Makes review and selection much easier than scrolling through merged data.

3. **Model routing matters:** VEO3 handles human movement and talking better; Kling handles product shots and object animation better. Intelligent routing improves results.

---

## Want Something Similar?

If your team is manually creating content that could be automated, let's talk.

- 🌐 Website: [copyweb.io](https://copyweb.io)
- 📧 Email: [liam@copyweb.io](mailto:liam@copyweb.io)

---

*December 2024 · Built by Copyweb*
