# Human + AI Skills: house conventions

Every skill in this pack follows these rules. Read them once before editing or adding a skill.

## 1. What a skill is

A skill is a floor, not a ceiling. It carries the judgment a senior operator would bring (when to do this, when not to, what good looks like), and leaves the obvious steps to the model. If the situation in front of you argues for a better path, take it and say why in one line. Deviating silently is the only wrong way to deviate.

Hard rules are few and are the same across the pack:

1. **Never send, publish or post on the owner's behalf without an explicit yes.** Drafts are the default output of every skill.
2. **No invented numbers.** A figure is either sourced (with a link and a date) or labelled illustrative.
3. **Say when to stay put.** If the business is better off on its current tool, or doing nothing, the skill says so. Honesty is the product.
4. **The owner's accounts, the owner's bills.** Skills set things up inside accounts the client owns. Never route a client's data or billing through ours.

## 2. Voice

Operator-first, plain English, short sentences. Numbers with sources. No hype words ("revolutionary", "game-changing", "unlock"). No fake logos, testimonials or client counts. Lowercase is fine for display headings; body copy is sentence case.

## 3. Where state lives

- One business: `./brand/` in the working folder.
- An agency or studio running several clients: `./clients/<slug>/`, with `./clients/active` naming the current one.

Files skills read and write (all Markdown, all optional):

| File | Owner skill | What it holds |
|---|---|---|
| `business.md` | discovery-prep | What they sell, to whom, where, tools they pay for, the one bottleneck |
| `voice-profile.md` | brand-voice | How the business sounds, with evidence |
| `competitors.md` | discovery-prep | The 2 to 3 true peers, and what their customers complain about |
| `plan.md` | discovery-prep | The 2 to 3 builds recommended, each with scope and a price band |
| `learnings.md` | any | Dated lines: what worked, what didn't, what the owner corrected |

If none exist, a skill proceeds standalone and asks only for what it strictly needs.

## 4. File layout

```
skills/<name>/
  SKILL.md          decision layer, under ~250 lines
  references/       dated knowledge, loaded only when the SKILL.md says so
```

Perishable facts (prices, menu paths, model names) never live in SKILL.md. They live in a dated reference file with sources.

## 5. Credit

Several skills adapt methods from Boring Marketing Skills (MIT, (c) 2026 Boring Marketing, LLC). Their notice is in `THIRD_PARTY_NOTICES.md` and stays with every copy of this pack.
