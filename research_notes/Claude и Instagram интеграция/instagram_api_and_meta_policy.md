# Instagram API and Meta Policy: what's possible and what's forbidden when connecting Claude to Instagram (as of Oct 2026)

> Method note: developers.facebook.com, respond.io and some other hosts could not be fetched from this research session (blocked by DNS/network allowlist). Findings come from web-search snippets of official Meta docs (developers.facebook.com, help.instagram.com) plus secondary press and vendor blogs. Where only vendor or secondary sources back a number, that is flagged. Verify exact numbers against the live Meta docs before building.

## 1. Official Instagram APIs (2024–2026): capabilities, account types, permissions, limits, deprecations

### Takeaway
The only legitimate way for an AI agent to act on Instagram is the **Instagram Platform** (Graph API). It comes in two setups. **Instagram API with Instagram Login** needs no Facebook Page and covers publishing, comments, DMs and insights. **Instagram API with Facebook Login for Business** additionally covers hashtag search, Business Discovery, ads and tagging. Both require a professional (Business or Creator) account and Meta App Review for Advanced Access. The publishing cap is now reportedly **100 API posts per rolling 24 h** (it was historically 25, then 50). General call limits come from the impressions-based Business Use Case formula, not a flat "200/hour".

### Cited Findings
**Two API setups**
- Meta's Instagram Platform overview has a capability table. Hashtag search is marked unavailable for "Business Login for Instagram" and available only via Facebook Login for Business, gated by the "Instagram Public Content Access" feature. — [Instagram Platform overview](https://developers.facebook.com/documentation/instagram-platform/overview)
- The Instagram Login setup "does not require a Facebook Page to be linked to the Instagram professional account". It "cannot access ads or tagging". — [Instagram API with Instagram Login](https://developers.facebook.com/docs/instagram-platform/instagram-api-with-instagram-login)
- Instagram Login scopes are `instagram_business_basic`, `instagram_business_content_publish`, `instagram_business_manage_messages` and `instagram_business_manage_comments`. They replaced older `business_*` scope values. The deprecation date for the old scopes differs between doc versions (Jan 27, 2025 vs Dec 17, 2024). — [Instagram API with Instagram Login doc](https://developers.facebook.com/documentation/instagram-platform/instagram-api-with-instagram-login); [older overview](https://developers.secure.facebook.com/docs/instagram/instagram-only-api/overview)
- The Facebook Login path uses classic scopes such as `instagram_basic` and `instagram_content_publish` (plus `instagram_manage_comments`, `instagram_manage_messages`, `instagram_manage_insights`, `pages_*`). A third-party guide notes that sources mix these names up. — [Phyllo guide 2026](https://www.getphyllo.com/post/instagram-api-guide)
- Unified.to's developer guide lists the Instagram Login API launch date as July 23, 2024. — [unified.to](https://docs.unified.to/skills/instagram-oauth-app/SKILL.md)

**Content publishing (posts, reels, carousels, stories)**
- Meta's content publishing doc covers single images, videos/Reels, carousels and stories. JPEG is the only supported image format. Media must be on a publicly accessible URL at the time of publishing. Publishing is a two-step flow: create a media container, then call `media_publish`. — [Meta Content Publishing doc](https://developers.facebook.com/documentation/instagram-platform/content-publishing); [Zernio 2026 guide](https://zernio.com/blog/instagram-api)
- **Publishing cap:** the current content-publishing page reportedly says **100 API-published posts per rolling 24 h per account**, and a carousel counts as one post. The cap was 25/day in 2021 and later 50. The `content_publishing_limit` field reference still says "currently 50", so docs are inconsistent. Check `GET /<IG_ID>/content_publishing_limit` at runtime. Meta recommends that apps enforce the limit themselves, especially when they offer scheduling. — [Blotato](https://www.blotato.com/blog/instagram-posting-api); [Meta Content Publishing doc](https://developers.facebook.com/documentation/instagram-platform/content-publishing); [DEV Community 2026](https://dev.to/preecha/how-to-use-instagram-graph-api-in-2026-5hlg)
- **Conflict:** the brief's "25/50 publishes per 24h" is outdated. Older docs said 25 and later 50, and current secondary sources cite 100. Confirm on the live page.

**Comments, mentions, hashtags, Business Discovery**
- Hashtag Search: max **30 unique hashtags per Business/Creator account per rolling 7 days**. Repeat queries on the same hashtag don't count again. The flow is `GET /ig_hashtag_search?user_id=..&q=..`, then `top_media` / `recent_media`. It requires App Review for Instagram Public Content Access plus `instagram_basic`. You **cannot comment** on hashtag-discovered media, and hashtags in Stories are unsupported. — [Meta Hashtag Search doc](https://developers.facebook.com/documentation/instagram-platform/instagram-api-with-facebook-login/hashtag-search)
- The Instagram Login path offers comment moderation via `instagram_business_manage_comments`: read, reply, hide and delete comments on your own media. — [Instagram API with Instagram Login](https://developers.facebook.com/docs/instagram-platform/instagram-api-with-instagram-login)

**Rate limits**
- There are two regimes. Platform Rate Limits apply to app/user tokens. Business Use Case (BUC) limits apply to Instagram Platform requests and are sized as **4800 × number of impressions** of the account per rolling 24 h. Usage is reported in the `X-Business-Use-Case-Usage` header, and BUC applies when both could apply. Phyllo disputes the commonly quoted flat "200 calls/hour". — [Phyllo rate-limit guide (Jan 2026)](https://www.getphyllo.com/post/navigating-instagram-api-rate-limit-errors-a-comprehensive-guide); [AdaptlyPost](https://adaptlypost.com/blog/instagram-api-rate-limit-4800-impressions); [bundle.social (Aug 2026)](https://bundle.social/blog/instagram-api-rate-limits)
- Messaging limits reported by secondary sources: Conversations API about 2 calls/sec per professional account, Send API (text/links) about 100 calls/sec per professional account. These are unverified against Meta's docs. — [apis.io rate-limits page](https://apis.io/rate-limits/instagram/instagram-rate-limits/)
- The "200 calls/hour" figure dates from the older Graph API platform limit (200 × users per hour). Treat it as legacy. — [Phyllo guide](https://www.getphyllo.com/post/instagram-api-guide)

**Deprecations**
- The **Instagram Basic Display API was shut down Dec 4, 2024**. Its replacement is Instagram API with Instagram Login, which needs a professional account. The vendor claim that it "supports personal accounts" is contested, and Phyllo points personal (non-Page) accounts to the Instagram Login API. Consumer personal accounts no longer have an official read API. — [Smash Balloon](https://smashballoon.com/instagram-is-shutting-down-basic-display-api-continue-displaying-instagram-feeds-on-your-site/); [Phyllo](https://www.getphyllo.com/post/instagram-api-get-post-use-display-api-to-access-user-info)

### Inferences
- A Claude agent through official APIs can draft and publish posts, Reels, carousels and stories; moderate and reply to comments on its own media; answer DMs within the policy windows; and read insights. These are all limited to the **user's own professional account**, authorized via OAuth.
- Competitor and hashtag research needs the Facebook Login path plus Public Content Access review, and is capped at 30 hashtags/week. Reading arbitrary private profiles or other users' DMs is impossible officially.
- An MCP server for Claude should wrap these endpoints with per-account token storage and a local publish-limit check.

### Gaps
- Could not fetch live Meta docs to confirm the exact current publishing cap (50 vs 100), messaging per-second limits, or 2026 changelog entries. Graph API version numbers for 2026 are not confirmed.
- Exact insights metric deprecations in 2025–2026 (e.g., impressions → views) were not verified.

## 2. Meta's rules for AI chatbots in Instagram DMs; the WhatsApp AI-provider ban; AI labels

### Takeaway
Instagram DMs via the Messaging API are governed by the **"Messenger Platform and IG Messaging API policy"**. Bots may reply within **24 h** of the user's last message. The **HUMAN_AGENT** tag extends this to 7 days, for human replies only. A newer ad-started-chat window of up to 7 days reportedly applies since 2026. The **WhatsApp Business ban on general-purpose AI assistants** (effective Jan 15, 2026) is **WhatsApp-specific**. No equivalent Instagram/Messenger rule was found, and in the EU it was challenged by Italy's AGCM and the European Commission. AI-generated content on Instagram carries "AI info" labels, and since Aug 31, 2026 accounts featuring AI-generated people must use the "AI-generated profile" label or lose recommendation eligibility.

### Cited Findings
**Messaging windows and tags**
- Standard window: **24 hours** from the customer's last message. The HUMAN_AGENT tag extends it to **7 days**, for cases such as the business being closed over the weekend or an issue needing more than 24 h. It needs the Human Agent permission and the tag on every message, and it is not for sales or automated messages. Automated or auto-reply messages fall under the 24 h window. — [KeyCRM help](https://help.keycrm.app/en/communications-sms-email-instagram-telegram-viber-marketplace-chats-telephony/response-timeframes-on-facebook-and-instagram); [Inro glossary](https://www.inro.social/glossary/24-hour-messaging-window)
- One vendor reports that since **Sept 28, 2026**, chats started from Click-to-Messenger / Click-to-Instagram-Direct ads get a messaging window of "up to" 7 days in which bots may also send. A vendor also claims Meta rejects message "update tags" since Apr 27, 2026. Neither claim is confirmed in Meta docs. — [Spur](https://www.spurnow.com/en/blogs/instagram-messenger-ads-7-day-messaging-window)
- The Messenger Platform and IG Messaging API policy (page reportedly last updated Apr 6, 2026) requires bots registered as "automated" to respond to every user message within a set time. No explicit AI-disclosure clause or general-purpose-AI ban was found in snippets. — [Meta Messenger Platform & IG Messaging API policy](https://developers.facebook.com/documentation/business-messaging/messenger-platform/policy)

**WhatsApp general-purpose AI ban (context; WhatsApp only)**
- WhatsApp Business Solution Terms added an "AI providers" section. It bars "providers and developers of artificial intelligence or machine learning technologies, including but not limited to large language models, generative AI platforms, and general-purpose AI assistants" when AI is the primary functionality. It applied to new users from Oct 15, 2025 and to all users from **Jan 15, 2026**. Business bots for support, sales and notifications remain allowed. — [TechCrunch Oct 18, 2025](https://techcrunch.com/2025/10/18/whatssapp-changes-its-terms-to-bar-general-purpose-chatbots-from-its-platform/); [Business Standard](https://www.business-standard.com/technology/tech-news/meta-bans-ai-chatbots-from-whatsapp-business-api-chatgpt-to-shut-down-jan-2026-125102200335_1.html)
- ChatGPT, Microsoft Copilot and Perplexity announced exits from WhatsApp, leaving Meta AI as the only general-purpose assistant there. — [Gulf News](https://gulfnews.com/technology/no-more-chatgpt-and-perplexity-on-whatsapp-meta-bans-major-ai-chatbots-from-2026-1.500316016); [APH Networks](https://aphnetworks.com/news/30920-meta-says-no-more-general-purpose-chatbots-whatsapp-except-its-own)
- Italy's AGCM imposed interim measures in Dec 2025 ordering suspension of the terms, and Meta exempted Italy. The European Commission sent a Statement of Objections in Feb 2026 and a supplementary SO on Apr 15, 2026. Meta reportedly replaced the outright ban with a pricing framework for third-party AI assistants. Aggregator and AP reports say the Commission adopted interim measures around June 9, 2026 ordering restored access on equivalent conditions; this is not verified against the EC press release. — [AGCM press release](https://en.agcm.it/en/media/press-releases/2025/12/A576); [SCL](https://www.scl.org/european-commission-notifies-meta-of-possible-interim-measures-to-reverse-exclusion-of-third-party-ai-assistants-from-whatsapp/); [PPC Land](https://ppc.land/eu-accuses-meta-of-using-fees-to-keep-ai-rivals-off-whatsapp/); [Digital Policy Alert](https://digitalpolicyalert.org/change/17349); [WHEC/AP](https://www.whec.com/?p=1093801)
- No source found extends the AI-provider ban to Instagram or Messenger. — (searches above; see Gaps)

**AI labels and disclosure**
- Meta labels AI content on Facebook, Instagram and Threads (since 2024). The "Made with AI" label was renamed "AI info". Labels are triggered by C2PA/IPTC metadata, invisible watermarks or self-disclosure. Fully generated content gets a more prominent label, while minor edits are noted in the menu. — [gradually.ai](https://www.gradually.ai/en/instagram-ai-label/)
- On **Aug 31, 2026** Instagram renamed the optional "AI creator" label to **"AI-generated profile"**. Accounts that feature an AI-generated person without disclosure may become ineligible for recommendations. Using AI tools for editing, captions or individual pieces of content does not require the profile label. — [TechCrunch Aug 31, 2026](https://techcrunch.com/2026/08/31/instagram-puts-new-limits-on-undisclosed-ai-profiles/); [TechRepublic](https://techrepublic.com/article/news-instagram-ai-generated-profile-label-recommendations/)

### Inferences
- A Claude-powered **customer-service/sales DM assistant** for a brand's own Instagram account is a sanctioned use case, as long as it respects the 24 h window, uses HUMAN_AGENT only for real humans, and offers human handoff.
- Offering "ChatGPT/Claude-as-a-general-assistant inside Instagram DMs" as a product is not explicitly banned on Instagram per available sources. It is, however, exactly the pattern Meta banned on WhatsApp, so platform risk is high and policy could change.
- Images generated by AI and published via API should be labelled AI using Instagram's "AI info" toggle or C2PA metadata. A virtual-influencer account run by Claude needs the "AI-generated profile" label. Telling users in the DM that they are talking to an AI is good practice and mirrors Meta's own Creator AI disclaimer.

### Gaps
- Could not read the full current Messenger/IG Messaging policy text to confirm whether it contains an explicit AI-disclosure requirement or AI-provider restriction.
- Whether the API can set the "AI info" label programmatically at publish time was not confirmed.
- Final outcome of the EC interim measures (and global vs EEA scope) is unverified.

## 3. Instagram Terms on automation and scraping; unofficial private APIs (instagrapi, instaloader); legal cases

### Takeaway
Instagram's Terms prohibit accessing or collecting data "using automated means (without our prior permission)". Meta's separate **Automated Data Collection Terms** (Oct 7, 2024) bar scrapers, bots and crawlers without express written permission. Unofficial libraries such as instagrapi (which emulates the mobile private API) and instaloader therefore violate the Terms and trigger "challenge_required" checkpoints, action blocks and bans. In court, *Meta v. Bright Data* (N.D. Cal., Jan 23, 2024) held that **logged-out scraping of public data** did not breach Meta's terms. Logged-in automation, which is what instagrapi does, remains a clear contract breach, and Meta actively sues in that area.

### Cited Findings
- Terms wording, as quoted by third parties: "You may not access or collect data from our Products using automated means (without our prior permission) or attempt to access data you do not have permission to access." — [ScrapeOps](https://scrapeops.io/websites/instagram/) (verify against [Instagram Terms](https://help.instagram.com/581066165581870))
- Instagram Help Center: the Terms don't allow attempts to create accounts or access and collect information in unauthorized ways, and it describes unauthorized scraping as automation that collects information in violation of the Terms. — [Instagram Help](https://help.instagram.com/740480200552298)
- Meta's Automated Data Collection Terms (effective Oct 7, 2024) bar scrapers, bots and crawlers without express written permission. — [Thunderbit summary](https://thunderbit.com/da/blog/is-scraping-instagram-legal) (secondary)
- **Meta v. Bright Data**, No. 3:23-cv-00077-EMC, Judge Edward Chen, Jan 23, 2024. Summary judgment for Bright Data on breach of contract: the terms did not bar logged-out scraping of public data. Bright Data's own business accounts were held unrelated to its scraping. A tortious-interference claim could be amended. Meta dropped the suit in Feb 2024, with no appeal. Commentators stress the ruling is fact-specific and does not bless all scraping. — [TechCrunch](https://techcrunch.com/2024/01/24/court-rules-in-favor-of-a-web-scraper-bright-data-which-meta-had-used-and-then-sued); [Eric Goldman blog](https://blog.ericgoldman.org/archives/2024/01/game-on-bright-data-scores-major-victory-in-web-scraping-dispute-with-meta-guest-blog-post.htm); [MediaPost (dropped)](https://www.mediapost.com/publications/article/393996/None); [Farella Braun](https://www.fbm.com/technology/publications/major-decision-affects-law-of-scraping-and-online-data-collection-meta-platforms-v-bright-data/)
- **Meta v. Social Data Trading Ltd** (complaint, 2021): Meta alleges the defendant used bots posing as Android devices to scrape public Instagram profiles. This is the same technique as private-API libraries. — [Complaint PDF via Jurist](https://www.jurist.org/news/wp-content/uploads/sites/4/2021/12/Meta-Platforms-Inc.-v.-Social-Data-Trading-Ltd.pdf)
- Ban mechanics: "challenge_required" is a verification checkpoint triggered by suspected bot-like behaviour. It often clears in hours, but repeated automation can lead to days-to-weeks restrictions or a ban. Instagram treats automated activity (likes, follows, comments, DMs) as suspicious regardless of intent. — [Proxidize](https://proxidize.com/blog/instagram-challenge-required/); [Spur](https://www.spurnow.com/blogs/instagram-automated-behaviour); [CreatorFlow](https://creatorflow.so/blog/we-suspect-automated-behavior-instagram/) (all vendor/SEO sources)
- Violating the terms is generally a civil contract matter rather than a crime. This is a secondary blog opinion, not legal authority. — [ScrapeOps](https://scrapeops.io/websites/instagram/)

### Inferences
- **High ban risk:** Claude "computer-use" or browser agents driving a logged-in Instagram account; instagrapi-based MCP servers (login with username/password, DM automation, mass follow/like); instaloader with login. These breach the Terms, can lose the account, and expose operators commercially to Meta litigation.
- **Gray area:** logged-out scraping of public data. Bright Data shows a contract claim may fail, but Meta can still block IPs and pursue other theories, and GDPR applies to personal data.
- **Legitimate:** Graph API via an approved Meta app with OAuth on the user's own professional account.

### Gaps
- No primary source found specifically naming instagrapi or instaloader in Meta enforcement. No quantitative ban-rate data exists in reliable sources.
- Could not fetch the current Instagram Terms text directly to verify wording or the latest revision date.

## 4. Meta's own AI on Instagram (Meta AI, AI Studio) as competitor and context

### Takeaway
Meta ships first-party AI inside Instagram. **Meta AI** is in DMs and search. **AI Studio** (US rollout July 2024) lets creators build a "Creator AI" that auto-answers DMs and story replies with a visible AI disclaimer. This makes Meta both the platform owner and a direct competitor to third-party Claude DM bots, and it exempted its own assistant from the WhatsApp ban.

### Cited Findings
- AI Studio rolled out to all US creators in July 2024 after June testing. Creators build chatbots from prompts or templates. — [TechCrunch Jul 30, 2024](https://techcrunch.com/2024/07/30/meta-is-rolling-out-its-ai-studio-in-the-u-s-for-creators-to-build-ai-chatbots)
- Instagram professional accounts can set up an AI "extension of themselves" to answer common DMs and story replies. Creators control auto-replies and who the AI responds to from the professional dashboard. A disclaimer in DMs tells users they are talking to an AI. — [Engadget](https://www.engadget.com/instagram-creators-can-now-make-ai-doppelgangers-to-chat-with-their-followers-220052768.html); [Social Samosa](https://www.socialsamosa.com/news-2/meta-rolls-out-ai-studio-us-6712235)
- Instagram help pages say these bots reply automatically and pause when a person joins the conversation. Availability depends on country and account. — [Inro 2026](https://www.inro.social/blog/instagram-ai-custom-ai-meta-ai-studio) (third-party)
- The WhatsApp ban leaves Meta AI as the only general-purpose assistant there, which drove EU and Italian antitrust action. — [APH Networks](https://aphnetworks.com/news/30920-meta-says-no-more-general-purpose-chatbots-whatsapp-except-its-own); [AGCM](https://en.agcm.it/en/media/press-releases/2025/12/A576)

### Inferences
- A Claude-based Instagram DM product competes with free, native Creator AI. Its differentiation would be brand control, CRM/back-office integrations, multi-channel use, and model quality.
- Meta's self-preferencing on WhatsApp signals a policy risk that similar terms could later reach the Instagram Messaging API.

### Gaps
- No reliable 2026-specific data on AI Studio availability outside the US/EU, or on Meta AI feature changes inside Instagram in 2026.
