---
layout: default
title: "Horizon Summary: 2026-11-17 (EN)"
date: 2026-11-17
lang: en
---

> From 17 items, 12 important content pieces were selected

---

**Technology News**
1. [vLLM v0.34.0 makes extensible KV cache default, drops Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI announces GPT-6.2 Astra and Sol](#item-tech-news-2) ⭐️ 8.0/10
3. [Optimizely reportedly compromised to serve malware via Zoom, GitLab](#item-tech-news-3) ⭐️ 8.0/10
4. [Datasette Lite rewritten to run full Datasette in browser via service workers](#item-tech-news-4) ⭐️ 8.0/10
5. [Carnegie Mellon launches free CS Learn lecture archive on YouTube](#item-tech-news-5) ⭐️ 7.0/10
6. [Reports: NSA&\#x27;s Highly Classified Communications Network Is Down](#item-tech-news-6) ⭐️ 6.0/10
7. [FrontierHarness Eval v1.1 compares AI agent harness and model pairings](#item-tech-news-7) ⭐️ 6.0/10
8. [Essay Argues for Better Open Source, Not More Apps](#item-tech-news-8) ⭐️ 6.0/10
9. [Claude Code verification advice draws cost and reliability pushback](#item-tech-news-9) ⭐️ 6.0/10
10. [Hacker News discusses why 3dfx cards produced washed-out colors](#item-tech-news-10) ⭐️ 6.0/10
11. [Apple explains macOS Full Disk Access and System and App Protection override](#item-tech-news-11) ⭐️ 6.0/10
12. [LLM 0.37.3 fixes logging breakage from SQLite 3.54.1](#item-tech-news-12) ⭐️ 5.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 makes extensible KV cache default, drops Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM v0.34.0 makes extensible KV cache sizing the default on CUDA and ROCm, sizing the cache from memory free after warmup rather than an estimate; the release notes say this yields a larger cache and higher throughput for most models, with possible per-token decode latency increases of 6–18% on some H200 models at concurrency 128. The release removes Model Runner V1, so setting VLLM\_USE\_V2\_MODEL\_RUNNER=0 now fails at startup and V1 logits processors must be ported. It adds 10 models, including Mistral Large 4 and Nemotron-3.5-Transcribe, and reports speedups up to 1.95× decode for Step5 on 4×GB200 and 1.6× output throughput for GLM-5.3-Flash. Upgraders must also account for the default block size changing from 16 to 64, ROCm 7.2 artifacts being dropped in favor of ROCm 10.0, and a new requirement for huggingface\_hub &gt;= 2.0.0.

github · khluu · Nov 16, 23:22

**「Background」** vLLM is an open-source engine for serving large language models, and its GPU Model Runner is the execution path that performs model forward passes. The KV cache stores attention state across generation steps, so the amount of GPU memory allocated to it affects how many tokens can be served concurrently; the block size controls the granularity of that cache allocation.

**「Impact」** Teams deploying vLLM should test with --block-size 16, --gpu-memory-utilization 0.9, or --no-enable-extensible-kv-cache if they need the prior defaults, and must remove the V1 runner flag and update dependencies before upgrading; fp\_quant checkpoints no longer load, and Marlin W4A8 configurations require --quantization humming with VLLM\_HUMMING\_INPUT\_QUANT\_CONFIG.

**Tags**: `#vLLM`, `#LLM inference`, `#open source`, `#performance`, `#breaking changes`

---

<a id="item-tech-news-2"></a>
### [OpenAI announces GPT-6.2 Astra and Sol](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 8.0/10

OpenAI published a release page titled &quot;Introducing GPT-6.2 Astra and Sol,&quot; indicating a new GPT-6.2 generation that adds a model called Astra alongside an updated Sol. The supplied material contains no release-page text, so benchmark figures, pricing, context limits, availability dates, and API or product compatibility for either model remain unconfirmed here. Commenters treat Sol as a model they already use in production and discuss the new version mostly through cost-versus-benchmark tradeoffs and comparisons with rival models such as Fable 5.2, Opus 5.5 and Gemini 4 Carbon.

hackernews · jasondavies · Nov 17, 17:46 · [Discussion](https://news.ycombinator.com/item?id=50535230)

**「What the source does and does not establish」** The item supplies only the announcement title and URL — no model card, benchmark table, pricing, context window, or availability details — so the specific capabilities of GPT-6.2 Astra and Sol cannot be verified from the source itself. Hacker News commenters treat &quot;Sol&quot; as a model already in production use \(one calling it their &quot;workhorse on company account&quot;\) and refer back to earlier variants such as GPT-5.6 Sol and &quot;Luna,&quot; which suggests an iteration within an established model family rather than a first-generation launch — but those references come from commenters, not from OpenAI documentation.

**「Impact」** Because no pricing, availability, deprecation timeline for earlier Sol versions, or benchmark methodology was captured in the supplied material, teams cannot yet judge whether moving to GPT-6.2 is worthwhile from the announcement alone; the practical step is to re-run their own evaluations on the tasks they actually use rather than rely on vendor benchmark figures.

**「Community Discussion」** Several commenters called the performance impressive relative to cost &quot;if those benchmarks hold up,&quot; while questioning whether familiar tests like the pelican benchmark are still useful and asking for quick real-world comparisons against Fable 5.2 and Opus 5.5. One commenter reported that OpenAI&\#x27;s published slideshow, workbook and memo examples looked worse than output they had gotten from GPT-5.6 Sol shortly before, and another said they were waiting for a new Luna, crediting the earlier Luna with ending what they called &quot;Tokenpocalypse.&quot;

**Tags**: `#OpenAI`, `#GPT-6.2`, `#large language models`, `#AI benchmarks`, `#model release`

---

<a id="item-tech-news-3"></a>
### [Optimizely reportedly compromised to serve malware via Zoom, GitLab](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/) ⭐️ 8.0/10

Optimizely, a third-party experimentation and A/B testing script embedded across many large websites, was reportedly compromised and used to deliver malware through pages including Zoom and GitLab. The report frames the incident as a third-party script supply-chain problem: sites that load vendor JavaScript inherit the vendor&\#x27;s security failures. The account available so far gives no technical specifics — no affected script versions, injection mechanism, time window, or confirmed victim count — and neither Optimizely nor the named sites have confirmed details in the supplied material. Independent verification of the scope is therefore still outstanding.

hackernews · kristjansson · Nov 16, 23:00 · [Discussion](https://news.ycombinator.com/item?id=50524767)

**「Background」** Optimizely supplies JavaScript snippets that customer sites embed, so code carried in the vendor&\#x27;s bundles can run on every participating domain. Reporting on the incident describes attacker JavaScript injected into Optimizely bundles rather than CDN cache poisoning, and says Optimizely&\#x27;s own www and login sites also carried the malicious code.

**「Third-party script exposure」** Because the malicious JavaScript was planted inside Optimizely Web, every site that embedded the vendor&\#x27;s script inherited the exposure; reporting cited by the search results says the code reached visitors of 178 organizations. Site operators should treat Optimizely as a compromised dependency and audit or temporarily remove its script rather than assuming the vendor&\#x27;s release controls contained the incident.

**「Community Discussion」** Commenters blamed the tag-manager model that lets marketing add scripts without engineering review, with one arguing the practice produced bloated JavaScript on news sites and hoping teams re-evaluate it now. Others called for vendor accountability — phased rollouts, security checks, and cooldowns at Optimizely — and argued large sites should vendor or self-host such code, while one reader asked whether the compromise persisted beyond a browser session and whether uBlock Origin would have blocked it; no one in the thread answered that.

<details><summary>References</summary>
<ul>
<li><a href="https://news.ycombinator.com/item?id=50524767">Optimizely compromised , served malware on Zoom , GitLab</a></li>
<li><a href="https://amirulcyber.com/2026/11/16/optimjack-optimizely-skimmer/">CNN, Zoom , Fox News Served Visitors... | Amirul Cyber</a></li>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal Credit...</a></li>

</ul>
</details>

**Tags**: `#supply-chain-security`, `#third-party-scripts`, `#web-security`, `#malware`, `#optimizely`

---

<a id="item-tech-news-4"></a>
### [Datasette Lite rewritten to run full Datasette in browser via service workers](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison released a complete rewrite of Datasette Lite that runs the full Datasette Python application in the browser using service workers and Pyodide. Through crafted URLs to lite.datasette.io, users can load SQLite databases, JSON files, CSV files, or SQL scripts; choose a released Datasette version from PyPI or a GitHub commit, tag, or branch; select from over 100 SQLite versions; and install plugins from PyPI or wheel URLs, including JavaScript visualization tools. Data URLs must have open CORS headers, and Willison demonstrates the setup with the datasette-maplibre plugin displaying country GeoJSON data on maps.

rss · Simon Willison · Nov 17, 16:48

**「Earlier Datasette Lite」** Datasette Lite first launched in 2022 as a way to run the Datasette Python application in the browser through Pyodide and WebAssembly. That version relied on a Pyodide web worker to simulate requests and then injected the resulting HTML into the top-level page with innerHTML, so JavaScript-dependent features failed because script tags inserted that way do not execute.

**「Impact」** Developers can now link to reproducible Datasette demos pinned to a specific Datasette version or commit, SQLite version, data file, and plugin set without running a server. Willison is already using this in Datasette issue reports to show an old pagination bug and the fixed behavior side by side.

**Tags**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#service workers`, `#SQLite`

---

<a id="item-tech-news-5"></a>
### [Carnegie Mellon launches free CS Learn lecture archive on YouTube](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

Carnegie Mellon has launched CS Learn, a free open-courseware project that publishes full-semester lectures from current CMU computer science courses on YouTube. Organizer Phillip Compeau said one course premieres each day during launch week, with more courses to follow in January, and that students built tools to automate much of the production work. The release provides lecture videos rather than a new degree or credential program.

hackernews · pcompeau · Nov 16, 20:43 · [Discussion](https://news.ycombinator.com/item?id=50522980)

**「Open courseware&\#x27;s long precedent」** Free lecture publishing has a long lineage: in the discussion thread, Phillip Compeau, the CMU faculty member running CS Learn, conceded that &quot;MIT got here 25 years ago,&quot; referring to MIT&\#x27;s earlier open courseware publishing. He framed CS Learn&\#x27;s distinction not as being first, but as the student-built automation that lets a small team produce full-semester lecture videos.

**「Impact」** Learners can watch complete CMU course lectures without enrolling, but the rollout is sequential—one course per day in launch week and more promised for January—so the catalog is not complete at launch.

**「Community discussion」** Commenters debated whether fundamentals still matter in the age of AI, with one arguing that learning them properly makes AI a “power tool” rather than a replacement. A viewer also reported production problems in a “Principles of Computing” lecture, saying a single middle-of-room microphone left the professor’s voice inaudible for most of a minute when she stepped away; that is one viewer’s report, not a verified assessment of the whole catalog.

**Tags**: `#open courseware`, `#computer science education`, `#Carnegie Mellon`, `#YouTube`, `#free online courses`

---

<a id="item-tech-news-6"></a>
### [Reports: NSA&\#x27;s Highly Classified Communications Network Is Down](https://www.reuters.com/technology/highly-classified-us-national-security-communications-network-is-down-cnn-2026-11-17/) ⭐️ 6.0/10

Reports attributed by Reuters to CNN say a highly classified U.S. national security communications network is down, described in the item as an NSA internal network outage. The available account provides no cause, scope, affected systems, or restoration timeline. It also does not include the underlying CNN report or any NSA confirmation, so the disclosure and operational details remain unverified.

hackernews · nodoodles · Nov 17, 15:50 · [Discussion](https://news.ycombinator.com/item?id=50533089)

**「Background」** The National Security Agency/Central Security Service describes its mission as leading U.S. government cryptology across foreign signals intelligence and cybersecurity. Its classified internal communications are distinct from public-facing networks, and the supplied reporting does not describe the affected systems or a cause.

**「Consequence for NSA staff」** With NSA Net unavailable, agency employees lose the internal channel they use to pass classified information among themselves, according to CNN&\#x27;s reporting, which cites six people familiar with the matter. The accounts do not specify the outage&\#x27;s cause, how long it has lasted, or when service is expected to resume, so the operational effect beyond internal classified messaging is unknown.

**「Community Discussion」** Commenters questioned why the NSA would publicly announce that a highly classified internal network was down before restoring it, and debated whether an apparent cluster of outages reflects a real increase in failures or heightened attention. Others speculated about state-level or AI-enabled cyberattacks, but no one offered evidence for a common cause.

<details><summary>References</summary>
<ul>
<li><a href="https://www.nsa.gov/">National Security Agency | Central Security Service</a></li>
<li><a href="https://www.cnn.com/2026/11/17/politics/highly-classified-national-security-communications-network-goes-down">Exclusive: Highly classified US national security communications ...</a></li>

</ul>
</details>

**Tags**: `#cybersecurity`, `#network-outage`, `#national-security`, `#NSA`, `#incident-reporting`

---

<a id="item-tech-news-7"></a>
### [FrontierHarness Eval v1.1 compares AI agent harness and model pairings](https://runta.com/blog/introducing-frontierharness-eval-v1-1/) ⭐️ 6.0/10

FrontierHarness Eval v1.1 is a newly introduced benchmark for comparing AI agent harness/model combinations on terminal-bench tasks, aimed at developers choosing coding-agent setups. The supplied material does not provide the exact model list, run count, or independent verification of the results. Commenters disputed the framing, including a reported figure that 64% of spending went to tasks that did not pass the benchmark&\#x27;s verifiers. The post is an evaluation proposal rather than an established ranking.

hackernews · Edward40 · Nov 17, 14:53 · [Discussion](https://news.ycombinator.com/item?id=50532191)

**「Background」** An agent harness is the scaffolding around a model — tool definitions, prompts, and the execution loop — that turns model output into actions, so the same model can behave differently depending on the harness wrapped around it. FrontierHarness Eval is a public leaderboard that runs these combinations across 21 coding-agent harnesses, 5 models, and 62 tasks, reporting pass rate, cost, and speed for each pairing; v1.1 is the version of that evaluation discussed here.

**「Impact」** Developers should read any result as specific to the harness/model pairing and task set, not as a general model ranking; the supplied material does not show that a winning pairing transfers to other terminal tasks.

**「Community discussion」** Commenters criticized the headline as confusing and argued that the best harness depends on the problem; one said that for their domain-specific workflows, supplying the right tools mattered more than the choice of model. Another clarified that “failed” meant not meeting all pass criteria on a benchmark task, not a runtime failure.

<details><summary>References</summary>
<ul>
<li><a href="https://frontierharness.org/">FrontierHarness Eval: AI coding agent harness benchmark</a></li>

</ul>
</details>

**Tags**: `#AI agents`, `#benchmarking`, `#LLM evaluation`, `#coding agents`, `#developer tooling`

---

<a id="item-tech-news-8"></a>
### [Essay Argues for Better Open Source, Not More Apps](https://jordankrueger.com/blog/better-open-source-not-more-apps/) ⭐️ 6.0/10

Nothing shipped or changed: an essay published on jordankrueger.com, “We don’t need more apps. We need better open source,” argues that users and maintainers should invest in improving existing open-source tools instead of producing more applications. The item is an opinion argument, not a release, version announcement, or independently measured result. The supplied source contains no full text, so the essay’s specific evidence and proposals cannot be verified beyond its title and short summary.

hackernews · pandemicsoul · Nov 17, 14:45 · [Discussion](https://news.ycombinator.com/item?id=50532086)

**「Context」** Open-source tools are frequently maintained by small, often volunteer teams, so the real cost of a change is measured in maintainer review time rather than in writing the initial code. The essay&\#x27;s premise — that effort should go into improving tools people already depend on rather than shipping new apps — rests on that constraint, which the accompanying discussion treats as a familiar bottleneck rather than a hypothetical one.

**「Impact」** For developers who want to improve an existing tool, the thread’s reports indicate that contribution capacity—not the number of apps—is the binding constraint: maintainers described unsolicited PRs arriving faster than they can review them, and one contributor said AI-assisted fixes were rejected under a planned no-AI policy. That makes maintainer coordination a precondition for the essay’s suggested weekend fix.

**「Community discussion」** Commenters disagreed about where the problem lies: one described hours lost trying to get a MIDI keyboard, DAW, and VST plugin working and called for a new software-delivery model, while another said a Google spreadsheet wrapped by a GrokBot had obsoleted many dedicated apps for food logging. A maintainer pushed back on easy fixes, saying unsolicited PRs for minor annoyances and hypotheticals now consume time they do not have.

**Tags**: `#open source`, `#software maintenance`, `#maintainer burnout`, `#AI contributions`, `#software usability`

---

<a id="item-tech-news-9"></a>
### [Claude Code verification advice draws cost and reliability pushback](https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/) ⭐️ 6.0/10

A Claude Code team blog post on verification practices drew a Hacker News debate over whether its token-intensive workflows are practical. One commenter characterized the post as assuming unlimited tokens, citing a section that describes per-change checks through skill files and asking Claude to use the chrome-for-Claude tool, and argued that Playwright could catch the same regressions without token spend. Others questioned Claude Code&\#x27;s current reliability and the cost of running agents at the scale the post discusses. The item announces no new product or independently measured result; the dispute is over workflow guidance and its operating cost.

hackernews · craigmart · Nov 17, 10:20 · [Discussion](https://news.ycombinator.com/item?id=50529612)

**「Prior context」** The post follows an earlier Anthropic write-up on how code review works inside the Claude Code team, where roughly 90% of the team&\#x27;s code is written and reviewed by Claude. This article shifts from review to verification — actually running the change — covering end-to-end, property, and differential tests and how the team tries to keep its automated verifiers honest.

**「Impact」** The thread&\#x27;s concrete concern is cost: one commenter reported spending about $2,000 per month on tokens with just one or two agents and questioned the post&\#x27;s suggestion, as quoted in the thread, that users can run dozens or hundreds in parallel. Another argued that regression checks could be handled by Playwright without token spend, so teams evaluating the described verification loop may compare it against deterministic browser automation before adopting per-change AI checks.

**「Community Discussion」** Commenters split between cost skepticism and reliability concerns: one called the practices expensive where near-free tooling would produce equal or better results, while another asked whether Claude Code has become reliable after a heavy, janky experience roughly nine months earlier with regular bugs and breaking UI changes. A further commenter dismissed Anthropic&\#x27;s teams outright, an opinion stated without specific supporting evidence in the thread.

<details><summary>References</summary>
<ul>
<li><a href="https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/">How the Claude Code team thinks about verification</a></li>
<li><a href="https://t.me/aisferaic/1270">AI для каждого | AISferaic – Telegram</a></li>

</ul>
</details>

**Tags**: `#Claude Code`, `#AI coding agents`, `#software verification`, `#developer tooling`, `#LLM costs`

---

<a id="item-tech-news-10"></a>
### [Hacker News discusses why 3dfx cards produced washed-out colors](https://twitter.com/id_aa_carmack/status/2122478083319992513) ⭐️ 6.0/10

A Hacker News thread examines why 3dfx graphics cards produced washed-out color output, with discussion centered on analog VGA signal-voltage standards and how sRGB values map to CRT signal voltage. Commenters describe early Voodoo cards as video switchers that selected between 2D passthrough and the 3D chip&\#x27;s output, and one reports that a Voodoo 2&\#x27;s output level is lower than an S3 Virge/DX, requiring brighter CRT settings. A commenter notes that John Carmack answered the question, but the supplied material does not include the technical details of his reply.

hackernews · mfiguiere · Nov 17, 00:16 · [Discussion](https://news.ycombinator.com/item?id=50525575)

**「Background」** 3dfx, founded in 1994, was an early dominant maker of PC 3D add-in cards; its Voodoo Graphics card helped establish the market in the mid-1990s before Nvidia acquired the company in 2000. The Voodoo 1 and 2 discussed here were 3D add-in boards that sat between an existing 2D card and the monitor, switching between a passthrough signal and their own analog output, so VGA voltage levels and output calibration are central to the washed-out-color question.

**「Impact」** For retro-PC users combining 3dfx and non-3dfx cards, the reported difference in output level means brightness may need to be readjusted when switching between the passthrough signal and the 3D card rather than treated as a color-space setting alone.

**「Community discussion」** Commenters offer two hardware-side explanations: VGA voltage standards were not always followed, and early Voodoo cards&\#x27; switching and output circuitry could produce different levels from the 2D card. One user reports having to brighten a CRT when running a Voodoo 2 paired with an S3 Virge/DX.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/3dfx">3dfx - Wikipedia</a></li>
<li><a href="https://zh.wikipedia.org/wiki/3dfx">3dfx - 维基百科，自由的百科全书</a></li>

</ul>
</details>

**Tags**: `#3dfx`, `#graphics hardware`, `#retro computing`, `#VGA`, `#color management`

---

<a id="item-tech-news-11"></a>
### [Apple explains macOS Full Disk Access and System and App Protection override](https://support.apple.com/en-us/149699) ⭐️ 6.0/10

Apple&\#x27;s support page explains when a macOS app may ask for Full Disk Access or a System and App Protection override, two broad permission requests that users can approve or deny. The page is explanatory documentation rather than an announcement of new permission-scoping controls, and it focuses on why an app would present either prompt. It does not provide independent data on how many apps request such access or whether each request is necessary.

hackernews · jshier · Nov 17, 02:17 · [Discussion](https://news.ycombinator.com/item?id=50526560)

**「Background」** Full Disk Access is a macOS privacy permission that gives an app broad access to files that would otherwise be protected, rather than the narrower access granted for a specific folder or device. In the linked Hacker News thread, commenters note that granting it requires clicking “Bypass System Protections,” a stronger step than the prompts used for other macOS permissions, and the Apple page lists backup, disk-cleaner, file-indexing, and security apps among those that may ask.

**「Impact」** Users faced with either prompt must decide whether to grant broad access or bypass protection, and developers whose apps depend on that access should expect to explain why narrower file or folder permissions are insufficient.

**「Community discussion」** Commenters disagreed sharply about the prompts: some argued macOS permissions are too coarse, forcing broad access because Apple does not offer per-folder scoping or exclusions, while another said the prompts are useful because too many apps request Full Disk Access unnecessarily. One user reported counting 44 apps that asked for Full Disk Access and granting it to only 8, citing Anki and Soulver as examples of apps that did not need it.

<details><summary>References</summary>
<ul>
<li><a href="https://news.ycombinator.com/item?id=50526560">If an App Asks for Full Disk Access or System and App Protection ...</a></li>

</ul>
</details>

**Tags**: `#macOS`, `#privacy`, `#permissions`, `#Apple`, `#security`

---

<a id="item-tech-news-12"></a>
### [LLM 0.37.3 fixes logging breakage from SQLite 3.54.1](https://simonwillison.net/2026/Nov/16/llm/) ⭐️ 5.0/10

LLM 0.37.3 is a bug-fix release for the LLM CLI, primarily addressing a logging failure triggered by SQLite 3.54.1, the version now shipped by Homebrew. In SQLite 3.54.1, \`select json\_object\(&\#x27;a&\#x27;, \(select json\_array\(1\)\)\)\` returns \`\{&quot;a&quot;:&quot;\[1\]&quot;\}\` instead of 3.54.0&\#x27;s \`\{&quot;a&quot;:\[1\]\}\`; SQLite&\#x27;s D. Richard Hipp says the new result is correct because \`\(SELECT json\_array\(...\)\)\` returns SQL text, not JSON. The release documents the workaround of wrapping the subquery in \`json\(\)\`: \`select json\_object\(&\#x27;a&\#x27;, json\(\(select json\_array\(1\)\)\)\)\`.

rss · Simon Willison · Nov 16, 23:57

**「Background」** SQLite&\#x27;s JSON functions distinguish an actual JSON value from text that merely contains JSON. A scalar subquery such as \`\(select json\_array\(1\)\)\` returns SQL text, so SQLite 3.54.1 stopped implicitly converting that text when it is passed to \`json\_object\(\)\`, requiring an explicit \`json\(\)\` cast to parse it.

**「Impact」** For users of the LLM CLI installed through Homebrew, upgrading to 0.37.3 is the direct fix for logging failures caused by the bundled SQLite 3.54.1. Developers writing similar SQLite JSON queries must wrap JSON-returning subqueries in \`json\(\)\` if they rely on nested JSON rather than a stringified value.

**Tags**: `#sqlite`, `#llm-cli`, `#release-notes`, `#json-functions`, `#bugfix`

---