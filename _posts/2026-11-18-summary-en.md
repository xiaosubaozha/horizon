---
layout: default
title: "Horizon Summary: 2026-11-18 (EN)"
date: 2026-11-18
lang: en
---

> From 20 items, 3 important content pieces were selected

---

**Technology News**
1. [SolidJS 2.0 Ships Server RPC and Live Primitives](#item-tech-news-1) ⭐️ 8.0/10
2. [Datasette Lite rewrite runs full Datasette in browser via service workers](#item-tech-news-2) ⭐️ 8.0/10
3. [Microsoft announces MAI Code 2 and Code 2 Flash coding models](#item-tech-news-3) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [SolidJS 2.0 Ships Server RPC and Live Primitives](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 8.0/10

SolidJS 2.0 has shipped with new server-side primitives and tooling, including server RPC and &quot;live&quot; and &quot;broadcast&quot; primitives intended to bridge frontend and backend code. The release also adds improved debug diagnostics, which the project frames as support for agent-written code.

hackernews · pier25 · Nov 17, 18:56 · [Discussion](https://news.ycombinator.com/item?id=50536387)

**「Background」** Solid 2.0 follows the framework&\#x27;s 1.x line. The project&\#x27;s &quot;Road to 2.0&quot; discussion had already framed the upgrade as a migration for existing 1.x codebases, with community members asking how much effort moving from 1.x to 2.0 would require.

**「Migration, not a drop-in upgrade」** Because 2.0 is a major version, teams running Solid 1.x should scope the upgrade as a migration rather than a patch: the project&\#x27;s own roadmap discussion frames the 1.x-to-2.0 move around how much effort core method signature changes will require, and beta-era write-ups caution that some identifiers could still shift before stable. A team retrospective describes containing the change to a single high-traffic widget instead of a full rewrite, an incremental path that lets adopters validate 2.0 in production before committing the rest of the codebase.

**「Community Discussion」** Commenters largely praised the server RPC and &quot;live&quot;/&quot;broadcast&quot; design; pwmglenn argued it feels more seamless and natural than Remix&\#x27;s middle-layer approach, LiveView, or htmx/Datastar. wk\_end questioned the &quot;Built to Be Written by Agents&quot; framing, noting that the diagnostics improvements also benefit hand-written code and blur the line between agent and human best practices.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/solidjs/solid/discussions/2425">The Road to 2 . 0 · solidjs solid · Discussion #2425 · GitHub</a></li>
<li><a href="https://github.com/solidjs/solid/discussions/2425">The Road to 2 . 0 · solidjs solid · Discussion #2425 · GitHub</a></li>
<li><a href="https://dev.to/johalputt/retrospective-solidjs-20-improved-our-dashboard-interactivity-by-40-no-react-rewrite-needed-2kfg">Retrospective: SolidJS 2 . 0 Improved Our... - DEV Community</a></li>
<li><a href="https://coderlegion.com/21782/solidjs-2-0-a-react-developers-first-look-at-signals-and-async">SolidJS 2 . 0 : A React Developer&#x27;s First Look at Signals... - Coder Legion</a></li>

</ul>
</details>

**Tags**: `#solidjs`, `#javascript-frameworks`, `#frontend-development`, `#reactivity`, `#server-rpc`

---

<a id="item-tech-news-2"></a>
### [Datasette Lite rewrite runs full Datasette in browser via service workers](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison released a complete service-worker-based rewrite of Datasette Lite, now running the full Datasette Python application in the browser via Pyodide and WebAssembly at lite.datasette.io. Developers can use URL arguments to load SQLite, JSON, CSV, or SQL data; select a released Datasette version from PyPI or a GitHub commit, tag, or branch; choose from over 100 SQLite versions; and install Datasette plugins from PyPI or wheel URLs, including JavaScript visualization tools. Data and metadata URLs must have open CORS headers, which Gist-hosted files provide.

rss · Simon Willison · Nov 17, 16:48

**「Background」** Datasette Lite is not a new project: Simon Willison launched it in 2022 as a Pyodide/WebAssembly port that ran Datasette in a web worker, simulated requests, and injected the returned HTML into the top-level page with \`innerHTML\`. That shortcut broke any Datasette feature that depended on JavaScript, because script tags inserted via \`innerHTML\` do not execute.

**「Impact」** The rewrite makes Datasette Lite usable for reproducible demos and bug reports: a single URL can pin the Datasette reference, SQLite version, data, and plugins—for example, Willison linked ?ref=1.0a42 to show an empty second page and ?ref=1.0a43 to show the fix—without running a web server. Users loading their own data must host it behind open CORS headers or the browser cannot fetch it.

**Tags**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#SQLite`

---

<a id="item-tech-news-3"></a>
### [Microsoft announces MAI Code 2 and Code 2 Flash coding models](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) ⭐️ 7.0/10

Microsoft announced MAI Code 2 and MAI Code 2 Flash, two coding models. The supplied announcement material does not include benchmark scores, model sizes, context limits, pricing, or a formal rollout schedule, so performance claims cannot be independently checked. Commenters reported that MAI Code 2 appeared in GitHub Copilot, with one saying it was offered at a 50% discount, but that availability is anecdotal rather than confirmed by the source.

hackernews · lemonish97 · Nov 17, 18:25 · [Discussion](https://news.ycombinator.com/item?id=50535885)

**「Background」** MAI Code 2 and Code 2 Flash are the next generation of Microsoft&\#x27;s MAI-Code family. GitHub&\#x27;s changelog frames the release as an expansion of that family from lightweight coding assistance to complex, agentic software engineering.

**「Impact」** For GitHub Copilot users, the practical change is a new selectable coding model if the reported rollout reaches their account. One commenter said MAI Code 2 resolved Python build problems under Windows WSL/Ubuntu, generated passing test cases, and fixed Azure Bicep deployment issues; that is a single user report, not a measured comparison with Claude Opus or other models.

**「Community Discussion」** Commenters debated the competitive moat: one argued that OpenAI and Anthropic are better than rivals only by a few months and must keep sprinting to stay ahead, while another asked how Microsoft caught up so quickly and speculated, without evidence, that distillation from GPT might explain it. A separate thread questioned Copilot&\#x27;s value, with one user saying they cancelled the $19 tier because credits ran out quickly and code review was not customizable, but would still try the new models.

<details><summary>References</summary>
<ul>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>

</ul>
</details>

**Tags**: `#AI coding models`, `#Microsoft`, `#GitHub Copilot`, `#model release`, `#developer tools`

---