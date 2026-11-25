---
name: brand-voice
description: Builds a voice profile from a founder's real words (voice notes, videos, emails, posts, reviews of them) so every newsletter, post and page sounds like them, not like a model. Use when starting any content build, when drafts sound generic or AI-written, or to check new content for drift.
when_to_use: brand voice, make it sound like me, sounds like AI, sounds generic, voice guide, voice profile, does this sound like us, drift check, write in my voice, founder voice
argument-hint: "[url | pasted content | transcript files | 'drift check' + new content]"
metadata:
  humanai:
    version: 0.1.0
    reads: [business]
    writes: [voice-profile]
---

# Brand Voice

Every Human + AI content build runs through one voice profile. If the profile is vague, every module downstream sounds like a stock template, and the owner stops trusting the system within a month. Done means a profile specific enough that a stranger holding it writes something the owner's customers would believe the owner wrote, and tight enough that every line rules something out.

Adapted from Boring Marketing's `brand-voice` (MIT). See THIRD_PARTY_NOTICES.md.

## Where the evidence comes from

Spoken words beat written ones for founders. Most owners write stiffly and talk well. In order of value:

1. **Voice notes and video transcripts** of the founder talking about their work. Two or three minutes each, three or more of them.
2. **Emails or DMs they wrote to customers** (with names removed).
3. **Their best posts or pages,** the ones they're proud of. Ask which.
4. **How customers describe them** in reviews. This is not their voice; it tells you which qualities the voice has to carry.

If a site exists, read it first and draft the profile before asking anything. Questions only fill gaps the material couldn't answer, usually the hard lines ("never say X").

## The profile

Write `voice-profile.md` with these sections. Every line must be falsifiable: if a competitor could paste it into their own profile unchanged, it is too vague. Rewrite it until it rules something out.

```
VOICE PROFILE: <business>, built <date> from <sources>

In one line: <how they sound, e.g. "a tradesman explaining it over a fence">
Sentence shape: <length, rhythm, how they open, e.g. "starts with the problem, never with 'I'">
Words they use: <8-12 verbatim words or phrases, each with where it came from>
Words they'd never use: <the AI tells and the jargon to ban>
How they handle numbers: <exact, rounded, avoided>
How they say no / disagree: <one quoted example>
How they sign off: <exact>
Hard lines: <topics, claims or tones that are off limits>
Three exhibits: <three short verbatim passages that ARE the voice>
```

## The test loop

Before saving, write one short paragraph on a neutral topic in the profile's voice. Show it next to one exhibit. Ask the owner one question: "Does this sound like you, or like someone doing an impression?" Fix what they point at. One round is usually enough; two at most.

## Banned by default

These read as AI to most readers. Ban them unless the founder genuinely uses them: "delve", "game-changer", "in today's fast-paced world", "unlock", "elevate", "seamless", "it's not just X, it's Y", triple-adjective lists, rhetorical-question openers, and em-dash chains.

## Drift check

Given the saved profile and 3 to 10 new pieces, score each against the profile: what matches, what drifted, and the one line that most breaks voice. Suggest edits, not rewrites. If the owner's voice has genuinely changed, update the profile and note the date; voices evolve and the profile follows them.
