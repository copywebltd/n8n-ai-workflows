# Case Study: AI Content Repurposing Engine

*Turn competitor inspiration into original content in 60 seconds*

---

## The Client

**Company:** Nomad Gear Co.

**Industry:** Outdoor/Travel E-commerce

**Team size:** 5-person marketing team + founder

**Their situation:** Wanted to post daily short-form video but couldn't generate enough original ideas. Competitors were posting daily TikToks and Reels while they struggled to produce 2-3 videos per week.

---

## The Challenge

The founder would save viral videos for "inspiration" but the team never had time to reverse-engineer what made them work. Ideation and scripting took too long, and by the time they created something, the trend had moved on.

**Pain points:**
- Script ideation taking 45+ minutes per video
- Only analyzing 3 inspiration videos per month
- Falling behind competitors posting daily
- No systematic way to study what made viral content work
- Team stuck in reactive mode, always chasing trends

**What they tried before:**
- **Manual analysis:** Too slow, couldn't keep up with volume
- **Generic templates:** Didn't capture their brand voice
- **Freelance writers:** Expensive and inconsistent turnaround

---

## The Solution

A Telegram-based content engine that lets the founder analyze inspiration videos and generate scripts from anywhere — phone, desktop, or tablet. Send a URL, get usable content back in under 60 seconds.

**Two workflows deployed:**

### 1. YouTube Short → Script

Send a competitor or inspiration video URL via Telegram. Gemini 3 Pro analyzes the video content and rewrites it as a script in the brand's voice.

```
Telegram (send YT URL)
    ↓
Gemini 3 Pro (video analysis)
    ↓
Script Generation (brand voice applied)
    ↓
Telegram (returns script)
```

**Brand voice training:** Rugged, practical, slightly irreverent tone. The AI was prompted to write like someone who actually uses outdoor gear, not someone selling it.

### 2. TikTok → Sora Vid

For "remix" content — AI analyzes viral video formats and generates a completely new video variation. Perfect for trending formats where the structure matters more than the specific content.

```
Telegram (send TikTok URL)
    ↓
Gemini 3 Pro (analyze format, extract what makes it work)
    ↓
Prompt Engineering (swap subject, keep structure)
    ↓
Sora 2 (generate new video)
    ↓
Multi-platform posting (Instagram, YouTube, TikTok)
```

**The "Animal Swap" technique:** When remixing viral animal videos, the AI keeps the exact camera angle, lighting, and action — but swaps the animal for something unexpected. A Golden Retriever becomes a Highland Cow. The format stays viral, but the content is original.

### 3. YouTube Long → Social Posts

Bonus workflow: Send a long-form YouTube video, get back a LinkedIn post and Twitter thread summarizing the key takeaways.

```
Telegram (send YT URL)
    ↓
Gemini 3 Pro (extract 3 main takeaways)
    ↓
Platform-specific formatting
    ↓
Auto-post to LinkedIn and Twitter
```

**Technologies used:**
- N8N (workflow automation)
- Telegram Bot (input interface)
- Gemini 3 Pro (video analysis and content generation)
- Sora 2 (AI video generation)
- Blotato (multi-platform social posting)
- Kie.ai (API aggregator)

---

## The Implementation

**Phase 1: Script Generator** *(Week 1)*
Built the YouTube Short → Script workflow. Focused on getting the brand voice right through detailed prompt engineering. Tested with 20+ videos until output quality was consistent.

**Phase 2: Video Remixer** *(Week 2)*
Added the TikTok → Sora pipeline. The tricky part was getting Gemini to extract the *structure* of what made a video work, not just describe what happened.

**Phase 3: Social Repurposing** *(Week 3)*
Added the long-form YouTube → social posts workflow. Different prompt engineering for LinkedIn (professional, 3 takeaways) vs Twitter (punchy, single insight).

**Key prompt engineering decisions:**

- **Alex Hormozi style for scripts:** Short punchy sentences, Grade 6 English, negative hooks, gym analogies
- **No fluff policy:** Prompts explicitly ban words like "delve," "unlock," "game-changer," and 50+ other AI-sounding terms
- **Platform-aware formatting:** LinkedIn gets bullet points and spacing; Twitter gets under 200 characters

---

## The Results

| Metric | Before | After |
|--------|--------|-------|
| Videos posted per week | 2-3 | 6-7 |
| Script ideation time | 45 min | 8 min (review + tweaks) |
| Inspiration videos analyzed | 3/month | 25/month |
| AI-generated remix videos | 0 | 8/month |
| Usable scripts on first pass | N/A | 65% |

**Qualitative wins:**
- Founder can analyze videos from anywhere (phone, coffee shop, airport)
- Team went from chasing trends to catching them
- Consistent brand voice across all content
- Ideas never get lost — every saved video becomes a potential script

**Founder quote:** 
> "I see a video I like, send the link from my phone, and have a script before I finish my coffee. We went from chasing trends to actually catching them."

---

## Key Technical Details

**Telegram as the interface:**

Why Telegram instead of a web app or Google Sheets? Because the founder lives on their phone. Inspiration strikes while scrolling TikTok at 11pm — the workflow needs to meet them where they are.

**Gemini video analysis:**

Gemini 3 Pro can analyze video content directly from a URL. No need to download, transcribe, or process — just send the link and ask questions about what's in the video.

**Brand voice prompt structure:**

```
# PERSONALITY
[Description of how the brand sounds]

# WRITING STYLE
[Specific rules: sentence length, vocabulary level, forbidden words]

# OUTPUT FORMAT
[Exactly what to return, nothing else]
```

**The "forbidden words" list:**

The prompts explicitly ban 50+ words that make AI content sound generic: "delve," "embark," "game-changer," "unlock," "revolutionize," etc. This single addition dramatically improved output quality.

---

## Key Takeaways

1. **Meet users where they are:** The founder scrolls TikTok on their phone. The workflow input is Telegram on their phone. Zero friction means actual adoption.

2. **Brand voice is trainable:** With detailed prompt engineering, AI can learn to write in a specific voice. The key is examples, explicit rules, and a list of what *not* to say.

3. **Structure > Content for viral formats:** When remixing viral videos, keep the structure (camera angle, pacing, hook) and swap the content. The format is what makes it work.

4. **65% first-pass accuracy is transformative:** Even if 35% of scripts need heavy editing, the team is starting from something instead of a blank page. That's the difference between 2 videos/week and 7.

---

## Want Something Similar?

If your team is drowning in content demands and swimming in unused inspiration, let's talk.

- 🌐 Website: [copyweb.io](https://copyweb.io)
- 📧 Email: [liam@copyweb.io](mailto:liam@copyweb.io)

---

*December 2024 · Built by Copyweb*
