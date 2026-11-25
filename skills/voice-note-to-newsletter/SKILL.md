---
name: voice-note-to-newsletter
description: Builds or runs a pipeline where a founder records a 2 to 5 minute voice memo and gets back a newsletter in their own voice, laid out in their template and saved as a draft broadcast in Resend for one-tap approval. Use to set up the pipeline for a client, to write this week's edition from a voice note, or to decide whether the pipeline is worth it.
when_to_use: voice note to newsletter, turn this voice memo into a newsletter, write this week's newsletter from my recording, newsletter from voice, set up the newsletter pipeline, resend newsletter, record and send newsletter
argument-hint: "[voice memo or transcript | 'set up' | 'is this worth it']"
metadata:
  humanai:
    version: 0.1.0
    reads: [business, voice-profile, learnings]
    writes: [learnings]
---

# Voice Note to Newsletter

Most founders know what to say and hate writing it down. This pipeline lets them talk for three minutes and approve a finished email. Done means a draft broadcast in Resend that the owner would send with at most small edits, and nothing sent without their tap.

Human + AI Module 1. The free course with every step is at humanai.news/learn/voice-note-to-newsletter. Full setup facts, prompts and sources: `references/setup.md` (dated; load it when building).

## Modes

| Signal | Mode |
|---|---|
| "is this worth it", no list yet, unsure | **Decide** |
| "set up", "build the pipeline", a new client | **Build** (load `references/setup.md`) |
| A memo, a transcript, "this week's edition" | **Write one edition** |

## Decide first

Worth it when: the founder has opinions and expertise, talks easily, and has (or wants) a list they'd email at least twice a month.

Not worth it, and say so, when:
- They have no list and no way to grow one yet. Build the list first (a lead magnet, a signup on the site).
- They're on Klaviyo for Shopify revenue attribution, predictive segments or SMS. Connect AI to Klaviyo instead of migrating.
- Their CRM and email live together in one tool the sales team depends on. Splitting them costs more in glue than it saves.
- They won't record. A pipeline with no input is just a monthly bill.

## Write one edition

1. **Read `voice-profile.md` first.** No profile: run brand-voice on the memo itself plus anything they've written, and say the profile is provisional.
2. **Find the one idea.** A three-minute memo usually holds one strong idea and two tangents. Lead with the strong one. Keep a tangent only if it earns its own short section.
3. **Keep their words.** Lift their best phrasings verbatim. Tidy grammar, never flatten it. If a sentence sounds like them, it stays even if it's imperfect.
4. **Structure:** subject line (under 50 characters, specific, no clickbait), a one-line preview, the opening in their voice, the idea, one practical takeaway, one call to action that matches the business (reply, book, read, buy), sign-off from the profile.
5. **Flag, don't invent.** Any figure, name, date or claim you can't trace to the memo gets `[CHECK: ...]`. The owner resolves it during approval.
6. **Output** the edition as clean HTML for the template plus the plain-text version, and a three-line note: the idea you led with, what you cut, any [CHECK] items.

## Build the pipeline (defaults)

Capture (phone memo into a watched folder) → transcribe → Claude rewrites with the voice profile into structured JSON (subject, preview, body) → render into the template → create a **draft** broadcast in Resend → send the owner an approve link → send only on approval.

Hard rules for the build:
- The send step is gated on an explicit approval. No timer-based sends, ever.
- The client's own Resend, n8n and AI accounts, on their billing.
- Unsubscribe link in every broadcast, and existing unsubscribes migrated before the first send.
- Verified sending domain (a subdomain like news.theirdomain.com protects their main inbox reputation).

## Run it weekly

Record Monday, approve Tuesday, send Tuesday or Wednesday morning in the list's time zone. Watch three numbers monthly: open rate trend (not absolute), replies, unsubscribes per send. When the owner edits the same kind of thing twice, add it to `voice-profile.md` and log it in `learnings.md`.
