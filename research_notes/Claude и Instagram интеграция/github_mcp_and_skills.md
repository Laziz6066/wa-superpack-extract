# GitHub census: Instagram MCP servers and Claude skills/plugins (as of 2026-10-30)

Method: GitHub repository search via the GitHub MCP tool (queries "instagram mcp" [786 hits], "instagram in:name mcp" [802], "instagram claude skill" [581], "instagram mcp instagrapi OR playwright OR instaloader OR apify"), GitHub code search (`instagram filename:SKILL.md path:.claude/skills`, 4,376 hits), plus raw README / LICENSE / requirements / package.json reads for ~20 repos, plus awesome-list READMEs. Star counts are from the GitHub search API on 2026-10-30. "Last activity" = the repo's `updated_at` from the API (note: `updated_at` also moves when a repo is starred, so it is a weak proxy for code activity; `pushed_at` was not available because direct REST search was blocked in this session). The raw GitHub REST search endpoint was blocked (403 "sessions are bound to their configured repositories"); developers.facebook.com could not be fetched (outside allowed network domains).

## Which Instagram MCP servers exist on GitHub, and which are most popular/maintained?

### Takeaway
There are dozens of Instagram MCP servers, but none has a large following: the most-starred dedicated one (jlbadano/ig-mcp) has about 200 stars. They split into two groups. One group is official Graph API servers (jlbadano/ig-mcp, mikusnuz/meta-mcp, exileum/meta-mcp, adelaidasofia/instagram-mcp, oliverames/meta-mcp-server, openinstaflow). The other is unofficial private-API, cookie or browser servers (trypeggy/instagram_dm_mcp via instagrapi, Bob-lance and arjun1194 via instagram-private-api, braindead-dev via session cookies, duhlink via Chrome profile + Puppeteer/Playwright, inssist via a Chrome extension). A third, growing set is hosted third-party data/scheduler MCPs (HasData, HikerAPI-based, Publora, PostZen, Composio, etc.). The highest-starred "Instagram + MCP" repos overall are adjacent tools (Meta Ads, video makers, schedulers) rather than Instagram account servers.

### Census table — dedicated Instagram MCP servers

| Repo | Stars | Last activity (updated_at) | Lang | API approach | Features | Auth | License | Maturity / risk notes |
|---|---|---|---|---|---|---|---|---|
| [jlbadano/ig-mcp](https://github.com/jlbadano/ig-mcp) | 203 | 2026-10-29 (created 2025-05) | Python | Official Instagram Graph API | Profile, media, insights, publish image/video, DM reply (needs Advanced Access) | Long-lived access token (`instagram_basic`, `instagram_content_publish`, `instagram_manage_insights`, `instagram_manage_messages`) | MIT | Most-starred dedicated IG MCP; Business accounts only; 8 open issues; "MseeP verified" badge |
| [trypeggy/instagram_dm_mcp](https://github.com/trypeggy/instagram_dm_mcp) | 187 | 2026-10-29 (created 2025-06) | Python | **Unofficial private API: `instagrapi==2.1.5`** (requirements.txt) | DMs: list threads/messages, send, shared post/reel info | Instagram **username + password** in `.env`/CLI args; `username_session.json` session files on disk | MIT (Gala Labs Inc) | Listed in wong2/awesome-mcp-servers; high ToS/ban risk; plaintext password in MCP config |
| [mikusnuz/meta-mcp](https://github.com/mikusnuz/meta-mcp) | 31 | 2026-10-29 | TypeScript | Official Graph API v26.0 + Threads API | 66 tools (IG 33, Threads 27, Meta 6): publish photo/video/reel/story/carousel, comments, insights, hashtag search, DMs, collab invites | Access tokens (env) | MIT | Actively versioned (v2.x); in punkpeye awesome list; sibling of mikusnuz/meta-ads-mcp (91★) |
| [exileum/meta-mcp](https://github.com/exileum/meta-mcp) | 13 | 2026-10-14 | TypeScript | Official Graph API v25.0 + Threads | Publish, comments, insights, hashtags, DMs; stdio or Streamable HTTP | `INSTAGRAM_ACCESS_TOKEN`, `THREADS_ACCESS_TOKEN`, optional app ID/secret | MIT | Config validation at startup; 19 open issues |
| [adelaidasofia/instagram-mcp](https://github.com/adelaidasofia/instagram-mcp) | 13 | 2026-10-29 | Python (FastMCP) | Official Graph API, explicitly "ToS-safe, no private API" | 29 tools: multi-account, publish (image/video/reel/carousel/story), publishing quota, insights incl. audience, comments (reply/hide/delete), review-gated DMs | Long-lived token; stored in macOS keychain or chmod 600 file; token scrubber on outputs; JSONL audit log | MIT | Best security posture observed (token redaction, keychain, audit log) |
| [oliverames/meta-mcp-server](https://github.com/oliverames/meta-mcp-server) | 64 | 2026-10-29 | TypeScript | Official Graph API (v21.0 badge) | ~200 tools across FB Pages, IG, Threads, Ads, Commerce, CAPI, Ad Library | `META_ACCESS_TOKEN` (Graph API Explorer token suggested) | MIT | Very broad surface; desktop bundle (.mcpb) available |
| [Narla-Venkata-Anand-Sai-Kumar/openinstaflow](https://github.com/Narla-Venkata-Anand-Sai-Kumar/openinstaflow) | 20 | 2026-07-28 | TypeScript | Official Graph API (IG Login or FB Login) | Profile, media, insights, publish image/reel/story/carousel, Pages, DMs (Advanced Access) | `IG_ACCESS_TOKEN`, `IG_USER_ID`, optional Page token | no LICENSE file found | Tools accept per-call token override |
| [arjun1194/insta-mcp](https://github.com/arjun1194/insta-mcp) | 13 | 2026-10-27 | TypeScript | **Unofficial: `instagram-private-api` npm** | Post photo/video/reel/carousel, insights, followers/unfollowers, like/comment, DMs, pending requests | `INSTAGRAM_USERNAME`/`INSTAGRAM_PASSWORD`; sessions in `./data` | none found | Listed in punkpeye awesome list; ban risk |
| [Bob-lance/instagram-engagement-mcp](https://github.com/Bob-lance/instagram-engagement-mcp) | 47 | 2026-10-29 (created 2025-03) | JavaScript | **Unofficial: `instagram-private-api`** (README: "uses the Instagram Private API, which is not officially supported") | Comment sentiment, demographics, lead identification, engagement reports | Username + password in `.env` / MCP config | MIT | Early (2025) entrant; lead-gen scraping use case |
| [duhlink/instagram-server-next-mcp](https://github.com/duhlink/instagram-server-next-mcp) | 51 | 2026-10-29 (created 2024-12) | TypeScript | **Browser automation**: Puppeteer + Playwright with Chrome's existing login (`CHROME_USER_DATA_DIR`) | Fetch posts, save media + metadata | Reuses Chrome profile session | none found | One of the oldest (Dec 2024); scraping only |
| [braindead-dev/instagram-dms-mcp](https://github.com/braindead-dev/instagram-dms-mcp) | 10 | 2026-09-23 | Go | **Unofficial web API via session cookies** | Read/send DMs; optional forwarding of new DMs to "Poke" | `IG_SESSION_ID`, `IG_CSRF_TOKEN` copied from DevTools; Render deploy button | none found | Deploying session cookies to a cloud host = account-takeover risk if leaked |
| [inssist/mcp](https://github.com/inssist/mcp) | 27 | 2026-10-22 (created 2026-09) | TypeScript | **Browser extension bridge**: INSSIST Chrome extension in the user's logged-in instagram.com session (loopback) | Profiles, DMs, publish/schedule posts/reels/stories with music, insights, audience reports, media download | User's own browser session; pairing via extension toggle | MIT | Vendor-backed; works for personal accounts; README pitches beyond Graph API limits (Stories with music etc.). Commercial extension |
| [lupikovoleg/instagram-cli](https://github.com/lupikovoleg/instagram-cli) | 44 | 2026-10-23 | Python (FastMCP) | **Third-party: HikerAPI** (paid private-API proxy) + OpenRouter | Analytics, downloads, pinned/tagged posts, comment replies, media insights | `HIKERAPI_KEY` | none found | Credit-metered; no IG login needed |
| [HasData/instagram-mcp](https://github.com/HasData/instagram-mcp) | 15 | 2026-10-29 | JavaScript | **Third-party hosted scraper (HasData)** | Read-only: public profile, posts feed, comments by URL | HasData API key or OAuth connector | MIT | In punkpeye awesome list; read-only public data |
| [Shudesu/ig-harness-oss](https://github.com/Shudesu/ig-harness-oss) | 62 | 2026-10-26 | TypeScript | Official Graph API (Instagram Login), Cloudflare Workers | Comment-to-DM, story-mention DM, keyword triggers, drip DMs, forms; MCP + SDK | Meta app + owner/admin key; `IG_HARNESS_READ_ONLY=true` mode | MIT | Japanese ManyChat-style alternative; 19 open issues |
| [Morfeu333/instagram-video-analyzer-mcp](https://github.com/Morfeu333/instagram-video-analyzer-mcp) | 13 | 2026-10-29 | Python | Download + AI analysis (not verified in detail) | Video analysis | n/a | n/a | Niche |

### Adjacent high-star repos that surface for "instagram mcp" (not IG-account servers)

| Repo | Stars | Notes |
|---|---|---|
| [gyoridavid/short-video-maker](https://github.com/gyoridavid/short-video-maker) | 1,448 | MCP + REST for generating Reels/Shorts videos (Remotion); does not post to IG |
| [pipeboard-co/meta-ads-mcp](https://github.com/pipeboard-co/meta-ads-mcp) | 1,342 | Meta Ads (FB/IG ads) MCP; hosted remote at `meta-ads.mcp.pipeboard.co` (42 tools); license **Business Source License 1.1** (not OSI open source); Pipeboard is a badged Meta Business Partner per README |
| [trypostit/trypost](https://github.com/trypostit/trypost) | 783 | Open-source PHP/Laravel social scheduler with MCP; multi-network incl. Instagram |
| [matiasbattocchia/open-bsp-api](https://github.com/matiasbattocchia/open-bsp-api) | 623 | WhatsApp + Instagram + TikTok business platform with MCP |
| [everyinfra/everyinfra-agent-plugins](https://github.com/everyinfra/everyinfra-agent-plugins) | 159 | Paid scraper API MCP/plugin (TikTok, IG, etc.) for Claude Code |
| [Sharan-Kumar-R/Custom-MCP-Server](https://github.com/Sharan-Kumar-R/Custom-MCP-Server) | 98 | Scrapes LinkedIn/FB/IG profiles via RapidAPI |
| [mikusnuz/meta-ads-mcp](https://github.com/mikusnuz/meta-ads-mcp) | 91 | Marketing API v25, 135 tools |
| [EfrainTorres/armavita-meta-ads-mcp](https://github.com/EfrainTorres/armavita-meta-ads-mcp) | 79 | Rust, Marketing API v26, token redaction |
| [socialclaw](https://github.com/ndesv21/socialclaw), [pendpost](https://github.com/pendpost/pendpost), [Chatway MCP](https://github.com/Chatway-app/chatway-mcp-server), [XPOZ MCP](https://github.com/XPOZpublic/xpoz-mcp), [stormy-cookbook](https://github.com/OneInterface/stormy-cookbook) | 13–103 | Schedulers / social-data APIs exposing IG via their own backend |
| [guimatheus92/mcp-video-analyzer](https://github.com/guimatheus92/mcp-video-analyzer), [siemd2/reel-relay](https://github.com/siemd2/reel-relay), [Overusedhydra/reels-vault](https://github.com/Overusedhydra/reels-vault) | 10–107 | Reel download (yt-dlp) + transcription for Claude |

### Cited Findings
- GitHub search "instagram mcp" returns 786 repos; the top-starred dedicated Instagram account server is jlbadano/ig-mcp at 203 stars, followed by trypeggy/instagram_dm_mcp at 187. — [GitHub search results via API](https://github.com/search?q=instagram+mcp&type=repositories&s=stars); [jlbadano/ig-mcp](https://github.com/jlbadano/ig-mcp); [trypeggy/instagram_dm_mcp](https://github.com/trypeggy/instagram_dm_mcp)
- jlbadano/ig-mcp uses the Instagram Graph API with a long-lived token. Its DM features "require Advanced Access approval from Meta". — [jlbadano/ig-mcp README](https://github.com/jlbadano/ig-mcp)
- trypeggy/instagram_dm_mcp pins `instagrapi==2.1.5` in requirements.txt. Its README configures `INSTAGRAM_PASSWORD` / `--password` and creates `username_session.json` session files automatically. — [trypeggy/instagram_dm_mcp](https://github.com/trypeggy/instagram_dm_mcp)
- mikusnuz/meta-mcp: "66 tools across Instagram (33), Threads (27), and Meta platform (6)", Graph API v26.0. — [mikusnuz/meta-mcp](https://github.com/mikusnuz/meta-mcp)
- adelaidasofia/instagram-mcp: 29 tools. It stores tokens in the macOS keychain, and every result and error "passes a scrubber that strips access tokens". DM tools need `instagram_manage_messages`, which Meta grants "only through App Review (typically weeks, and stricter in 2025–2026)". — [adelaidasofia/instagram-mcp](https://github.com/adelaidasofia/instagram-mcp)
- oliverames/meta-mcp-server advertises 200 tools across Pages, Instagram, Threads, Ads, Commerce and CAPI with a single `META_ACCESS_TOKEN`. — [oliverames/meta-mcp-server](https://github.com/oliverames/meta-mcp-server)
- Bob-lance/instagram-engagement-mcp and arjun1194/insta-mcp depend on the `instagram-private-api` npm package and take username/password. Bob-lance's README says it "uses the Instagram Private API, which is not officially supported by Instagram". — [Bob-lance](https://github.com/Bob-lance/instagram-engagement-mcp); [arjun1194](https://github.com/arjun1194/insta-mcp)
- duhlink/instagram-server-next-mcp depends on puppeteer and playwright and reuses Chrome's login session via `CHROME_USER_DATA_DIR`. — [duhlink/instagram-server-next-mcp](https://github.com/duhlink/instagram-server-next-mcp)
- braindead-dev/instagram-dms-mcp requires the `sessionid` and `csrftoken` cookies copied from DevTools and offers a Render deploy button. — [braindead-dev/instagram-dms-mcp](https://github.com/braindead-dev/instagram-dms-mcp)
- inssist/mcp works "inside your own logged-in Instagram session, through the INSSIST Chrome extension". It claims that "every other Instagram MCP wraps the Graph API: business accounts only, no Stories, no music". — [inssist/mcp](https://github.com/inssist/mcp)
- lupikovoleg/instagram-cli is "powered by HikerAPI, OpenRouter, and FastMCP" and requires `HIKERAPI_KEY`. — [lupikovoleg/instagram-cli](https://github.com/lupikovoleg/instagram-cli)
- HasData/instagram-mcp is a hosted, read-only server for public profile, posts and comments data. — [HasData/instagram-mcp](https://github.com/HasData/instagram-mcp)
- pipeboard-co/meta-ads-mcp is licensed under Business Source License 1.1 and offers a hosted remote MCP with 42 Meta Ads tools. — [pipeboard-co/meta-ads-mcp](https://github.com/pipeboard-co/meta-ads-mcp)
- Meta runs an official **Ads** MCP server at `https://mcp.facebook.com/ads`, which a community skill connects with `claude mcp add --transport http meta-ads https://mcp.facebook.com/ads`. — [sepivip/meta-ads-skill](https://github.com/sepivip/meta-ads-skill). Third-party guides date it to 2026-04-29 and say it does not cover organic posting, comments, DMs or insights — [mcp.directory guide](https://mcp.directory/blog/meta-ads-mcp-complete-guide-2026); [adspirer blog](https://www.adspirer.com/blog/meta-ads-mcp)
- Whether Meta has an official organic Instagram MCP is unclear. A search summary of Meta's developer docs mentions official remote MCP servers covering Facebook, Instagram, WhatsApp and Ads ([developers.facebook.com/documentation/mcp](https://developers.facebook.com/documentation/mcp)). A third-party guide says no official MCP exists for IG organic posting ([usecarly blog](https://www.usecarly.com/blog/instagram-mcp/)). I could not fetch the Meta page to verify.

### Inferences
- Popularity is low and fragmented: no dedicated Instagram MCP server has crossed ~200 stars, while Meta Ads MCPs and multi-network schedulers attract more attention. The ecosystem is young; most repos were created in 2025–2026.
- Choice of API sorts the repos into two groups. Graph API servers are ToS-compliant but need a Business/Creator account, a Meta app, and App Review for DMs. Private-API and cookie servers work on any account but put the account at risk.
- The best-maintained options appear to be mikusnuz/meta-mcp (frequent version bumps tracking Graph API v25→v26), adelaidasofia/instagram-mcp (security features) and jlbadano/ig-mcp (most stars).

### Gaps
- Exact `pushed_at` (last commit) dates were not retrieved because GitHub REST search was blocked, and `updated_at` may reflect star activity rather than commits.
- Licenses for duhlink, arjun1194, braindead-dev, openinstaflow and lupikovoleg: no root `LICENSE` file was found, so they may be unlicensed.
- Meta's official MCP docs page could not be fetched (developers.facebook.com is blocked in this session).

## Which Claude Code skills / plugins / subagents target Instagram?

### Takeaway
Claude skills for Instagram are now more popular than Instagram MCP servers. Several skill packs have hundreds to thousands of stars, but most only write or plan content (captions, Reels scripts, carousels) and do not touch the API. Skills that do publish usually delegate to an MCP server: the official Graph API, or a vendor such as Publora, PostZen or Composio.

### Census table — skills/plugins

| Repo | Stars | Last activity | What it is | Posts to IG? / how | License |
|---|---|---|---|---|---|
| [Jakeschincariol/instagram-agent-skill](https://github.com/Jakeschincariol/instagram-agent-skill) | 3,844 | 2026-10-30 (created 2026-09) | 13 Claude skills (/ig-reel, /ig-caption, /ig-dm, /ig-comment, /ig-viral…) + 5 Python tools (hook scorer, caption linter, "slop" detector) | **No.** README: "These skills do not post to Instagram"; the author argues that browser automation and third-party tools violate IG Terms | MIT |
| [postzen-dev/instagram-agent-skill](https://github.com/postzen-dev/instagram-agent-skill) | 31 | 2026-10-30 | Fork-like 14-skill version + Claude Code plugin (`/plugin marketplace add postzen-dev/instagram-agent-skill`) | Yes, via hosted PostZen MCP (`https://mcp.postzen.dev/mcp`, OAuth). The PostZen connect page **takes the IG username and password** | MIT (same author copyright) |
| [ScrapeCreators/social-media-research-skills](https://github.com/ScrapeCreators/social-media-research-skills) | 5,127 | 2026-10-30 | Research skills (outliers, comment mining, ad libraries) across TikTok/IG/YouTube… | Read-only via ScrapeCreators paid scraping API | n/a |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | 65,985 | 2026-10-30 | General research skill whose sources include Instagram | Read-only | n/a |
| [Hao0321/claude-skill-social-post](https://github.com/Hao0321/claude-skill-social-post) | 745 | 2026-10-30 | Learns FB voice; auto-posts to FB/IG/Threads/X | Yes, via **Chrome MCP browser automation** (topic `chrome-mcp`) | n/a |
| [sergebulaev/instagram-skills](https://github.com/sergebulaev/instagram-skills) | 672 | 2026-10-30 | Captions, carousels, hooks, hashtags, weekly plan | Publishes via Publora MCP | MIT (per description) |
| [Ootto-AI/claude-content-skills](https://github.com/Ootto-AI/claude-content-skills) | 329 | 2026-10-30 | Reels content-factory skills | Content only | n/a |
| [social-media-skills/skills](https://github.com/social-media-skills/skills) | 218 | 2026-10-30 | 106 social media skills | Mixed | n/a |
| [publora/skills](https://github.com/publora/skills) | 61 | 2026-10-28 | 9 SKILL.md for Publora MCP (multi-network posting incl. IG) | Yes, via Publora hosted MCP | MIT |
| [nicojunk/claude-ig](https://github.com/nicojunk/claude-ig) | 20 | 2026-10-28 | 13 sub-skills, 6 agents, 100-point content scoring | Content engine | n/a |
| [moboutrig/instagram-claude-skill](https://github.com/moboutrig/instagram-claude-skill) | 14 | 2026-10-25 | Skill wrapping Graph API v25 scripts: publish image/video/reel/story/carousel, insights, DMs, token validation | Yes, official Graph API (token) | none found |
| [YSY-99/meta-ads-api-field-guide](https://github.com/YSY-99/meta-ads-api-field-guide) | 16 | 2026-09-13 | Skill + 3 subagents + safety hooks for Meta Ads | Ads via Marketing API | n/a |
| [sepivip/meta-ads-skill](https://github.com/sepivip/meta-ads-skill) | 14 | 2026-10-02 | Skill for Meta's official Ads MCP (`mcp.facebook.com/ads`) | Ads only | n/a |
| [JayceBatallones/instagram-reel-extractor](https://github.com/JayceBatallones/instagram-reel-extractor) | 13 | 2026-10-01 | Extracts transcript, music, comments, frames from Reels | Read/scrape | n/a |
| Carousel/Reel makers: [threads-carousel-claude-skill](https://github.com/itchernetski/threads-carousel-claude-skill) (119), [instagram-thread-carousel](https://github.com/Samin12/instagram-thread-carousel) (81), [remotion-ads](https://github.com/Maartenlouis/remotion-ads) (64), [carousel-builder](https://github.com/charlesdove977/carousel-builder) (47), [video-edit-skill](https://github.com/tenfoldmarc/video-edit-skill) (110) | 47–119 | 2026 | Asset generation | No | various |

Code search found 4,376 `SKILL.md` files under `.claude/skills/` mentioning Instagram, mostly inside personal or agency workspaces. Examples: `.claude/skills/instagram-dm/SKILL.md` in Boonanpro/done, `.claude/skills/instagram-api/SKILL.md` in olivenet-iot/olivenet-social-bot, `.claude/skills/instagram-poster/SKILL.md` in metachemist/Full-Time-Employee, `.claude/skills/meta-instagram/SKILL.md` in tg12/aw-cloudless. — [GitHub code search](https://github.com/search?q=instagram+filename%3ASKILL.md+path%3A.claude%2Fskills&type=code)

### Cited Findings
- Jakeschincariol/instagram-agent-skill (3,844★, MIT) says: "These skills do not post to Instagram… Everything else people use to automate posting, commenting, following or DMing is browser automation or a third-party tool, and both violate Instagram's Terms of Use". It also says `/ig-viral` "never asks for your password". — [README](https://github.com/Jakeschincariol/instagram-agent-skill)
- The PostZen variant installs as a Claude Code plugin that registers the PostZen MCP (`claude mcp add --transport http postzen https://mcp.postzen.dev/mcp`). Its README says the connect page "takes your Instagram username and password and does not offer 'Log in with Facebook'". — [postzen-dev/instagram-agent-skill](https://github.com/postzen-dev/instagram-agent-skill)
- moboutrig/instagram-claude-skill covers publishing (image/video/reel/story/carousel), insights and DMs via the official Graph API v25.0. — [README](https://github.com/moboutrig/instagram-claude-skill)
- Ootto-AI's autopilot README tells users to connect Instagram through Composio's MCP directory (OAuth, Business/Creator) so "Claude can post reels, reply to comments, and send DMs". — [Ootto-AI/claude-instagram-autopilot README (read from repo)](https://github.com/Ootto-AI/claude-instagram-autopilot)
- Hao0321/claude-skill-social-post auto-posts to FB/IG/Threads/X and is tagged `chrome-mcp`, which points to browser automation. — [repo](https://github.com/Hao0321/claude-skill-social-post)

### Inferences
- The most-starred "Instagram + Claude" assets are content-craft skills, not integrations. The integration layer is commonly outsourced to a hosted MCP (Publora, PostZen, Composio, Pipeboard), which moves credential custody to a third party.
- Even a skill pack that is careful about ToS can, once it gains a vendor publishing add-on, end up with a password-based connect flow (the PostZen case).

### Gaps
- Star counts for the 3–5k-star skill repos grew very quickly (created Jun–Sep 2026). Whether they are organic was not assessed.
- License of several skill repos was not checked individually.

## Notable awesome-list entries for Instagram

### Takeaway
punkpeye/awesome-mcp-servers lists about 35 Instagram-related entries, mostly schedulers and data APIs plus a few dedicated IG servers. wong2/awesome-mcp-servers lists only the trypeggy DM server and Pipeboard Meta Ads. appcypher/awesome-mcp-servers has no Instagram entries.

### Cited Findings
- punkpeye/awesome-mcp-servers Instagram-related entries include HasData/instagram-mcp, arjun1194/insta-mcp, mikusnuz/meta-mcp, mikusnuz/meta-ads-mcp, drashrafsaiyed-cyber/instagram-mcp, farukkolip/instapdown-mcp, afanasenkoa/instavision-mcp, pjpoulose/PIL (saved posts), and schedulers such as publora/mcp-server, Upload-Post/upload-post-mcp, postfast-mcp, posteverywhere/mcp, pendpost, adaptlypost/agent, taisly/agent, solnk-mcp, tokportal-mcp, SocialAPIsHub/mcp-server and socialintel-mcp. — [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)
- wong2/awesome-mcp-servers lists "Instagram DMs (trypeggy/instagram_dm_mcp) — Send Instagram DMs via your LLM" and "Meta Ads Remote MCP (pipeboard-co/meta-ads-mcp)". — [wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers)
- A grep of appcypher/awesome-mcp-servers found no "instagram" matches. — [appcypher/awesome-mcp-servers](https://github.com/appcypher/awesome-mcp-servers)

### Inferences
- Awesome-list inclusion skews toward commercial hosted "post everywhere" MCPs, which outnumber self-hosted IG-specific servers.

### Gaps
- Glama/Smithery/mcp.so registry listings and their quality scores were not examined.

## Security / quality observations (passwords, session cookies, ToS risk)

### Takeaway
About half the dedicated IG MCP servers ask for the raw Instagram password or session cookies and keep them in plaintext env/config or session files. They use unofficial clients (instagrapi, instagram-private-api) or browser sessions, which go against Instagram's Terms and risk challenges or bans. Graph API servers avoid this but need Professional accounts, Meta apps, 60-day tokens and App Review for DMs. Only a few, such as adelaidasofia/instagram-mcp and armavita-meta-ads-mcp, implement token redaction.

### Cited Findings
- Plaintext password in MCP client config: trypeggy (`--password {{YOUR_INSTAGRAM_PASSWORD}}`), Bob-lance (`"INSTAGRAM_PASSWORD": "your_instagram_password"`) and arjun1194 (`INSTAGRAM_PASSWORD`, sessions in `./data`). — [trypeggy](https://github.com/trypeggy/instagram_dm_mcp); [Bob-lance](https://github.com/Bob-lance/instagram-engagement-mcp); [arjun1194](https://github.com/arjun1194/insta-mcp)
- Session cookie exfiltration pattern: braindead-dev asks users to copy `sessionid`/`csrftoken` from DevTools into env vars and deploy to Render. — [braindead-dev/instagram-dms-mcp](https://github.com/braindead-dev/instagram-dms-mcp)
- Full Chrome profile access: duhlink points the server at the Chrome user-data dir. — [duhlink](https://github.com/duhlink/instagram-server-next-mcp)
- adelaidasofia/instagram-mcp states that most IG automation tools "wrap the unofficial private API (username + password) — which violates Instagram's Terms and risks a ban". It mitigates with keychain storage, output scrubbing of `EAA…`/`IGQV…` tokens, and an audit log. — [adelaidasofia/instagram-mcp](https://github.com/adelaidasofia/instagram-mcp)
- Graph API constraints cited across repos: Business/Creator accounts only; DMs need `instagram_manage_messages` Advanced Access through App Review; publishing needs public HTTPS media URLs. — [adelaidasofia](https://github.com/adelaidasofia/instagram-mcp); [openinstaflow](https://github.com/Narla-Venkata-Anand-Sai-Kumar/openinstaflow); [jlbadano](https://github.com/jlbadano/ig-mcp)
- IG Harness warns that handing the MCP an owner/admin key grants DM sending and broadcast rights, and offers `IG_HARNESS_READ_ONLY=true`. — [Shudesu/ig-harness-oss](https://github.com/Shudesu/ig-harness-oss)
- Third-party hosted MCPs (PostZen, Publora, HasData, HikerAPI, Composio, Pipeboard) put the account credential or OAuth grant with the vendor. PostZen's connect flow collects the IG password. — [postzen-dev/instagram-agent-skill](https://github.com/postzen-dev/instagram-agent-skill); [lupikovoleg/instagram-cli](https://github.com/lupikovoleg/instagram-cli)
- Prompt-injection surface: DM and comment tools feed untrusted user-generated text into the model while send/publish tools are also exposed. Several servers expose both in one tool set: arjun1194 (read + send DMs, like/comment), trypeggy and inssist. — [arjun1194](https://github.com/arjun1194/insta-mcp); [inssist/mcp](https://github.com/inssist/mcp)

### Inferences
- For a production Claude–Instagram integration, the low-risk path is a Graph API MCP with scoped tokens and a read-only mode, or a human approval gate before publish/DM. Private-API MCPs suit only throwaway or personal experimentation.
- Many small repos lack LICENSE files, tests and releases; maturity is generally "hobby/early" apart from vendor-backed repos (Pipeboard, HasData, inssist, Publora).

### Gaps
- I did not audit code, so it is not verified whether password-based servers log credentials or whether token scrubbing works as claimed.
- No reported ban incidents linked to specific MCP repos were found. GitHub issue trackers were not searched for "challenge_required" or ban reports.
