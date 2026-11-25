---
name: website-that-updates-itself
description: Turns a founder's voice notes or videos into SEO blog posts and page updates that land on their site as drafts for approval, via WordPress, Webflow, Shopify or a Git-based site. Use to write a post from a transcript, to set up the auto-draft pipeline for a client, or to check a draft against Google's guidance on AI content.
when_to_use: turn this video into a blog post, turn this voice note into a post, blog post from transcript, website that updates itself, auto publish blog, wordpress drafts from voice notes, webflow cms automation, seo post from youtube video, is AI content ok for SEO
argument-hint: "[transcript | video url | 'set up' + CMS | 'check' + draft]"
metadata:
  humanai:
    version: 0.1.0
    reads: [business, voice-profile, learnings]
    writes: [learnings]
---

# Website That Updates Itself

One real idea, in the founder's own words, published as a well-structured page each week. That compounds. A hundred thin AI pages a month gets a site demoted. Done means a draft on their site (never a live publish) that a reader would find genuinely useful and that the owner would put their name on.

Human + AI Module 2. Free course: humanai.news/learn/website-that-updates-itself. Setup facts, prompts and sources: `references/setup.md` (dated; load it when building).

## The line Google draws

Google doesn't penalise AI-assisted writing. It penalises pages made mainly to rank instead of to help, and "scaled content abuse": many pages generated without adding value. Keep every post on the right side:
- One post per real idea the founder actually has. Never generate posts from a keyword list alone.
- Their experience, examples and opinions in every post. That is the value a generic page can't copy.
- A named author, and the date.
- If you can't say what a reader learns here that they couldn't get from the top three results, don't publish it.

## Write one post

1. **Clean the transcript.** Remove filler, keep their phrasing. Note the one question the piece answers.
2. **Title:** the question or promise in plain words, under ~60 characters. **Meta description:** one sentence, ~150 characters, says what the reader gets.
3. **Structure:** a direct answer in the first two sentences, then H2 sections that each answer one sub-question, then a short "what to do next".
4. **Internal links:** two or three to their own service pages or related posts, with descriptive anchor text.
5. **FAQ section:** optional, for readers only. Google stopped showing FAQ rich results in 2026, so don't expect extra space in results from it.
6. **Flag, don't invent.** Unsourced numbers and claims become `[CHECK: ...]`.
7. Check against `voice-profile.md` before handing over.

## Build the pipeline (defaults)

Transcript in (YouTube captions or voice memo) → Claude structures the post as JSON (title, meta, slug, body HTML, internal links) → n8n creates a **draft** in the CMS → owner reviews and publishes.

- WordPress: an Application Password for a dedicated user with Author role, never the owner's admin login.
- Webflow: a site token scoped to CMS; items created as drafts.
- Shopify: needs a one-time developer setup for a custom app. Flag it in the plan.
- Git sites (Next.js, Astro): commit to a branch and open a pull request; the preview deploy is the draft.

Say when not to: if the site has no traffic and no service pages yet, fix the service pages first. A blog can't rescue a site that doesn't say what the business does.

## Measure

Search Console, monthly: impressions and clicks per post, the queries each post shows for, and posts with impressions but no clicks (rewrite the title and meta). Log what worked in `learnings.md`.
