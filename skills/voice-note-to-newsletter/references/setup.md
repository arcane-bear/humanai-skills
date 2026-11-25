# Voice note to newsletter: setup reference

Load this when you are actually building the pipeline. Facts, menu paths and prices were checked against the vendors' own docs on 2026-11-25. Anything older than about 90 days: re-check the linked source before relying on it, and say so if you couldn't.

## 1. Is this right for you, and what it costs

**Goal:** Decide in ten minutes whether a voice-to-newsletter pipeline is worth building for your business, and what it will cost each month.

**Time:** about 10 minutes. **Needs:** Resend, n8n, OpenAI transcription, Claude

**Steps (the path that works):**

1. Picture the finished system. You talk into your phone for 2–5 minutes. About 5 minutes later an email lands in your inbox with a ready-to-send newsletter and two buttons, Approve and Decline. Approve sends it to your list. Decline leaves it as a draft for you to fix by hand.
2. Check that you have something to say each week. This works when you already have opinions, client stories or lessons in your head. It does not create ideas for you. It only saves you the writing.
3. Check the size of your list and where it lives. Resend's free Marketing plan covers up to 1,000 contacts. Pro Marketing starts at $40/month for 5,000 contacts (resend.com/pricing, checked 2026-11-25). You'll need to export your current list as a CSV, and the people on it must have agreed to hear from you.
4. Add up the running costs (approximate, checked 2026-11-25). Transcription with OpenAI's gpt-transcribe is $0.0045 per minute of audio, so four 4-minute memos come to about 7 cents a month. Claude Sonnet 5.5 is $2 per million input tokens and $10 per million output tokens. A newsletter draft is a few thousand tokens, so expect a few cents per draft. n8n is free if you self-host the Community edition (you pay for a small server). n8n Cloud Starter is listed at $20/month billed annually (shown as €20 in Europe), with 2,500 workflow executions, and you'll use about 4–10 of those a month.
5. Make a rough total. Illustrative example, not a quote: a 400-person list, weekly sends, n8n Cloud Starter and the free Resend tier comes to about $21 a month. Self-hosting n8n brings that down to the cost of your server.
6. Read the 'when NOT to do this' list below and make your decision. If two or more items apply to you, stop here and write by hand, or use your email tool's built-in AI writer instead.

**Done when:** You can say in one sentence what this will cost you a month and which plan you'll use for each tool. You've also confirmed that you can export your list as a CSV with permission to email everyone on it.

**Watch out:** When NOT to do this. (1) Your list is under about 50 people. Just write a personal email. (2) You're in a regulated field (finance, health, legal) and every claim needs compliance sign-off. The approval step helps, but this course doesn't cover proper compliance review. (3) You already pay for an email platform you're happy with, such as Mailchimp, Kit or Beehiiv. You can keep that and use only the transcription and Claude parts. (4) You won't actually read the draft before tapping Approve. The whole safety of this system depends on that 10-second read. Prices change often, so check each vendor's pricing page before you commit.

## 2. Set up capture, your list and your voice guide

**Goal:** Get a voice memo from your phone into a cloud folder, get your list into Resend on a verified domain, and write a one-page voice guide for Claude.

**Time:** about 40 minutes. **Needs:** iPhone Voice Memos or Android recorder, Google Drive, Resend, Claude app

**Steps (the path that works):**

1. Make the inbox folder. In Google Drive, create a folder called 'Voice notes inbox'. Install the Google Drive app on your phone and sign in.
2. iPhone capture: open Voice Memos, record, then tap the recording > More Actions (the ••• button) > Share > Options > Rendered (this gives you a single .m4a file). Choose Save to Files and pick Google Drive > Voice notes inbox, or tap the Drive app in the share sheet. Android capture: record with your phone's recorder app, then in the Google Drive app tap New (+) > Upload and pick the file. Most recorder apps can also share straight to Drive.
3. Set up sending in Resend. Create a free account, go to Domains > Add Domain and enter a subdomain such as news.yourbusiness.com (Resend recommends a subdomain for deliverability). Copy every record from the Records tab into your DNS host, exactly as shown. If your DNS host is Cloudflare, turn proxying off for any CNAME. Verification often takes about 15 minutes but can take up to 72 hours. Once it's verified, add a DMARC record as Resend suggests.
4. Load your list. In Resend, go to Segments > Create Segment, name it 'Newsletter', then click Add. Import your subscribers as contacts (Resend supports a .csv upload) and make sure they're in the Newsletter segment. Only import people who opted in.
5. Create keys and save them in a password manager. You need a Resend API key (from the API Keys page in Resend), an OpenAI API key (platform.openai.com, with a few dollars of credit), and an Anthropic API key (platform.claude.com). Never paste these into an email or a Google Doc.
6. Build your voice guide. Open the Claude app, paste the prompt below, and paste in 3–5 emails or posts you've written yourself that you're proud of. Save the result as a document called 'Voice guide'. You'll paste it into the workflow in Lesson 3.

**Prompt: Voice guide builder (paste into the Claude app)**

```
I want you to write a one-page voice guide that another writer could use to sound exactly like me in my weekly newsletter.

About me: [your name], [what your business does in one line], writing for [who your readers are, e.g. 'independent café owners in the UK'].

Below are [3–5] pieces I wrote myself. Study them closely.

[paste sample 1]
---
[paste sample 2]
---
[paste sample 3]

Write the guide with these headings:
1. Tone in three words, with a one-line explanation of each.
2. Sentence style: typical length, how I open, how I sign off.
3. Words and phrases I actually use (quote them from the samples).
4. Things I never do (e.g. hype words, exclamation marks, emojis). Base this only on the samples.
5. How I handle opinions, stories and advice.
6. Two short 'sounds like me' vs 'doesn't sound like me' example pairs.

Rules: base everything on the samples, not on general good-writing advice. If the samples disagree with each other, say so instead of guessing. Keep it under 400 words.
```

**Done when:** A test memo from your phone shows up in the Voice notes inbox folder on drive.google.com as an .m4a (or similar) file. Your Resend domain shows as Verified. Your Newsletter segment has the right number of contacts. You also have a saved voice guide that, when you read it back, sounds like you.

**Watch out:** The exact share-sheet labels depend on your iOS version and which apps you've installed. 'Save to Files' only shows Google Drive as a location if the Drive app is installed. Android recorder apps vary by phone maker, so we've described the Drive upload path, which works on any Android phone. Dropbox or OneDrive work too, as long as n8n has a trigger for them. You'd just swap the trigger node in Lesson 3. Keep memos under about 20 minutes, because OpenAI's transcription endpoint has a 25 MB file limit.

## 3. Build the n8n flow: transcribe and rewrite in your voice

**Goal:** When a new memo lands in the folder, n8n automatically transcribes it and Claude turns it into a newsletter draft (subject, preview and body).

**Time:** about 45 minutes. **Needs:** n8n, Google Drive, OpenAI (gpt-transcribe), Anthropic Claude (Sonnet 5.5)

**Steps (the path that works):**

1. In n8n, create a new workflow. Add the Google Drive Trigger node, connect your Google account, set it to watch the 'Voice notes inbox' folder for new files, and poll every 5–15 minutes. Then click 'Fetch test event' with your test memo already in the folder.
2. Add a Google Drive node: Resource 'File', Operation 'Download'. For File, choose 'By ID' and drag in the file ID from the trigger output. Under Options, leave 'Put Output File in Field' as data.
3. Add an HTTP Request node to transcribe. Method POST, URL https://api.openai.com/v1/audio/transcriptions. Set Authentication to 'Predefined Credential Type' and pick your OpenAI credential. Turn on Send Body and set Body Content Type to 'Form-Data'. Add two body parameters. The first has Parameter Type 'n8n Binary File', Name file and Input Data Field Name data. The second has Parameter Type 'Form Data', Name model and Value gpt-transcribe. Run the node. The transcript appears in a field called text.
4. Add an Anthropic node, Text > 'Message a Model'. Connect your Anthropic credential and pick claude-sonnet-5-5. Paste the prompt below as the system message (fill in the brackets and paste your full voice guide). Set the user message to: Transcript of this week's voice note: {{ $json.text }}. Set max tokens to about 2,000.
5. Add a Code node to turn Claude's reply into fields. Paste: return [{ json: JSON.parse($input.first().json.content[0].text) }]. Run it. You should see subject, preview, body_html and checks as separate fields.
6. Read the draft in the output panel. If it doesn't sound like you, change the voice guide, not the transcript, and run it again. Two or three rounds is normal.

**Prompt: Newsletter ghostwriter (system message in the n8n Anthropic node)**

```
You are the ghostwriter for [your name], who runs [your business in one line]. You turn a rough voice-note transcript into this week's newsletter for [who the readers are].

VOICE GUIDE
[paste your full voice guide from Lesson 2]

RULES
- Use only ideas, stories, facts and numbers that appear in the transcript. Never invent a statistic, client, quote, result or link. If something is unclear or sounds misheard, keep it and mark it like this: [CHECK: what is unclear].
- One main idea. [300–500] words. Short paragraphs of 1–3 sentences.
- Structure: (1) a first line that is specific and concrete, not clickbait; (2) the story or point, told the way I told it; (3) one practical takeaway the reader can use this week; (4) one call to action: [your CTA, e.g. 'hit reply and tell me…' or 'book a call at URL'].
- Remove filler words, repetition and false starts from the speech, but keep my phrases, my opinions and my examples.
- Spelling: [British or US] English.
- Never use these words: [e.g. game-changer, unlock, delve, leverage, supercharge].
- HTML for the body: use only <p>, <h2>, <ul>, <li>, <strong>, <em> and <a href>. No inline styles, no images, no <html>, <head> or <body> tags. Do not add a greeting line or sign-off; the template adds them.

OUTPUT
Return only valid JSON, with no code fences and no text before or after it:
{"subject": "under 60 characters, plain and specific", "preview": "under 90 characters, adds to the subject rather than repeating it", "body_html": "the newsletter body", "checks": ["every [CHECK] item and any claim the owner should verify; empty list if none"]}
```

**Done when:** Drop a new memo into the folder, then run the workflow up to the Code node. You get a subject line, preview text and body that a friend would recognise as yours, with nothing in it that you didn't say. Anything uncertain shows up in the checks list.

**Watch out:** n8n's built-in OpenAI node also has an Audio > 'Transcribe a Recording' operation, but n8n's docs say it uses whisper-1 by default. OpenAI now lists whisper-1, gpt-4o-transcribe and gpt-4o-mini-transcribe as deprecated, shutting down 26 February 2027, and recommends gpt-transcribe. That's why we use the HTTP Request node. The exact menu labels for the Google Drive Trigger and the field names in the Anthropic node's output may differ slightly by n8n version. If content[0].text isn't the right path, click the Anthropic node's output panel and drag the field holding Claude's reply into the Code node instead. If Claude ever adds code fences, tell it again in the prompt to return 'only valid JSON'.

## 4. Lay it out, approve it with one tap, send it

**Goal:** Put the draft into your email template, save it as a draft broadcast in Resend, email yourself Approve/Decline buttons, and send only when you tap Approve.

**Time:** about 45 minutes. **Needs:** Claude app, n8n, Resend (n8n node), Gmail (or Slack)

**Steps (the path that works):**

1. Make your template once. Use the prompt below in the Claude app to create a simple, email-safe HTML template with your logo, colours and sign-off. It must contain {{BODY}} where the newsletter goes, and {{{RESEND_UNSUBSCRIBE_URL}}} in the footer.
2. In n8n, add a Code node after the Lesson 3 Code node. Paste: const t = `[paste your whole template here]`; const d = $input.first().json; return [{ json: { ...d, html: t.replace('{{BODY}}', d.body_html) } }];
3. Install the official Resend node. Open the nodes panel (+ or Tab), search Resend and click Install. Under Credentials > Add credential, choose 'Resend OAuth2 API' and Connect my account, or use 'Resend API' with your key.
4. Add a Resend node: Broadcasts > Create. Set Segment to your Newsletter segment, From to Your Name <hello@news.yourbusiness.com>, Subject to {{ $json.subject }}, HTML to {{ $json.html }} and Name to something like Weekly – {{ $now.toFormat('yyyy-MM-dd') }}. Leave sending off. This creates a draft that you can also open and edit in the Resend dashboard.
5. Add a Gmail node: Message > 'Send and Wait for Response'. Send it to yourself, with a subject like 'Approve this week's newsletter?'. Put the subject line, the checks list and the html in the message. Set Response Type to 'Approval' and Type of Approval to 'Approve and Disapprove'. The workflow pauses here until you tap a button.
6. Add an IF node that checks {{ $json.data.approved }} is true. On the true branch, add a Resend node: Broadcasts > Send, passing the broadcast ID from the Create step. Leave the false branch empty, so the draft stays in Resend for you to fix and send by hand.
7. Test safely first. Temporarily point the Create step at a 'Test' segment containing only you. Run it end to end, tap Approve on your phone, and check the email that arrives (layout, links, unsubscribe link). Then switch to the Newsletter segment and click Publish/Activate on the workflow.

**Prompt: Email template maker (paste into the Claude app)**

```
Create a simple HTML email template for my weekly newsletter.

Brand: [business name], logo URL [https://…/logo.png], main colour [#hex], text colour [#hex], font preference [e.g. Georgia or system sans-serif].
Sign-off: [e.g. 'Talk soon, Sam'] and a one-line footer: [business name, postal address if you have one, and why the reader is getting this email].

Requirements:
- Single column, max width 600px, works in Gmail, Apple Mail and Outlook: table-based layout, inline CSS only, no JavaScript, no external CSS, no web fonts required.
- Readable on phones: 16–18px body text, generous line height, links clearly underlined.
- A greeting line at the top: Hi {{{contact.first_name|there}}},
- Put the exact text {{BODY}} where the newsletter content goes. Style p, h2, ul, li and a tags inside that area.
- In the footer, include an unsubscribe link whose href is exactly {{{RESEND_UNSUBSCRIBE_URL}}}.
- Return the complete HTML document only, ready to paste.
```

**Done when:** You tap Approve in the test email and, within a minute or two, the finished newsletter arrives in your own inbox from your subdomain. The greeting shows your first name, the layout looks right on your phone, and the unsubscribe link opens Resend's unsubscribe page. Tapping Decline on a second test sends nothing, and the draft is still there under Broadcasts in Resend.

**Watch out:** Menu labels here come from n8n's docs and Resend's n8n integration page, but n8n renames things between versions. In some versions the Gmail operation shows as 'Send and Wait for Approval'. If you'd rather approve in Slack, the Slack node has the same 'Send and Wait for Response' operation with an Approval response type, and it returns data.approved. Resend's Broadcast API also accepts send: true on Create, but don't use it here, because it skips your approval. Check the Resend node's field names (for example Segment versus Segment ID) in your n8n version. We couldn't confirm every field label from the docs.

## 5. Run it weekly, safely, and see if it's working

**Goal:** Turn the pipeline into a 15-minute weekly habit with clear safety rules and three numbers worth watching.

**Time:** about 20 minutes. **Needs:** Resend dashboard, n8n Executions, Claude app

**Steps (the path that works):**

1. Set a weekly slot. Pick the same day each week to record, for example Tuesday on a walk. Before you hit record, say three things to yourself: the one idea, the story behind it, and what the reader should do next.
2. Follow the approval rule every time. Read the whole draft and the checks list before you tap Approve. If anything in checks is unresolved, tap Decline and fix the draft in Resend's Broadcasts editor. Never approve from a notification preview.
3. Check that it ran. After each memo, open Executions in n8n to see a green (success) or red (failed) run. Common failures are an expired Google connection, no API credit left, or a memo over 25 MB. Turn on an error workflow or email alert in n8n's workflow settings if your plan supports it.
4. Measure three things monthly in Resend's Broadcasts page: clicks on your call-to-action link, replies to the email (count them in your inbox), and unsubscribes. Treat open rates as a rough signal only, because some email apps preload images, which inflates opens.
5. Improve the voice once a month. Paste two of Claude's drafts, and what you actually sent after edits, into the prompt below. Copy the updated voice guide into the system message from Lesson 3.
6. Keep your list clean. In Resend Contacts, filter All subscriptions > Unsubscribed to see who left. Resend won't email unsubscribed or suppressed contacts. Remove any address that bounces repeatedly, and never re-add someone who unsubscribed.

**Prompt: Monthly voice tune-up (paste into the Claude app)**

```
Here is my current newsletter voice guide:
[paste voice guide]

Below are pairs of (A) the draft an assistant wrote from my voice note and (B) the version I actually sent after editing.

Pair 1 – A:
[paste draft]
Pair 1 – B:
[paste sent version]

Pair 2 – A:
[paste draft]
Pair 2 – B:
[paste sent version]

Tasks:
1. List the specific changes I keep making (words cut, tone shifts, structure changes). Quote examples.
2. Rewrite the voice guide so that future drafts need fewer of those edits. Keep the same headings and keep it under 400 words.
3. List anything in the old guide that my edits contradict, so I can decide whether to drop it.
Do not add general writing advice that isn't supported by my edits.
```

**Done when:** After four weeks you've sent four issues, each approved after a full read. You know your click, reply and unsubscribe counts for the month, and your edits per draft are getting smaller (track this roughly yourself, for example 'heavy, medium, light').

**Watch out:** When to pause the system: unsubscribes jump well above your usual level after an issue, a reader points out something factually wrong, or you notice you're approving without reading. Go back to writing by hand for a week and fix the prompt. Resend's Broadcasts page shows deliverability and, if tracking is turned on, opens and clicks. Exact report names may differ from what we describe, so we've kept the menu paths general.

## Sources

- [Resend pricing (transactional and marketing plans)](https://resend.com/pricing)
- [Claude API: models overview and pricing](https://platform.claude.com/docs/en/models/overview)
- [Resend API: Create Broadcast](https://resend.com/docs/api-reference/broadcasts/create-broadcast)
- [Resend docs: Broadcasts introduction](https://resend.com/docs/dashboard/broadcasts/introduction)
- [Resend docs: Segments](https://resend.com/docs/dashboard/segments/introduction)
- [Resend docs: Add a domain](https://resend.com/docs/dashboard/domains/add-a-domain)
- [Resend docs: Handle unsubscribes](https://resend.com/docs/dashboard/broadcasts/handle-unsubscribes)
- [Resend docs: n8n integration (official node)](https://resend.com/docs/knowledge-base/n8n-integration)
- [n8n pricing](https://n8n.io/pricing/)
- [n8n docs: Slack Send and Wait for Response approvals](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.slack/approvals)
- [n8n docs: Gmail message operations](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/message-operations/)
- [n8n docs: HTTP Request node](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/)
- [n8n docs: OpenAI node audio operations](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/audio-operations/)
- [OpenAI: Speech to text guide](https://developers.openai.com/api/docs/guides/speech-to-text)
- [OpenAI: gpt-transcribe model page](https://developers.openai.com/api/docs/models/gpt-transcribe)
