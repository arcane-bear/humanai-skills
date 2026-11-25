---
name: discovery-prep
description: Reads a small business from its website, Google profile and reviews before a discovery call, writes the brand files the other skills use, and after the call turns the notes into a 2 to 3 build plan with fixed price bands. Use before a free consult, after a discovery call, or when onboarding a new client.
when_to_use: prep for a discovery call, prep this client, research this business before the call, onboard a new client, new client, write the plan after the call, turn my call notes into a proposal, what should we build for them, 48 hour plan, proposal deck
argument-hint: "[business name + url | 'after call' + notes | 'new client <url>']"
metadata:
  humanai:
    version: 0.1.0
    reads: [business, voice-profile, competitors, learnings]
    writes: [business, competitors, plan]
---

# Discovery Prep

The free 20-minute call is diagnostic only. This skill makes sure you walk in already knowing the business, and walk out with a plan you can send inside 48 hours. Done means: a one-page brief before the call, and after it a plan with 2 to 3 builds, each scoped, timed and priced, that the owner can say yes to without another meeting.

Adapted from Boring Marketing's `start-here`, `competitive-intel` and `first-screen-check` (MIT). See THIRD_PARTY_NOTICES.md.

## Modes

| Signal | Mode |
|---|---|
| A business name or URL, a booking notification, "prep" | **Before the call** |
| Call notes, a transcript, "after the call", "write the plan" | **After the call** |
| "new client <url>" | Before the call, saved under `./clients/<slug>/` |

## Before the call (about 10 minutes of agent time)

Read, don't interview. The owner already answered four questions on the intake form (tools, bottleneck, content target, budget). Start from those; never ask them again.

1. **The business in one paragraph.** From the site's home, services and about pages: what they sell, to whom, where, and how a customer contacts them. Note who the founder is and whether the founder is the voice of the brand (they usually are in businesses under $5M).
2. **The phone test.** Open their main page at phone width. On the first screen, can a customer see what they do, where, and how to call or book? Note the one thing that would cost them customers. This is a conversation opener, not the pitch.
3. **What customers say.** Read the newest 10 to 20 Google reviews. Pull 3 verbatim phrases that show what customers value, and any repeated complaint (slow replies, hard to book, no follow-up). Repeated complaints about response time point straight at Module 4.
4. **Two or three true peers.** The businesses that show up first for their main service. One line each on what they do better or worse. No aspirational giants.
5. **Map the intake answers to modules.** Use the table below. Mark one as the likely first build, and say why in one sentence.

| What you see | Likely module |
|---|---|
| Founder has expertise but posts rarely; no newsletter or a dead one | 1. Voice note to newsletter |
| Thin or stale site; blog last updated a year ago; no service pages | 2. Website that updates itself |
| Founder is good on camera or has a story; content target is high | 3. AI video pipeline |
| Inbox, leads, quotes or SOP questions eat the week; slow-reply reviews | 4. Custom ops agents |
| Wants all of 1 to 3 and has budget at or above the bundle | Full content engine |

Write `business.md` and `competitors.md`, then a brief for the person running the call:

```
CALL BRIEF: <business>, <date>
Who: <founder>, <role>. Voice of the brand: yes/no.
They said (intake): bottleneck "<their words>", target <x>, budget <tier>
What I saw: <phone test finding> · <review pattern, with one quote>
Likely first build: <module> because <one reason>
Three questions to ask: <open questions, how/what, no yes/no>
Do not: design the solution live, quote a price on the call
```

Hard rule for the brief: every claim points to something you saw, with the URL. If a page wouldn't load, say "not checked", never guess.

## After the call

Load the notes or transcript. Summarise the owner's situation in their own words first, in three lines, and check it against `business.md`. Where the call contradicts the pre-read, the call wins.

Then write `plan.md` as the content for a short deck (6 to 8 slides):

1. **Where you are now.** Their workflow today, in their words, with the hours it costs (their estimate, labelled as theirs).
2. **What changes.** The same workflow automated. A simple before/after diagram description.
3. **The builds.** 2 to 3 modules, each with: what they get, what it connects to, timeline (usually 2 to 4 weeks), fixed price within the published band, and what would push it to the top of the band.
4. **What it costs to run.** Software runs on their own accounts with no markup. Give rough monthly tool costs, sourced or labelled approximate.
5. **Care plan.** The monthly option and what it includes.
6. **Next step.** 50% to start, 50% at launch. One question to close.

Pricing defaults (Human + AI published bands; check `references/pricing.md` for the current figures before quoting):
- Pick a single number inside the band, never a range, in the plan.
- Precise beats round: $3,250 reads as calculated; $3,000 reads as a guess.
- If they named a budget tier below the first build, say so plainly and offer the smallest useful build or the free course for that module. Never shrink scope silently to fit the money.

## Say when not to build

If the bottleneck is better solved by a setting in a tool they already pay for, or by a freelancer for a one-off script, the plan says so. Losing a small deal honestly is how the next big one finds you.
