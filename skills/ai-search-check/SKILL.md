---
name: ai-search-check
description: Checks whether ChatGPT, Perplexity, Gemini and Google's AI answers name a business for the questions its customers ask, explains why the businesses that do get named win, and lists the fixes in order of impact. Use for "does ChatGPT recommend us", when a competitor keeps getting recommended instead, or as a fixed-price entry audit for a new client.
when_to_use: does chatgpt recommend us, ai search check, are we in ai answers, why does AI recommend my competitor, AEO, GEO, AI overviews, get cited by ChatGPT, llms.txt, ai visibility audit
argument-hint: "[business + domain + city if local | 'monitor']"
metadata:
  humanai:
    version: 0.1.0
    reads: [business, competitors]
    writes: [learnings]
---

# AI Search Check

More buyers now ask an assistant before they search, and get a short list with reasons. This skill measures whether the business is on that list, honestly, and says what would put it there. Done means a check anyone could re-run with the same questions, results counted only over answers actually seen, and a short fix list in order of impact.

Adapted from Boring Marketing's `ai-search` (MIT). See THIRD_PARTY_NOTICES.md.

## Measurement rules (these make the result worth trusting)

- **10 to 15 questions, frozen.** Write them down verbatim; a re-check uses exactly the same list.
- **Four states per answer:** CITED (their site is a source), MENTIONED (named, but others tell their story), ABSENT (answer seen, they're not in it), NOT CHECKED (couldn't capture it).
- **Count over what you saw.** "Named in 4 of 11 answers checked", never "36% visible".
- **A failed capture is never a finding.** A timeout is NOT CHECKED, not ABSENT. Never tell a client they're invisible over a run with failed captures.
- **Say which engine, which date, which location.** Answers vary run to run; one run is a sample.
- **Proxies are labelled.** If you used web search results as a stand-in for an engine's live answer, say so in plain words.

## Build the questions

Ask the way a buyer asks an assistant, not the way they type into Google. Mix: category ("best <service> for <buyer> in <city>"), comparison ("<them> vs <competitor>"), problem (the pain before they know the category), and brand ("is <them> any good"). For a local business, every question names the place, plus one urgent and one cost question.

Run the brand probe first: "What is <business>?" If the answer describes someone else, that's finding number one. Nothing else compounds until the engines connect the name to the site.

Ask the owner once to paste real ChatGPT, Perplexity or Gemini answers for their top three questions. Pasted answers beat any proxy.

## Why the winners win

For each answer, read the sources the engine cited. The usual reasons, in order of how often they matter for small businesses:
1. A page that answers the exact question directly in the first two sentences.
2. Being named on third-party pages the engines trust (directories, local press, "best of" lists, review sites).
3. Consistent facts everywhere: name, address, phone, services, hours.
4. Fresh, dated content with a named author.
5. Structured data (Organization, LocalBusiness, Service, FAQ) and a crawlable site that doesn't block AI crawlers in robots.txt.

Check facts in every answer that names them: wrong phone numbers or services are the most urgent fix.

## The fix list

Order by leverage: wrong facts first, then the missing direct-answer pages for the questions they're absent from, then third-party mentions worth earning, then technical items (robots.txt, schema, an llms.txt summary page). One line each on why. Say plainly what can't be fixed quickly.

## Monitor

Monthly, re-run the frozen questions, compare states question by question, and note what changed and the likely reason. No new questions in a monitor run; add them in a fresh check.
