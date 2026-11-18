---
layout: default
title: "Horizon Summary: 2026-11-18 (ZH)"
date: 2026-11-18
lang: zh
---

> 从 20 条内容中筛选出 3 条重要资讯。

---

**科技新闻**
1. [SolidJS 2.0 发布，新增服务端 RPC 与 live/broadcast 原语](#item-tech-news-1) ⭐️ 8.0/10
2. [Datasette Lite 用 Service Worker 在浏览器运行完整应用](#item-tech-news-2) ⭐️ 8.0/10
3. [微软发布 MAI Code 2 与 Code 2 Flash 编程模型](#item-tech-news-3) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [SolidJS 2.0 发布，新增服务端 RPC 与 live/broadcast 原语](https://www.solidjs.com/blog/solid-2-0-the-long-hold/) ⭐️ 8.0/10

SolidJS 发布 2.0，新增服务端 RPC 以及 \`live\`、\`broadcast\` 原语，并包含调试诊断方面的改进，主要面向使用该框架的前端与全栈开发者。现有材料没有披露破坏性变更、迁移步骤或具体兼容性条件，因此升级影响仍不明确。

hackernews · pier25 · 11月17日 18:56 · [社区讨论](https://news.ycombinator.com/item?id=50536387)

**「背景」** Solid 是一个以细粒度响应式为核心的 JavaScript 框架，此前长期停留在 1.x 版本线；官方曾开设 “The Road to 2.0” 讨论帖，向使用者征集从 1.x 升级到 2.0 的迁移工作量预期，说明大版本迁移一直是该项目的公开议题。第三方整理资料也提示，Solid 2.0 与 Solid 1.x 乃至 React 的写法都存在差异，沿用旧有或 React 式模式是常见错误来源。

**「升级成本」** 对已经使用 Solid 1.x 的团队，2.0 是需要实际评估迁移量的大版本：SolidJS 官方仓库的讨论帖里，用户就在追问从 1.x 升到 2.0 的工作量究竟落在“改动两个核心方法签名”还是更大范围；一篇第三方实践记录采取的做法是先只迁移一个高流量的筛选组件做验证，再决定是否整体升级。计划采用新服务端原语的项目宜把这种渐进式验证写进升级路径，而不是按可直接替换来排期。

**「社区讨论」** 有评论者认为，Solid 的服务端 RPC 与 \`live\`、\`broadcast\` 原语衔接自然，比 LiveView、htmx/datastar 更易用。另有评论者质疑“Built to Be Written by Agents”的定位，认为其中不少内容只是更好的调试诊断，对手写代码同样有帮助，并非智能体开发独有。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/solidjs/solid/discussions/2425">The Road to 2 . 0 · solidjs solid · Discussion #2425 · GitHub</a></li>
<li><a href="https://www.skills.sh/khmm12/solidjs-v2-skills/solidjs-v2">solidjs -v2 — khmm12/ solidjs -v2-skills</a></li>
<li><a href="https://github.com/solidjs/solid/discussions/2425">The Road to 2 . 0 · solidjs solid · Discussion #2425 · GitHub</a></li>
<li><a href="https://dev.to/johalputt/retrospective-solidjs-20-improved-our-dashboard-interactivity-by-40-no-react-rewrite-needed-2kfg">Retrospective: SolidJS 2 . 0 Improved Our... - DEV Community</a></li>

</ul>
</details>

**标签**: `#solidjs`, `#javascript-frameworks`, `#frontend-development`, `#reactivity`, `#server-rpc`

---

<a id="item-tech-news-2"></a>
### [Datasette Lite 用 Service Worker 在浏览器运行完整应用](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison 发布了 Datasette Lite 的完整重写版：此前 2022 年版本把 Datasette 放在 Pyodide web worker 中运行，并用 innerHTML 注入结果，导致依赖 JavaScript 的功能失效；新版改用 Service Worker，让完整的 Datasette Python 服务端应用通过 Pyodide 和 WebAssembly 直接在浏览器中运行，作者称其已接近真实服务端版本。通过 lite.datasette.io 的 URL 参数，用户可以加载 SQLite 数据库、JSON、CSV 或 SQL 脚本，选择 PyPI 上发布的 Datasette 版本，指定 GitHub 仓库的提交、标签或分支，并在 100 多个 SQLite 版本中选择。还可以从 PyPI 或 wheel 文件 URL 安装额外插件，包括 JavaScript 可视化插件；示例中的 datasette-maplibre 插件直接在浏览器里渲染国家边界地图。加载远程数据或元数据文件时，对应 URL 必须提供开放的 CORS 头。

rss · Simon Willison · 11月17日 16:48

**「背景」** Datasette Lite 并非新项目：作者在 2022 年推出了初版，用 Pyodide Web Worker 运行 Datasette 并模拟请求，再把生成的 HTML 通过 \`innerHTML\` 注入页面。这种做法导致 \`&lt;script&gt;\` 不会执行，依赖 JavaScript 的功能和插件因此无法工作；此次改用 Service Worker 重写，正是为了消除这一限制。

**「影响」** 对插件作者和 Datasette 维护者来说，可以把特定 Datasette 版本、SQLite 版本与插件组合固定在一个 lite.datasette.io 链接中，用来复现 bug 或演示未完成功能，而无需部署服务器；作者已用 ?ref=1.0a42 与 ?ref=1.0a43 的链接对比分页 bug 的旧行为和修复。

**标签**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#Service Workers`, `#SQLite`

---

<a id="item-tech-news-3"></a>
### [微软发布 MAI Code 2 与 Code 2 Flash 编程模型](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) ⭐️ 7.0/10

微软宣布推出 MAI Code 2 和 MAI Code 2 Flash 两款编程模型。现有材料只确认了型号与发布动作，未提供参数规模、基准测试成绩、定价或独立评测结果。社区评论称 GitHub Copilot 已提供 MAI Code 2，并有用户报告将其用于 Python/WSL、Azure Bicep 和测试生成；这些属于个人体验，尚不能视为官方可用范围或性能结论。

hackernews · lemonish97 · 11月17日 18:25 · [社区讨论](https://news.ycombinator.com/item?id=50535885)

**「背景」** GitHub 的更新日志称，MAI Code 2 和 MAI Code 2 Flash 是 MAI-Code 系列的新一代模型，作用从轻量编码辅助扩展到复杂的代理式软件工程，并已进入 GitHub Copilot。微软的发布页则把 Code 2 Flash 定位为日常高频编码任务模型，称其在三项编码基准上以 GPT-6 Luna 的 65% 成本和 Claude Haiku 5.5 的 20% 成本达到相近表现；第三方报道还提到，Code 2 达到 GPT-6.1 Sol 98% 的性能、成本为其 40%。这些性能与成本说法均来自厂商或转述，尚非独立实测结果。

**「影响」** 对 GitHub Copilot 用户而言，能否在现有订阅中切换到 MAI Code 2、以及是否按评论所说享受折扣，需要以微软或 GitHub 的官方模型列表和计费页面为准；在缺少基准数据的情况下，团队不宜仅凭单条使用体验替换生产环境中的默认模型。

**「社区讨论」** 有评论者称，MAI Code 2 在 Copilot 里处理 Python/WSL 构建、Azure Bicep 部署和生成测试用例的表现接近 Claude Opus；也有评论者认为 OpenAI 和 Anthropic 相对其他模型的领先只能维持几个月，并追问微软快速追赶是否依赖对 OpenAI 模型的蒸馏。另有用户表示已因额度消耗快、代码审查不可定制而取消 GitHub Copilot 订阅，但愿意在价格合适时再试新模型。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.blog/changelog/2026-11-17-mai-code-2-and-mai-code-2-flash-in-github-copilot/">MAI Code 2 and MAI Code 2 Flash in GitHub Copilot</a></li>
<li><a href="https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/">MAI Code 2 and Code 2 Flash: Everyday coding at scalable ...</a></li>
<li><a href="https://www.unite.ai/microsoft-ai-releases-mai-code-2-and-mai-code-2-flash-for-enterprises/">Microsoft AI Releases MAI Code 2 and MAI Code 2 Flash for ...</a></li>

</ul>
</details>

**标签**: `#AI coding models`, `#Microsoft`, `#GitHub Copilot`, `#model release`, `#developer tools`

---