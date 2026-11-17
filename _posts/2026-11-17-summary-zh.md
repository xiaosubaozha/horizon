---
layout: default
title: "Horizon Summary: 2026-11-17 (ZH)"
date: 2026-11-17
lang: zh
---

> 从 17 条内容中筛选出 12 条重要资讯。

---

**科技新闻**
1. [vLLM v0.34.0 默认启用可扩展 KV 缓存并移除 Model Runner V1](#item-tech-news-1) ⭐️ 8.0/10
2. [OpenAI 宣布 GPT-6.2 Astra 与 Sol](#item-tech-news-2) ⭐️ 8.0/10
3. [Optimizely 据报被入侵，经 Zoom、GitLab 等站点传播恶意软件](#item-tech-news-3) ⭐️ 8.0/10
4. [Datasette Lite 重写：浏览器运行完整 Datasette 应用](#item-tech-news-4) ⭐️ 8.0/10
5. [卡内基梅隆推出 CS Learn，免费发布完整学期课程](#item-tech-news-5) ⭐️ 7.0/10
6. [路透社：美高度机密国家安全通信网络据报宕机](#item-tech-news-6) ⭐️ 6.0/10
7. [FrontierHarness Eval v1.1 比较终端任务中的代理框架与模型](#item-tech-news-7) ⭐️ 6.0/10
8. [观点文章主张改善现有开源工具而非增加应用](#item-tech-news-8) ⭐️ 6.0/10
9. [Claude Code 验证实践引发成本与可靠性讨论](#item-tech-news-9) ⭐️ 6.0/10
10. [3dfx 显卡色彩偏淡原因讨论](#item-tech-news-10) ⭐️ 6.0/10
11. [Apple 说明 macOS 完全磁盘访问与系统保护覆盖请求](#item-tech-news-11) ⭐️ 6.0/10
12. [LLM 0.37.3 修复 SQLite 3.54.1 引发的日志故障](#item-tech-news-12) ⭐️ 5.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [vLLM v0.34.0 默认启用可扩展 KV 缓存并移除 Model Runner V1](https://github.com/vllm-project/vllm/releases/tag/v0.34.0) ⭐️ 8.0/10

vLLM 发布 v0.34.0，包含来自 412 名贡献者的 1,061 个提交，默认启用可扩展 KV 缓存、移除 Model Runner V1，并新增 10 个模型。新的默认行为会根据预热后实际空闲的显存确定 KV 缓存大小；发布说明称，MiniMax-M3 在 H200 上的缓存从 433k tokens 增至 672k tokens，但部分 H200 模型在并发 128 时 TPOT 可能上升 6%–18%，可用 --gpu-memory-utilization 0.9 或 --no-enable-extensible-kv-cache 退出。升级还带来破坏性变更：默认 --block-size 从 16 改为 64，ROCm 7.2 构建不再发布，并要求 huggingface\_hub &gt;= 2.0.0；设置 VLLM\_USE\_V2\_MODEL\_RUNNER=0 会在启动时失败。发布说明称，Blackwell 与 MI355X 上最高有 1.95× 解码、1.6× 吞吐和 1.24–1.40× 长提示词 TTFT 提升，同时新增 Mistral Large 4 等模型支持。

github · khluu · 11月16日 23:22

**「背景」** vLLM 通过 PagedAttention 以固定大小的块管理 KV 缓存，此前默认块大小为 16；本次发布将默认值改为 64，而 ROCm 上的分页注意力仍沿用 16。Model Runner 是 vLLM 在 GPU 上执行模型的运行时路径，V2 是接替旧版 V1 的实现，本次发布后 V1 被彻底移除，继续设置 VLLM\_USE\_V2\_MODEL\_RUNNER=0 会导致启动失败。KV 缓存容量此前依赖显存占用估算，本次改为按 CUDA 图捕获与预热后实际空闲的显存计算，并把 gpu\_memory\_utilization 默认值提到 1.0；若想保留旧行为，可传入 --gpu-memory-utilization 0.9 或 --no-enable-extensible-kv-cache。

**「升级影响」** 现有部署升级前应检查兼容性：若依赖旧的 16 块大小或旧 KV 缓存估算，需显式传入 --block-size 16 和/或 --gpu-memory-utilization 0.9；使用 V1 日志处理器的代码需迁移到 vllm.v1.worker.gpu.sample.logits\_processor，ROCm 7.2 用户需改用 ROCm 10.0 的镜像或 wheel。

**标签**: `#vLLM`, `#LLM inference`, `#open source`, `#performance`, `#breaking changes`

---

<a id="item-tech-news-2"></a>
### [OpenAI 宣布 GPT-6.2 Astra 与 Sol](https://openai.com/index/introducing-gpt-6-2-astra-sol/) ⭐️ 8.0/10

根据条目信息，OpenAI 宣布推出 GPT-6.2 Astra 与 Sol，加入 GPT-6.2 版本线。除名称外，提供的材料没有给出参数规模、上下文长度、定价、API 可用性或独立基准结果，因此无法确认这是一次全面发布还是有限开放。相关能力与成本说法仍需以官方页面或独立测试为准。

hackernews · jasondavies · 11月17日 17:46 · [社区讨论](https://news.ycombinator.com/item?id=50535230)

**「背景」** 这条消息指向 OpenAI 官网的一个发布页面（openai.com/index/introducing-gpt-6-2-astra-sol/），但抓取时未获得任何正文，因此 GPT-6.2 Astra 与 Sol 的具体能力、版本编号、可用范围与定价目前只能从标题和评论推断，均未获官方文本确认。评论中出现的「Sol」「Luna」「GPT-5.6 Sol」等提法显示，Sol 更像是延续自此前模型系列的名称而非全新术语，但这些都属于社区说法，不能当作既定事实。

**「社区讨论」** 有评论者认为，若基准数据成立，其性价比“高得惊人”，但更关心真实任务表现，并询问是否有比 Pelican 基准更适合快速评估的替代方案；也有人称 Sol 是公司账户上的主力模型，同时期待新的 Luna。另有评论批评展示的幻灯片、工作簿和备忘录示例质量不佳，并质疑为何科学基准未列出 Gemini 4 Carbon 的分数。

**标签**: `#OpenAI`, `#GPT-6.2`, `#large language models`, `#AI benchmarks`, `#model release`

---

<a id="item-tech-news-3"></a>
### [Optimizely 据报被入侵，经 Zoom、GitLab 等站点传播恶意软件](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/) ⭐️ 8.0/10

据 Report-uri 博客报道，第三方实验与个性化脚本供应商 Optimizely 遭入侵，并被用来通过包括 Zoom、GitLab 在内的多个大型网站向访问者分发恶意软件。报道将此定性为第三方脚本供应链风险：恶意代码沿 Optimizely 向这些站点提供脚本的路径投递。现有材料未披露受影响的脚本版本、感染时间窗口、载荷类型或受影响站点的完整名单，相关方也未作出回应，因此该事件目前仍属未经独立确认的报道。

hackernews · kristjansson · 11月16日 23:00 · [社区讨论](https://news.ycombinator.com/item?id=50524767)

**「背景」** Optimizely 是一个网页实验与个性化平台，站点通过嵌入其客户端脚本，从供应商托管的 CDN 加载 JavaScript；一旦该脚本被篡改，恶意代码就会随受信任的第三方代码进入访客浏览器。相关讨论指出，这次并非 CDN 缓存投毒，而是 Optimizely 的 CDN 分发了被放入的内容，Optimizely 自己的 www 与 login 站点脚本也包含该代码。

**「影响与处置」** 对使用 Optimizely Web 做 A/B 测试和个性化投放的站点来说，这段脚本运行在自有页面的第一方上下文里，一旦被植入恶意代码，访客浏览器会直接执行，站点无法靠同源策略把它隔离在外。据 cybersecuritynews.com 的报道，11 月 16 日注入的 JavaScript 触达了 178 家机构的访客；受影响的站点若要止损，通常只能先移除或阻断 Optimizely 脚本，代价是同期实验与个性化功能随之中断，恢复前还需确认所加载脚本的版本与来源。

**「社区讨论」** 评论者集中质疑第三方脚本的治理方式：stickfigure 认为 Google Tag Manager 让市场团队无需工程介入即可加标签，正是新闻页面动辄加载大量 JavaScript 的来源，希望业界重新评估；mcoliver 认为缺乏实质追责机制才是问题根源，主张大型站点应自行托管（vendoring）关键脚本，而不是直接引用供应商。另有用户询问该感染是否会持久影响手机和电脑、uBlock Origin 能否拦截，讨论中未给出确定答案。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/">World&#x27;s Largest Brands Infected With Malware Via Optimizely</a></li>
<li><a href="https://cybersecuritynews.com/optimizely-websites-hijacked/">Hackers Infect 178 Major Websites via Optimizely to Steal Credit...</a></li>

</ul>
</details>

**标签**: `#supply-chain-security`, `#third-party-scripts`, `#web-security`, `#malware`, `#optimizely`

---

<a id="item-tech-news-4"></a>
### [Datasette Lite 重写：浏览器运行完整 Datasette 应用](https://simonwillison.net/2026/Nov/17/datasette-lite/) ⭐️ 8.0/10

Simon Willison 发布了 Datasette Lite 的完全重写版，借助 service workers 和 Pyodide 在浏览器中运行完整的 Datasette Python 服务端应用，并称其效果“几乎与真正的服务端应用无法区分”。新版可通过 lite.datasette.io 的 URL 参数加载 SQLite 数据库、JSON、CSV 或 SQL 脚本，从 PyPI 选择已发布的 Datasette 版本，或从 GitHub 指定 commit、tag、branch，还可在 100 多个 SQLite 版本中选择，并从 PyPI 或 wheel URL 安装插件（包括 JavaScript 可视化插件）。这取代了 2022 年初版依靠 Pyodide web worker 模拟请求、再用 innerHTML 注入 HTML 的做法；旧方式会使依赖 JavaScript 的功能失效。

rss · Simon Willison · 11月17日 16:48

**「背景」** Datasette Lite 并非新项目：作者于 2022 年首次发布它，最初是在 Pyodide Web Worker 中运行 Datasette、模拟请求，再通过 innerHTML 把生成的 HTML 注入顶层页面。该方案的限制在于，innerHTML 中的 script 标签不会执行，因此依赖 JavaScript 的功能无法正常工作。此次重写改用 service worker 来处理请求，使完整的服务端 Datasette 应用能在浏览器中运行，并恢复插件等此前受限的能力。

**「实际影响」** 对需要演示或复现问题的开发者，可直接分享固定到特定 Datasette 版本、插件和 SQLite 版本的 lite.datasette.io 链接，无需启动 Web 服务器；Willison 已用 1.0a42 与 1.0a43 的链接对比分页 bug。使用外部数据库、CSV 或 metadata 文件时，托管这些文件的服务器必须提供开放的 CORS 响应头，否则浏览器端无法加载。

**标签**: `#Datasette`, `#Pyodide`, `#WebAssembly`, `#service workers`, `#SQLite`

---

<a id="item-tech-news-5"></a>
### [卡内基梅隆推出 CS Learn，免费发布完整学期课程](https://www.cs.cmu.edu/learn/) ⭐️ 7.0/10

卡内基梅隆大学推出 CS Learn，在 YouTube 免费发布该校当前计算机科学课程的完整学期讲座。项目负责人 Phillip Compeau 在讨论中表示，本周每天首播一门课程，明年 1 月还会上线更多课程。Compeau 还称，几名该校学生构建的工具自动化了大量制作工作，让小团队也能完成课程发布。

hackernews · pcompeau · 11月16日 20:43 · [社区讨论](https://news.ycombinator.com/item?id=50522980)

**「背景」** 开放课件（open courseware）指高校将完整学期的课程材料免费公开发布到网上，供任何人学习。CMU 的 Phillip Compeau 在讨论中主动承认，MIT 大约 25 年前就已经在这条路上先行一步；他解释，此次 CMU 的不同之处不在“免费公开”本身，而在于几位学生开发的自动化工具让小团队也能承担整学期讲座视频的制作。

**「影响」** 对自学者来说，完整学期课程可以按课程结构免费跟进；但已有观众指出，已上线的《Principles of Computing》在教师离开麦克风后出现明显回声和压缩失真，录音质量可能影响学习体验。

**「社区讨论」** 评论区就 AI 时代是否还值得学习基础展开争论：有评论认为打好基础后 AI 会成为增强工具，否则可能被替代；也有人反问为何要学习自己永远用不到的内容。

**标签**: `#open courseware`, `#computer science education`, `#Carnegie Mellon`, `#YouTube`, `#free online courses`

---

<a id="item-tech-news-6"></a>
### [路透社：美高度机密国家安全通信网络据报宕机](https://www.reuters.com/technology/highly-classified-us-national-security-communications-network-is-down-cnn-2026-11-17/) ⭐️ 6.0/10

路透社 2026 年 11 月 17 日发稿，引述 CNN 报道称，美国一个高度机密的国安通信网络处于宕机状态。报道没有说明该网络的具体名称、受影响范围、故障起止时间或是否涉及外部攻击，也未给出恢复时间表。标题所指的 NSA 内部网络与报道所称“国安通信网络”之间的关系，在现有材料中未获进一步说明。就目前公开信息看，这是一则仅有标题层面细节的宕机报道，尚无厂商或官方技术说明可供核实。

hackernews · nodoodles · 11月17日 15:50 · [社区讨论](https://news.ycombinator.com/item?id=50533089)

**「背景」** 美国国家安全局与其中央安全局（NSA/CSS）负责美国政府的密码学工作与外国信号情报，并提供网络安全产品和服务，其内部网络承载的是涉密通信与情报业务，而非普通办公系统。正因如此，这类网络的可用性问题通常同时被视为安全事件，而不只是运维故障。

**「影响」** 由于 NSA Net 承载 NSA 内部的机密信息通信，此次中断直接影响该机构员工在内部传递涉密内容的能力；报道未说明是否存在可用的备用通道，也未给出恢复时间或原因，因此相关工作人员只能依赖未公开的替代方式维持联络。

**「社区讨论」** Hacker News 评论者对披露时机提出疑问，dustfinger 表示意外：在恢复运行并确认安全之前就公开高度机密网络宕机，与他的预期不符。另一些评论者把此事与近期多起服务中断并列，认为“四件事连着发生”已成某种模式（ssalka、tgsovlerkhgsel），lucascdotnet 则提出这可能是“巴德尔-迈因霍夫现象”，即报道变多而非故障率上升；AISnakeOil 猜测是否存在国家支持的人工智能网络攻击并掩盖痕迹，但上述均为未获证据支持的推测。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.nsa.gov/">National Security Agency | Central Security Service</a></li>
<li><a href="https://www.cnn.com/2026/11/17/politics/highly-classified-national-security-communications-network-goes-down">Exclusive: Highly classified US national security communications ...</a></li>
<li><a href="https://www.zerohedge.com/markets/nsas-spy-network-reportedly-goes-dark-sending-stocks-sliding">NSA &#x27;s Spy Network Reportedly Goes Dark, Sending... | ZeroHedge</a></li>

</ul>
</details>

**标签**: `#cybersecurity`, `#network-outage`, `#national-security`, `#NSA`, `#incident-reporting`

---

<a id="item-tech-news-7"></a>
### [FrontierHarness Eval v1.1 比较终端任务中的代理框架与模型](https://runta.com/blog/introducing-frontierharness-eval-v1-1/) ⭐️ 6.0/10

一篇博客文章介绍了 FrontierHarness Eval v1.1，用于在 terminal-bench 任务上比较 AI 代理的 harness 与模型组合。目前可确认的是评测对象和用途，具体任务集、评分方法和排名结果尚不清楚。该评测面向需要选择代理框架和模型的开发者，但这次介绍没有呈现可供独立判断的基准数据。

hackernews · Edward40 · 11月17日 14:53 · [社区讨论](https://news.ycombinator.com/item?id=50532191)

**「背景」** 这里的 harness 指包裹大模型、负责组织提示词、工具调用、上下文与执行流程的智能体框架，因此同一模型在不同 harness 下的表现可能不同。FrontierHarness Eval 的公开发布信息显示，该评测覆盖 21 个 AI 编程智能体 harness，包括 Claude Code、Codex CLI 和 OpenCode，并在 5 个模型、62 个任务上比较通过率、成本和速度。

**「影响」** 对正在选型的开发者来说，这类评测更适合理解为特定 terminal-bench 任务和 harness 配置下的相对表现，而不是跨任务选择唯一最佳组合的依据。评论者还提醒，“Failed”指未满足基准测试的通过条件，并非运行时崩溃，因此不能把失败运行中的 token 消耗直接等同于系统故障成本。

**「社区讨论」** HN 评论者质疑原标题把 64% 的支出与未通过 terminal-bench 验证器的任务联系起来，认为这可能是在迎合“AI 烧钱”的叙事，并指出后来标题已被修改。另一条讨论认为最佳 harness 取决于具体问题，且随着模型能力提升，harness 可能比模型更重要。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://frontierharness.org/">FrontierHarness Eval: AI coding agent harness benchmark</a></li>
<li><a href="https://github.com/frontier-harness-eval/eval">GitHub - frontier-harness -eval/eval: Public results and task ...</a></li>

</ul>
</details>

**标签**: `#AI agents`, `#benchmarking`, `#LLM evaluation`, `#coding agents`, `#developer tooling`

---

<a id="item-tech-news-8"></a>
### [观点文章主张改善现有开源工具而非增加应用](https://jordankrueger.com/blog/better-open-source-not-more-apps/) ⭐️ 6.0/10

这是一篇观点文章，主张开发者和用户把精力投入改进现有开源工具，而不是继续发布更多应用。文章提出的做法是：选一个日常使用的开源工具，找出安装或运行中最烦人的问题，花一个周末与维护者一起修复。文中没有给出已实施的项目、版本、性能数据或可验证的采用结果。

hackernews · pandemicsoul · 11月17日 14:45 · [社区讨论](https://news.ycombinator.com/item?id=50532086)

**「背景」** 开源项目往往依赖少数维护者处理问题分类、代码审查和后续维护；外部提交的改动即使只想修一个小麻烦，也会增加这些人的审查与长期维护负担。Hacker News 评论者 joshdata 以自己项目“几乎难以为继”为例描述了这种压力，而这篇观点文章的主张正建立在这一维护现实之上：改善现有工具的安装与运行体验，不只是写代码，还涉及与维护者协作并承担持续维护。

**「影响」** 对想按此建议贡献代码的人，实际约束是维护者的审阅时间：评论中的维护者表示，外部拉取请求增多后自己没有时间处理，修复小问题和性能边缘情况的贡献可能积压。

**「社区讨论」** 评论对文章的前提有分歧：joshdata 说自己的开源项目在少量拉取请求时已难以持续，如今收到更多修复小问题的拉取请求却无暇处理；linsomniac 则称，AI 辅助的缺陷修复曾因项目计划采取“不用 AI”政策而被拒绝，并建议干脆用 AI 生成替代工具。timbert 认为问题不止是应用数量，而是软件交付方式本身，并以让 MIDI 键盘配合 DAW 和 VST 插件为例描述安装配置的挫败。

**标签**: `#open source`, `#software maintenance`, `#maintainer burnout`, `#AI contributions`, `#software usability`

---

<a id="item-tech-news-9"></a>
### [Claude Code 验证实践引发成本与可靠性讨论](https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/) ⭐️ 6.0/10

Hacker News 上围绕《Claude Code 团队如何看待验证》的讨论，聚焦于 Claude Code 团队所采用的验证实践，而不是一次产品发布或版本更新。讨论中的主要争议是：用大量 token 驱动代理逐项验证是否实用、是否可靠，以及是否有更省成本的替代方案。

hackernews · craigmart · 11月17日 10:20 · [社区讨论](https://news.ycombinator.com/item?id=50529612)

**「背景」** Claude Code 团队此前已撰文介绍 Anthropic 的代码审查流程；据其博客，该团队约 90% 的代码由 Claude 编写和审查，而这篇新文章进一步聚焦“验证”，即实际运行改动。文章还讨论了端到端测试、属性测试和差分测试如何为编码代理提供证据，并约束验证器本身。

**「影响」** 对使用 AI 编码代理的开发者来说，评论中出现了明确的成本信号：一位用户称每月仅运行一两个代理就要花费 2000 美元 token，这使是否把回归检查交给专用测试工具成为实际的工程取舍。

**「社区讨论」** 评论者对文章中的高 token 验证方式意见不一：OtherShrezzing 认为逐项用 Claude 和浏览器工具检查回归过于昂贵，Playwright 等工具能以更低成本取得相同或更好效果；girvo 则称自己每月已为一两个代理花费 2000 美元，质疑如何承担更大规模并行。tshaddox 还追问 Claude Code 如今是否足够稳定，显示部分用户仍对其实用性有所保留。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://claude.dev/blog/how-the-claude-code-team-thinks-about-verification/">How the Claude Code team thinks about verification</a></li>
<li><a href="https://t.me/aisferaic/1270">AI для каждого | AISferaic – Telegram</a></li>

</ul>
</details>

**标签**: `#Claude Code`, `#AI coding agents`, `#software verification`, `#developer tooling`, `#LLM costs`

---

<a id="item-tech-news-10"></a>
### [3dfx 显卡色彩偏淡原因讨论](https://twitter.com/id_aa_carmack/status/2122478083319992513) ⭐️ 6.0/10

这则 Hacker News 讨论试图解释 3dfx 显卡为何色彩偏淡，焦点包括模拟 VGA 信号电压标准是否被遵守、不同显卡的输出电平差异，以及 sRGB 与 CRT 信号电压的线性关系。AkBKukU 举例称，Voodoo 2 搭配 S3 Virge/DX 时输出电平低于 2D 卡，在 CRT 上需要调亮。Dwedit 则澄清，sRGB 编码值虽非线性，但 CRT 的信号电压与 50% sRGB 的对应关系是线性的。

hackernews · mfiguiere · 11月17日 00:16 · [社区讨论](https://news.ycombinator.com/item?id=50525575)

**「背景」** VGA 用模拟电压分别传输红、绿、蓝信号，显示器再把电压映射为亮度；sRGB 的伽马编码使线性亮度 50% 大约对应 74% 的编码值，因此模拟输出电平或伽马处理不一致时，颜色就容易显得发白。3dfx 在 1990 年代中期以 Voodoo 系列 3D 加速卡成为 PC 图形市场的先驱，早期 Voodoo 还通过 2D 显卡的 VGA 直通或切换来输出画面，模拟链路会涉及多块卡。

**「影响」** 对仍使用 CRT 或模拟采集的复古硬件用户，Voodoo 2 与不同 2D 卡之间的输出电平差异意味着切换信号源时可能需要单独调亮或校准；这是模拟链路兼容性问题，不能只靠统一的软件色彩配置解决。

**「社区讨论」** 社区讨论提供了两条技术线索：AkBKukU 强调 VGA 模拟电压标准未必被厂商遵守，并用 Voodoo 2 与 S3 Virge/DX 的电平差异佐证；Dwedit 则从 sRGB 与 CRT 信号电压的线性关系解释为何不能把 sRGB 非线性直接当作原因。这些是评论者的经验与解释，并非对 3dfx 全部产品的统一结论。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/3dfx">3dfx - Wikipedia</a></li>

</ul>
</details>

**标签**: `#3dfx`, `#graphics hardware`, `#retro computing`, `#VGA`, `#color management`

---

<a id="item-tech-news-11"></a>
### [Apple 说明 macOS 完全磁盘访问与系统保护覆盖请求](https://support.apple.com/en-us/149699) ⭐️ 6.0/10

Apple 的支持文档解释了 macOS 应用何时会请求“完全磁盘访问”（Full Disk Access），以及何时会请求“系统与应用保护”覆盖。它面向遇到权限弹窗的用户和需要申请权限的开发者，属于支持文档而非独立技术分析。Hacker News 的讨论则集中在该权限模型的范围过宽：应用经常申请超出实际需要的访问权，开发者若无法套用更窄的授权范围，仍会请求全局访问。

hackernews · jshier · 11月17日 02:17 · [社区讨论](https://news.ycombinator.com/item?id=50526560)

**「背景」** macOS 的“完全磁盘访问权限”（Full Disk Access）是一项系统隐私权限：应用只有获得用户授权后，才能访问受保护的位置，否则会被系统拦截。Apple 的这份支持文档说明应用会在什么情况下请求该权限，以及何时会请求“系统与应用保护覆盖”（System and App Protection Override）。据讨论中引述文档内容，授予完全磁盘访问权限需要点击“Bypass System Protections”，而其他权限提示没有这一步。

**「影响」** 需要遍历磁盘的 macOS 工具（如磁盘空间可视化应用）在用户拒绝完全磁盘访问后可能只能显示受限结果；用户若想保留 ~/.ssh 等目录的私密性，目前更现实的做法是拒绝全局授权，而不是依赖按文件夹排除。

**「社区讨论」** 支持者认为强提示能阻止应用滥用：有评论者称自己的 Mac 上有 44 个应用请求完全磁盘访问，但只授权了 8 个，Anki 和 Soulver 等应用没有该权限也能正常工作。批评者则认为 API 权限粒度不足，呼吁允许按常用目录授权并排除 ~/.ssh 等敏感路径；还有观点强调，连熟悉安全运维的人都可能被攻破，因此不应把整块磁盘随意交给 AI 工具。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://news.ycombinator.com/item?id=50526560">If an App Asks for Full Disk Access or System and App Protection ...</a></li>

</ul>
</details>

**标签**: `#macOS`, `#privacy`, `#permissions`, `#Apple`, `#security`

---

<a id="item-tech-news-12"></a>
### [LLM 0.37.3 修复 SQLite 3.54.1 引发的日志故障](https://simonwillison.net/2026/Nov/16/llm/) ⭐️ 5.0/10

LLM 0.37.3 是一个错误修复版本，主要解决 Homebrew 最新附带的 SQLite 3.54.1 导致 LLM 日志代码出错的问题。SQLite 3.54.1 修正了 3.54.0 的 JSON 子查询行为：\`select json\_object\(&\#x27;a&\#x27;, \(select json\_array\(1\)\)\)\` 现在返回 \`\{&quot;a&quot;:&quot;\[1\]&quot;\}\`，而不是 \`\{&quot;a&quot;:\[1\]\}\`。发布说明给出的变通方法是在子查询外再套一层 \`json\(\)\`，即 \`select json\_object\(&\#x27;a&\#x27;, json\(\(select json\_array\(1\)\)\)\)\`。

rss · Simon Willison · 11月16日 23:57

**「背景」** SQLite 维护者 D. Richard Hipp 解释，这一变化是错误修复而非回归：按文档，\`\(SELECT json\_array\(...\)\)\` 返回的是 SQL 文本，不是 JSON，因此 3.54.1 的行为才是正确的，3.54.0 才是缺陷。LLM 的日志代码此前依赖了 3.54.0 的旧行为。

**「影响」** 使用 Homebrew 安装 LLM 且已升级到 SQLite 3.54.1 的用户应升级到 0.37.3，否则日志功能会因上述查询结果变化而出错；直接使用 SQLite JSON 函数的开发者若依赖旧的自动转换，也需要在 \`json\_object\(\)\` 中显式调用 \`json\(\)\`，否则会得到字符串化后的数组。

**标签**: `#sqlite`, `#llm-cli`, `#release-notes`, `#json-functions`, `#bugfix`

---