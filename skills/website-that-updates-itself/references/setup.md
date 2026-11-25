# Self-updating website: setup reference

Load this when you are actually building the pipeline. Facts, menu paths and prices were checked against the vendors' own docs on 2026-11-25. Anything older than about 90 days: re-check the linked source before relying on it, and say so if you couldn't.

## 1. Should you do this at all? (and how to stay on Google's good side)

**Goal:** Decide whether a voice-to-blog pipeline fits your business, and set the one rule that keeps it safe: every post is a draft until a human approves it.

**Time:** about 15 minutes. **Needs:** Google Search Central docs, A notepad

**Steps (the path that works):**

1. List 10 questions customers actually ask you on calls, in DMs or at the counter. If you can't get to 10, stop here. You don't have enough to say yet, and the system will produce filler.
2. Check your raw material. Do you record at least one 5+ minute voice note or video a week where you explain something to a customer? That's the fuel. Without it, this becomes an AI article generator, which is the thing Google warns about.
3. Read Google's 'Using generative AI content' page and the 'Scaled content abuse' section of the spam policies (links in Sources). The short version: AI help is fine. Mass-producing pages that add nothing for readers is not, however they were made.
4. Write your house rules on one line and stick them where you work: 'One idea from me per post. Nothing publishes without my read-through. Max [2] posts a week.'
5. Pick your site platform. WordPress and Webflow can take drafts from an automation today with a simple key. Shopify can too, but since January 2026 you need a developer for a one-time setup (see Lesson 4). Squarespace and Wix are outside this course.
6. Decide what 'success' means in 90 days, for example 'impressions for my 10 customer questions are growing in Search Console.' Leave out 'traffic doubles'. You can't control that number.

**Done when:** You have a list of 10 real customer questions, a written approval rule, a weekly post cap, and you know which platform you're on.

**Watch out:** When NOT to do this: you sell in a regulated field (medical, legal, financial advice) and can't commit to a careful expert review of every draft; you have nothing to say beyond what competitors already wrote; or you want 50 location pages by Friday. Google's own self-assessment asks whether you're 'using extensive automation to produce content on many topics'. If the honest answer is yes, don't build this.

## 2. Get a transcript you can actually use

**Goal:** Turn one video or voice memo into clean text, free, in under 10 minutes.

**Time:** about 20 minutes. **Needs:** YouTube (Show transcript), Your phone's voice recorder or transcription app, Google Docs or any text editor

**Steps (the path that works):**

1. From YouTube (your own video): open the video on a computer, expand the description, and click 'Show transcript'. The transcript opens next to the video.
2. Select the transcript text, copy it, and paste it into a new doc. If timestamps come along with it, that's fine. Claude can ignore them in Lesson 3.
3. From a voice memo: use your phone's built-in transcription if it has one (recent iPhones show a transcript inside Voice Memos). Otherwise use any transcription app. Copy the text into the same doc.
4. Spend 3 minutes fixing the words machines get wrong: your business name, product names, street and suburb names, prices. Auto-captions often mangle exactly these words.
5. At the top of the doc, add one line of context: who the post is for, the question it answers, and the page on your site it should point to (for example 'For: homeowners asking how long a bathroom reno takes. Link to: /services/bathrooms').
6. Save the doc in one folder called 'Raw transcripts'. In Lesson 4 the automation will watch this folder (or a form) for new ones.

**Done when:** You have one transcript doc with names and prices corrected and a context line at the top.

**Watch out:** Verified 2026-11-25: YouTube's help page gives the desktop path ('In the video description, click Show transcript'). It doesn't document a mobile path or a caption-file download from YouTube Studio, so we don't give one. Apple documents a 'View a transcription' feature in Voice Memos, but we couldn't confirm which iOS versions and languages support it. Check on your own phone. Transcripts only exist where captions exist. Very short videos or music-heavy audio may have none.

## 3. Claude turns your words into a structured post

**Goal:** Get a draft with a title, meta description, H2 sections, FAQ and internal links that still sounds like you, with no keyword stuffing.

**Time:** about 25 minutes. **Needs:** Claude (claude.ai, Free or Pro), Your transcript doc, A list of 5-10 key pages on your site

**Steps (the path that works):**

1. Write a 'site map cheat sheet' once: 5-10 of your most important URLs with one line each (for example '/services/bathrooms: our bathroom renovation service'). Claude can only link to pages you give it.
2. Open Claude, start a new chat, and paste the prompt below. Fill in the [brackets], then paste the transcript at the end.
3. Read the 'Facts to check' list Claude returns first. Check every item. If something is wrong, tell Claude and ask it to fix the draft.
4. Read the draft out loud. If a sentence doesn't sound like something you'd say to a customer, ask Claude to rewrite it in the transcript's words.
5. Once you're happy, save the prompt as a Project instruction in Claude (or keep it in a doc). Lesson 4 reuses the exact same prompt inside the automation.
6. Do this by hand for your first 3 posts before automating. You'll learn what you always change, and you can add that to the prompt.

**Prompt: Transcript to SEO draft (paste into Claude)**

```
You are editing a blog post for [Business name], a [what you do] in [city/region]. The author is [your name], the owner. Turn the transcript below into one blog post draft.

RULES
- Use only facts, stories, numbers and opinions that appear in the transcript. Do not invent statistics, prices, customer stories or credentials. If something important is missing, list it under 'Questions for the owner' instead of filling the gap.
- Keep the owner's voice: plain words, short sentences, first person ('we', 'I'). Keep 1-2 memorable phrases from the transcript word for word.
- Write for a reader asking: [the customer question this post answers]. Answer it in the first 2-3 sentences.
- Use the main phrase [main search phrase, e.g. 'how long does a bathroom renovation take'] naturally in the title and once in the opening. Do not repeat it unnaturally or stuff variations. Never write for search engines over people.
- 600-1,200 words, or shorter if the transcript doesn't support more. Don't pad.

OUTPUT, in this order, using these exact headings:
1. Facts to check: bullet list of every claim, number, price or name the owner should verify.
2. Questions for the owner: anything missing that would make the post more useful (max 3).
3. Title: under 60 characters, specific, no clickbait.
4. Slug: lowercase-with-hyphens.
5. Meta description: 140-155 characters, says what the reader gets.
6. Body: in HTML using <h2>, <p>, <ul>, <li> only. 3-5 H2 sections that follow the order of the transcript.
7. FAQ: 3 short questions and answers, taken only from the transcript, as <h2>FAQ</h2> followed by <h3> questions and <p> answers.
8. Internal links: 2-3 links woven into the body, chosen ONLY from this list, with natural anchor text (not 'click here'):
[paste your site map cheat sheet]
9. Call to action: one closing sentence pointing to [your main offer page].

TRANSCRIPT
[paste transcript here]
```

**Done when:** You have one draft where every fact is verified, at least one phrase is yours word for word, and every link points to a real page on your site.

**Watch out:** On FAQs: Google says it stopped showing FAQ rich results in Search from May 7, 2026. Keep a short FAQ because it helps readers skim. Don't expect the FAQ to win extra space in Google results, and don't add FAQ markup for that reason. Google also says AI-written titles, meta descriptions and alt text need the same human review as the body.

## 4. Wire it up: transcript in, draft on your site out

**Goal:** Build a small n8n workflow that sends each new transcript to Claude and creates a DRAFT post on WordPress or Webflow. Nothing goes live without you.

**Time:** about 60 minutes. **Needs:** n8n (Cloud or self-hosted), Anthropic API key, WordPress Application Password or Webflow site API token

**Steps (the path that works):**

1. Get your site key. WordPress: log in to wp-admin, go to Users -> Profile, scroll to 'Application Passwords', type a name like 'n8n drafts', generate it, and copy it right away (WordPress won't show it again). Your site must be on HTTPS. Webflow: open site settings (gear icon) -> Apps & integrations -> scroll to 'API access' -> Generate API token. Name it, tick only the CMS read and write scopes, generate, and copy.
2. In n8n, create a new workflow. Add a trigger that fits how you work: a Form Trigger where you paste the transcript, or a trigger that watches your 'Raw transcripts' Google Drive folder.
3. Add a Claude step. Use n8n's Anthropic node if your n8n has one, or an HTTP Request node that calls the Anthropic Messages API with your API key. Paste your Lesson 3 prompt and map the transcript into the [paste transcript here] spot. Ask Claude to return JSON with title, slug, meta_description, body_html and facts_to_check.
4. WordPress: add the WordPress node, create a credential (your username + the Application Password + site URL), choose Post -> Create, and map title, content and slug. Set status to 'draft'. If the node doesn't show a status option, use an HTTP Request node instead: POST to https://[yoursite]/wp-json/wp/v2/posts with Basic Auth and the field status = draft.
5. Webflow: add an HTTP Request node. POST to https://api.webflow.com/v2/collections/[collection_id]/items/insert, header 'Authorization: Bearer [token]', body {"items":[{"isDraft":true,"fieldData":{"name":"...","slug":"...","post-body":"..."}}]}. Field names must match your Blog collection's field slugs (check them in the Webflow CMS collection settings).
6. Add a final step that emails or messages you the 'Facts to check' list and a link to the draft. Run the workflow once with a real transcript, open your CMS, and confirm the post is sitting in Drafts, not live.
7. Turn the workflow on. Your weekly job is now to review the draft, check the facts, and click Publish yourself.

**Done when:** A test transcript produced a post that you can see in WordPress 'Drafts' or as a Webflow draft item, and the live site did not change.

**Watch out:** Verified 2026-11-25. WordPress REST API post status accepts publish, future, draft, pending, private. Application Passwords have been in core since WordPress 5.6. Webflow: items created via the API are drafts by default (isDraft: true), each site can have up to 5 tokens, and tokens expire after 365 days of inactivity. We could not confirm on n8n's docs whether the WordPress node exposes a Status field or whether the Webflow node uses API v2, which is why we give the HTTP Request fallback. Shopify: since January 1, 2026, new custom apps can't be created in the Shopify admin. You build one in the Dev Dashboard, and the client-credentials tokens expire every 24 hours, so a developer should set this up once. Then use the Admin GraphQL 'articleCreate' mutation with isPublished: false (needs the write_content or write_online_store_pages scope). Shopify's page doesn't explicitly say isPublished:false creates a draft, so test it on a hidden blog first. Never put API keys in a shared doc.

## 5. Measure what's working and run it weekly

**Goal:** Use Google Search Console to see whether your posts are being found, and lock in a 30-minute weekly routine.

**Time:** about 30 minutes. **Needs:** Google Search Console, Your CMS, A calendar

**Steps (the path that works):**

1. If you haven't already, add your site to Google Search Console and verify it (follow Google's on-screen options).
2. After you publish a post, paste its full URL into the inspection bar at the top of Search Console, then click 'Request indexing'. Google limits how many requests you can make per day, and a request doesn't guarantee indexing. For many pages, rely on your sitemap.
3. Every week, open Performance (Search results), set the date range to the last 3 months, click the 'Pages' tab, and click a post's URL. Then switch to the 'Queries' tab to see which searches it shows up for.
4. Look at impressions first. Clicks come later. A new post from a small site may show few or zero impressions for weeks. That's normal. The newest days are preliminary and can change.
5. If a post gets impressions for a question it doesn't answer well, record a 3-minute voice note answering that exact question and run it through the pipeline as an update to the same post. Don't start a new post.
6. Lock the routine into your calendar (illustrative): Monday, record 1 voice note (10 min). Wednesday, review the draft and check facts (15 min). Wednesday, publish and request indexing (2 min). Friday, look at Search Console (5 min).

**Done when:** You can open Search Console, filter to one of your posts, and name the top 3 queries it appears for, or confirm it's too early to have data.

**Watch out:** Realistic costs, checked 2026-11-25 (approximate, prices change). Claude: Free plan $0, or Pro $20/month billed monthly ($17/month billed annually). If n8n calls the API, Sonnet 5.5 is listed at $2 input / $10 output per million tokens. Illustrative calculation: a 4,000-token transcript plus a 2,000-token draft is about $0.03 per post. n8n Cloud Starter: $20/month billed annually (€20 in Europe) (2,500 executions), or self-host the Community edition on your own server. Webflow: CMS API access is included on the free Starter plan (50 CMS items) and Premium ($25/month billed yearly, 20,000 items). The Basic plan has no CMS. WordPress: no extra cost beyond your hosting. Search Console: free. Illustrative total for a WordPress owner: about $20-45/month. Ranking results are not guaranteed, and Google does not tell you how long they take.

## Sources

- [Google Search Central: Using generative AI content (updated 2026-10-01)](https://developers.google.com/search/docs/fundamentals/using-gen-ai-content)
- [Google Search Central: Spam policies, scaled content abuse (updated 2026-11-23)](https://developers.google.com/search/docs/essentials/spam-policies)
- [Google Search Central: Creating helpful, reliable, people-first content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)
- [Google Search Central: FAQPage structured data (FAQ rich results deprecated May 2026)](https://developers.google.com/search/docs/appearance/structured-data/faqpage)
- [Search Console Help: Performance report](https://support.google.com/webmasters/answer/7576553)
- [Search Console Help: URL Inspection tool](https://support.google.com/webmasters/answer/9012289)
- [YouTube Help: View video transcripts](https://support.google.com/youtube/answer/15930243?hl=en)
- [WordPress REST API: Posts reference](https://developer.wordpress.org/rest-api/reference/posts/)
- [WordPress.org: Application Passwords](https://developer.wordpress.org/advanced-administration/security/application-passwords/)
- [Webflow Data API v2: Create items](https://developers.webflow.com/data/reference/cms/collection-items/staged-items/create-items)
- [Webflow: Site tokens](https://developers.webflow.com/data/reference/site-token)
- [Shopify changelog: Legacy custom apps can't be created after January 1, 2026](https://shopify.dev/changelog/posts/legacy-custom-apps-can-t-be-created-after-january-1-2026.md)
- [Shopify Admin GraphQL: articleCreate](https://shopify.dev/docs/api/admin-graphql/latest/mutations/articleCreate)
- [n8n: WordPress node docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.wordpress/)
- [n8n pricing](https://n8n.io/pricing/)
