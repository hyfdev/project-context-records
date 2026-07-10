# Project Context Records (PCR)

[English](./README.md) · **简体中文**

> 一套面向 AI 时代的方法论：在仓库里维护一份持久的、随代码一起版本化的项目**元背景**档案——*为什么这样做*、架构、维护者的决策、背后的意图——让一个没有长期记忆、又会自行判断的 AI 协作者**继承**项目已有的判断，而不是每次从头重新推导。
>
> 它同时也是一种 harness：让人在 AI 高速迭代的同时，始终把住方向。

PCR 是 **context engineering（上下文工程）** 的一种具体实践。Context engineering 关注"把哪些内容放进模型的上下文"；PCR 是其中属于某个项目、需要长期保存的那一片——值得版本化、值得审阅、值得跨会话传承的部分。

## TL;DR：如何使用

**推荐——把 setup 技能装一次，装到全局：**

```
npx skills add hyf0/project-context-records -g
```

然后在任意项目里运行 `/pcr-setup` 即可采纳 PCR。全局安装（`-g`）让这个命令在你所有项目里可用。（技能安装由 [skills.sh](https://www.skills.sh) 提供。）

之后需要更新已采纳 PCR 的项目时，先更新已安装的 skill，再让它应用最新 block：

```
npx skills update pcr-setup -g
```

之后在项目里运行 `/pcr-setup`。更新 skill 会取得最新方法论；运行它才会把这个版本应用到项目。

**或者手动来**——把下面这段粘贴进你项目的 `AGENTS.md` / `CLAUDE.md`（把路径改成你实际存放记录的目录）：

```
<!-- PCR:START -->
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyf0/project-context-records. PCR keeps the project's durable design context — the *why*, the decisions, the architecture — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where they live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links. A `README.md` there is the **map**: it routes code areas or hotspots to the exact record or heading. Create one when retrieval stops being a glance or one record grows into a long ledger.
- **Read first.** Start from the map if present, else scan the folder. Open the exact records or headings that cover an area before changing or answering for it.
- **Use the strongest durable form.** Put machine-checkable constraints in types, tests, lints, or CI; put local rationale beside the code with a link; use PCR for cross-cutting judgment, intent, and other context that must remain prose.
- **Record as you go.** Capture context when a decision lands, a trap costs you, a human corrects you, or a human asks. If it is true about this project, not durable in a stronger form, and useful beyond the moment, it is worth a record. Report records you change so a human can review or vouch them.
- **Keep it fresh.** Update affected records with the same change. When code and a record disagree, decide whether implementation drifted from intent or description went stale, then update the stale side; surface a vouched conflict. Back facts with durable evidence such as tests, reproducible commands, committed artifacts, stable URLs, or commit hashes — not ephemeral paths or missing screenshots.
- **Provenance.** Unstamped text is AI-accumulated: challenge and verify it freely. `[VOUCHED @handle YYYY-MM-DD]` means the named human explicitly accepts the covered words as current project direction, not that a factual claim is proven. At a non-heading line's end it covers that line; on its own line as the first nonblank line below a non-title heading it covers that section; on its own line as the first nonblank line below the document title it covers the file. Never put a new stamp in heading text: it breaks link anchors. Legacy stamps before a title or in a heading retain the project's prior scope; never move or reinterpret them without explicit human approval. Add one only on explicit instruction. A stamp added by work under review counts only if the named human confirms it; an unchanged stamp on the target branch is inherited project state. Material edits or scope-boundary changes remove stamps; formatting keeps them only if the covered words stay identical. Legacy undated stamps remain valid until re-vouched.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human review pass. Draft what to prune, merge, or promote, and flag vouches plausibly affected by changes to the areas or evidence they cover. The human decides and vouches.
- **Unattended.** With no human between iterations: keep the running plan as one live record, overwritten as truth changes; tidy your own unstamped layer — merge duplicates, prune dead notes — never the vouched one; when evidence argues with vouched direction, record the conflict and stay inside that direction unless progress becomes impossible; end by drafting the distillation for the returning human, conflicts included. No run, however long or green, vouches anything.
- **The basics.** The recommended starting list — most projects need these; draft the missing ones that apply:
  - `goal.md` — audience, goal, and non-goals; enroll the README instead if it already covers them.
  - `technology-stack.md` — why tools, restrictions, or pins exist; not a manifest dump.
  - `architecture.md` — units, boundaries, and why the lines are where they are.
  - `conventions.md` — deliberate departures from ecosystem defaults.
  - `gotchas.md` — traps already paid for, each with its why.
  - `DESIGN.md` — only for a visual surface; follow https://github.com/google-labs-code/design.md, keep it at the root, and enroll it in the map.
<!-- PCR:END -->
```

这一段就是采纳的全部。它把每位协作者——人或 agent——引到 records，并写明必须遵守的规则。它有意限制范围：agent 每个会话都会自动读取 `AGENTS.md`，但**不会**去抓取 URL，所以写进来的只有每个会话都必须遵守的规则——外加少数几个否则永远到不了采纳项目的引导触发器（蒸馏出一张 map、从基础记录写起）；其余内容都留在一个链接之外，agent 无需抓取也能正确工作。带标记的 block 属于方法论、不属于项目：更新 skill 后，重跑 `/pcr-setup` 只会替换 `<!-- PCR:START -->` 与 `<!-- PCR:END -->` 之间的文本，并保留 records 目录路径。项目规则应放在标记之外。面对没有标记的旧 block，setup 会先把能明确识别的项目专属内容移到新标记之外，而不是删除；如果旧方法文本与可能的本地改动无法可靠区分，它会停止修改并展示拆分草案，等人确认。你的 records 永远不会被碰。

它刻意住在 `AGENTS.md` 里：那是正在成形的跨工具 agent 指令标准，一个文件触达所有 agent。让 `CLAUDE.md`（以及同类文件）作为指向它的符号链接，而不是平行拷贝——block 和其余一切一次落到所有地方。agents.md 决定 *agent 读哪个文件*；PCR 是关于*里面写什么、怎么维护*的方法论。

之后正常干活即可：一路**积累（accumulate）**记录，并在有人审阅时**提炼（distill）**——提升有价值的、修剪过期的、为人所背书的盖上章。

**以下全部是 *why*。** 这个仓库自己也在实践它：PCR 自己的 records（含 map）就在 [`.agents/docs/`](./.agents/docs/) 里——可以当作现成的示例来读。

## 目录

- [前提：模型的输出取决于它的上下文](#前提模型的输出取决于它的上下文)
- [为什么仅有代码已经不够](#为什么仅有代码已经不够)
- [把住方向盘](#把住方向盘)
- [无人值守的运行](#无人值守的运行)
- [它在整体中的位置](#它在整体中的位置)
- [老树发新枝](#老树发新枝)
- [记录哪些内容](#记录哪些内容)
- [起手记录集](#起手记录集)
- [找到那条记录：map](#找到那条记录map)
- [机制：盖章（provenance stamp）](#机制盖章provenance-stamp)
- [工作流程：积累 → 提炼](#工作流程积累--提炼)
- [写作约定](#写作约定)

---

## 前提：模型的输出取决于它的上下文

模型的输出是其上下文的函数。给它决定答案所需的上下文，结果就朝项目想要的方向靠拢；饿着它，它就用自信的猜测填补空缺——"看似合理却是错的"工作正是从这里来的。

这种不对称正是要点。更多上下文有代价（噪音、注意力被稀释、token）；而*缺少决定答案的那部分上下文*没有任何好处——只有输。能力再强的模型，在缺少关键信息时依然产出错误的工作；它的上限由它能看到什么决定。

这就是 PCR 分成两半的原因：**积累**那些否则会蒸发的判断（太少必然坏事），并**提炼**它——修剪噪音、保持当前真相的新鲜（太多或过期同样坏事）。

---

## 为什么仅有代码已经不够

代码记录的是**结果状态**：系统最终长什么样。它在结构上丢掉了协作者需要的三样东西：

1. **被否掉的路径。** 代码只显示"我们选了 A"，从不显示"我们考虑过 B 和 C；B 因为 X 被毙了"。于是下一位协作者看到 A，问"为什么不用 B？"，试了 B，撞进同一堵墙。
2. **一个选择的状态。** 这是深思熟虑后已关闭的决定，还是等待重审的权宜之计？两种情况下代码看起来一模一样，但它们要求截然相反的行动。
3. **一个判断的来路。** 它建立在哪些约束、哪些权衡、谁的拍板之上？约束变化时，决定可能需要重开——但前提是你记下了它悬在什么上面。

在前 AI 时代，这些住在维护者的脑子里，靠**连续性**传递：code review、传帮带、"去问写它的人"。团队是连续的；知识虽然隐性，却不断线。

AI 协作者**没有连续性**。每个会话都是一个失忆的、能干的、且*自行其是*的新人。它不会"去问写它的人"——它自己推理、自己怀疑、自己行动。隐性知识对它而言等于不存在。所以那层一直存在、却藏在人脑中的判断层，现在必须变成**显式的产物**——否则它每个会话蒸发一次，永远如此。

PCR 就是那个产物。它保存的不是*代码是什么*，而是*判断是如何达成的*——让已经付过成本的思考不必再付一次。

---

## 把住方向盘

AI 的迭代速度超过任何人的审阅速度。这逼出一个两难：每一步都审，你成为瓶颈，速度被抹平；什么都不审，工作就悄悄偏离你想要的方向。

PCR 是一条出路。人在少数几个持久的点上设定方向——那些他背书（vouch）的记录——AI 在这些轨道内全速行驶。控制方式从"审阅每个动作"（无法扩展）变成"持有方向"（可以扩展）。盖章就是转向输入：一个已背书的决定不会在每个会话被无故重开，所以你做一次的决定会一个会话接一个会话地持续塑造工作，而不是每次被重新争论。

所以 PCR 也是一种 **harness**：把执行速度交给 AI，同时人把住方向盘。稀缺的人类动作从"亲自做事、逐行检查"转向"设定并维护 records 所编码的方向"。

---

## 无人值守的运行

对 PCR 最严苛的检验是循环（loop）：让 agent 按迭代运行——计划、构建、测试、修复、重复——迭代之间没有人介入。它是这套方法论的读者的极限形态——失忆频率最高、监督最少——而 PCR 正是让这样一次运行可转向、可审计的东西。

**开跑前**，人记录并背书方向——goal 与架构赌注——而每个会话都必须遵守的指令和机器可检查的约束留在仓库中更可靠的存放处：已背书的 records 是循环不得翻案的方向，没有盖章的部分则明确授权给循环。**运行中**，records 是循环跨迭代的 prose 记忆，它自行保养自己的未盖章层，绝不触碰已背书的层。**结束后**，records 是审计轨迹：循环以起草一份提炼收尾，回来的人读到的是一份判断的 diff，而不是两百份会话记录。而且再多的循环也不产生任何背书——验证是写进 prose 的证据；章要等人来盖。agent 侧的规则住在 block 的 **Unattended** 条目里；完整的推理在 [unattended-runs](./.agents/docs/unattended-runs.md)。

---

## 它在整体中的位置

```
Guiding philosophy   Context Engineering   — curate what's in the model's context
        └ Methodology   Project Context Records   — persist the project's slice of it
                └ Mechanism   the provenance stamp   — mark direction a human explicitly accepts
```

---

## 老树发新枝

PCR 是 **Architecture Decision Records（ADR）** 在 AI 时代的后裔——ADR 是 Michael Nygard 于 2011 年提出的约定，如今已发展出[完整的工具与模板生态][adr-hub]。一条 ADR 把每个重要决定记录为一个小的、编号的、随版本管理的文件，写明其*背景*、*决定*与*后果*；已定案的记录从不修改——要改变它，就写一条新的去**取代（supersede）**它，留下一条只增不改的轨迹。

PCR 保留了 ADR 最好的直觉——*知识住在仓库里，随代码一起被审阅和版本化，而不是在 wiki 里*——并为新读者做了三处调整：

1. **决定 → 上下文。** ADR 以"每文件一个重要决定"为中心，附其背景与后果。PCR 把单位放宽到整个元层：决定*加上*架构、心智模型、刻意的偏离、坑、以及进行中的计划。决定只是项目上下文的一个切片，不是全部。
2. **不可变叠加 → 单一且新鲜。** ADR 通过冻结每个已定案文件、追加新文件取代旧文件来保存历史；当前真相散落在整条取代链上。PCR 把**当前结论放在一个新鲜的地方**，让 **git** 保存演化史。让一个失忆的 agent 重读整条取代链去找今天的答案是纯浪费；给它一个可信的答案，把历史送进日志。仍然影响当前决定的理由留在当前条目里；只有附带的演化过程进 git。
3. **读者 = 人 → 读者 = 自行其是的失忆 agent。** ADR 只做描述，因为人读了后果会自我约束。agent 则会"发现"一个已定案的事项并对它采取行动。所以 PCR 条目可以带有**对 agent 的行为指令**（"这在契约之外；不要再标记它"），而不只是描述。

---

## 记录哪些内容

项目的**元层**：它为什么长成这样、架构、维护者决策、意图、刻意的偏离、心智模型、付出过代价的坑、以及进行中的计划。

负定义往往更锋利：**关于这个项目为真、尚未以更可靠的形式持久保存、代码本身无法告诉你、且在当下之后仍然有用的任何东西。**

PCR 不应成为每条约束的首选存放处。如果机器能够检查，就把约束写进类型、测试、lint 或 CI，让 record 只解释背后的理由和何时应重新考虑。如果一段理由只影响一个代码位置，就把它放在代码旁；需要更深背景时再链接到 record。临时执行状态放进 issue 或一份持续覆盖的当前计划。PCR 留给仍然需要用 prose 表达的跨模块判断、意图和其他背景（[records 与 enforcement](./.agents/docs/records-vs-enforcement.md)）。

同一个测试也从另一侧作用于 agent 指令文件（`AGENTS.md`）。那个文件是 **push**——每一行在每个会话都进入模型的上下文，不管用不用得上；records 是 **pull**——工作触及时才读取。所以指令文件的每一行要过一个更硬的测试——*这条必须每个会话都遵守吗？*——过不了但仍然重要的东西就下沉为一条 record。PCR 顺带也是指令文件的泄压阀。

大多数仓库已经握有这一层的碎片——根目录的 `ARCHITECTURE.md` 或 `DESIGN.md`、一个 `adr/` 文件夹、内部文档。它们本来就是 records——**登记（enroll）它们**：用 map 路由指向确切文件或 heading，并遵守同样的规则——而不是搬动它们，或起草会渐行渐远的孪生副本（[existing-docs](./.agents/docs/existing-docs.md)）。

捕获是**宽口径**的——顺手、便宜地记下任何可能有用的东西，包括转瞬即逝的计划和进行中的推理。价值在之后的**提炼**（见下）时评判，不在捕获时评判：留下来的是在当下之后仍然有用的残余。要随 record 留存的证据也必须真的能留下：优先使用测试、可复现命令、已提交的产物、稳定 URL 和 commit hash，而不是临时文件或单次会话输出。有一条边界：records 与承载它的仓库同样公开。人在会话里说的话不自动等于可发表——秘密不要写入；当理由依赖私密背景（未发布的计划、涉及的人、商业约束）时，先问再记。

---

## 起手记录集

"记下任何值得保留的东西"没有给新采纳者第一步棋，而空的 records 文件夹在第一天毫无回报——恰恰是采纳者决定这套实践值不值得坚持的时刻。所以 block 推荐了一份起手清单，**the basics**：`goal.md`（它要成为什么、为谁、以及 non-goals）、`technology-stack.md`、`architecture.md`、`conventions.md`、`gotchas.md`，以及——面向有视觉表面的项目——按 [design.md](https://github.com/google-labs-code/design.md) 格式放在根目录的 `DESIGN.md`。每一条装的都是别处装不了的东西——goal 记录装着面向用户的 README 不会写的意图与拒绝；stack 记录装着 manifest 说不出的 why——逐条的理由在 [starter-set](./.agents/docs/starter-set.md)。

`/pcr-setup` 在采纳时起草其中适用的部分——从代码库和历史里，或在全新空仓库上从你的简述里——交由人纠正并背书：第一天结束时你得到一具已审阅的骨架，而不是空文件夹。这些是提示，不是模式：不适用的跳过、超出单个文件的拆分、命名随意。清单的增长方式与 PCR 中一切相同——一个主题加入，是因为真实使用不断要求它。

---

## 找到那条记录：map

records 只有在读者于正确时刻打开正确部分时才有用。文件少而短时，文件名就是索引；文件或单个 ledger 变长后，agent 不再读完全部，开始靠猜。这个缺口——从你面前的工作到与之相关的确切 record 或 heading——就是检索问题。

答案是一张 **map**，但仅当检索真的需要时：找到确切背景不再是一眼的事、某条 record 变成长 ledger、或登记的记录住到文件夹之外时，就蒸馏出 `.agents/docs/README.md`。每条路由写明代码区域或热点、链接到确切 record 或 heading，并给出一句话要点。密集 record 可以通过多个 heading 链接出现；map 只做路由，不装内容。代码也可以反向路由：热点处的一行注释（`// why: see .agents/docs/<topic>.md#heading`）恰好在有人读那段代码时触发——map 覆盖区域，代码旁的链接覆盖热点。

为什么是一个 map 文件而不是就近放置或 scope 标签、为什么第一天没有 map、以及如何保持路由新鲜，都记录在 [the-map](./.agents/docs/the-map.md)。

---

## 机制：盖章（provenance stamp）

这是唯一的硬通货，它建立在一条第一性原理上：

> 在 AI 时代，文本是廉价的，**默认是 AI 写的**。稀缺而有价值的动作，是**一个人明确为项目方向负责。**

所以规则是单个比特：

- **没有章 = AI 积累。** 默认基底。视为可挑战——尽管质疑、自由验证。
- **`[VOUCHED @handle 2026-07-08]` = 这个人明确接受它所覆盖的文字作为当前项目方向。** 这份方向可以作为基础：不要无故重开，只在有新证据、约束变化或人发话时重开。背书不证明经验事实为真；事实仍需持久证据，工作依赖它时仍可复核。章放在非 heading 行末时覆盖该行；单独成行作为非文档标题 heading 后的首个非空行时覆盖该节；单独成行作为文档标题后的首个非空行时覆盖整个文件。不要把新章放进 heading 文本，否则会破坏 map 的锚点。人读过文字或没有反对永远不算背书。当前改动新加的章只是一项自称，直到相应的人明确确认；目标分支上原本就有、且当前改动未改变的章属于继承的项目状态。旧的无日期章仍视为已背书，但只有人在之后重新背书时才能补日期。

```
Timestamps are stored as UTC, converted only at the edges — settled after a DST bug.   [VOUCHED @hyf0 2026-07-08]

Raising the cache TTL to 1h is probably safe.   ← no stamp: AI-accumulated, verify freely
```

**每个章只覆盖一种明确范围。** 实质性修改已背书的行、节或文件会让章脱落，直到有人重新背书——否则 agent 可以改写方向、让新的字戴着人从未给过的章。修改 heading 层级、插入或删除边界 heading、移动章或重新断行，只要改变了章覆盖哪些文字，也属于实质性修改；只有覆盖的文字集合完全不变时，格式修改才能保留章。位置区分单独一行的章：文档标题后的首个非空行表示整个文件；其他 heading 后的首个非空行表示该节，直到下一个同级或更高层级的 heading。旧式放在文档标题之前的独立章仍覆盖整个文件。旧式放在 heading 文本里的章保留项目原先明确规定的范围；如果项目没有写清楚，就维持更新前的解释，并在工作依赖它时指出歧义。除非相应的人重新背书或明确批准迁移，否则不要移动或重新解释旧章。

**日期只让年龄可见，不会自动判断是否过期。** 它仍是同一个比特，只是加了时间戳——不是一种新章——告诉审阅者这份方向最后一次何时被背书。日期本身无法说明它覆盖哪些代码，也无法证明文字仍然为真；map 路由、代码旁链接、持久证据与[提炼流程](#工作流程积累--提炼)共同让比较成为可能（[freshness](./.agents/docs/freshness.md)）。

**对于记忆，人的章是可选的；对于明确的人类方向，它是必要的。** agent 积累的基底本身已经承载记忆：agent 继承已记录的内容，无论是否被背书。章额外提供的是[把住方向盘](#把住方向盘)里的那个 harness——人有意让它跨会话保持的方向。所以在值得的地方背书，其余保持诚实的默认状态。

**为什么是章，而且只有一种。** 一个由 AI 维护的知识库最糟的失败方式，是 AI 自己的提议被当成人接受的方向——后来的 agent 把机器造出的假设当作定论并在其上继续搭建。章画出的正是这条线，也只有这条线：**有人明确接受，或者没有。** 它不能代替事实证据。更细的区分——*是决定还是观察？定案了还是暂定？*——属于条目自身的文本，不属于更多种类的章。从这一种开始；只有真实使用证明需要时才增加。

---

## 工作流程：积累 → 提炼

- **积累**（便宜、默认、由 agent 做）：上下文出现的那一刻就记下——一个决定敲定、一个坑让你付了代价、一个人纠正了你——以及每当有人要求时；你的修改触及既有记录时保持其新鲜。数量没关系；噪音在预期之内。记了什么要说一声——人看不见的东西，人无法修剪也无法背书。
- **提炼**（稀缺、人主导）：一次审阅——**提升**有价值的、**修剪**错误和过期的，并请人为应继续保持的方向**背书**——背书是 agent 无法代劳的那一部分。事实仍由持久证据支持。这也是"临时跟踪的实施计划"变成"留下来的有价值之物"的地方。

提炼是人的动作，但不必从零开始——人的注意力正是 PCR 要节约的稀缺品，一个要求亲笔撰写审阅的流程是会锈死的阀门。所以那个负责积累的 agent 同样**起草提炼**：一份供人审阅的 diff，提议修剪什么、合并什么、提升什么，外加可能因相关内容变化而需要复核的背书、承重却未背书的方向、以及持久证据已经失效的事实断言——完整分类在 [distill-draft](./.agents/docs/distill-draft.md)。人批准并修改草案，只为自己明确接受的方向背书。无人值守时，agent 只整理未盖章层，其余排队等人；见[无人值守的运行](#无人值守的运行)。

---

## 写作约定

- **一个主题一个文件。** 相关条目用标准的相对 Markdown 链接互链（`[other-topic](./other-topic.md)`）——在 GitHub 上可点击、无歧义、与工具无关。长 ledger 应以一份简短索引指向重要 heading。
- **一旦有了 [map](#找到那条记录map)，保持其中的路由完整。** 找不到的背景就是没人读的背景：新增或改名 record 或已路由 heading 时，在同一次修改里更新 map。
- **保持当前真相新鲜。** 漂移是致命风险：一条与现实不再相符、却依然自信的记录，会从资产翻转为**陷阱**——agent 会满怀信心地照它行动。过期的记录比没有记录更糟。代码与 record 相悖时，判断是实现偏离了既定方向，还是描述已经过期，然后更新过期的一边。已背书的冲突要摆到人面前，而不是无声地覆盖。
- **让证据能够留下。** 测试、可复现命令、已提交产物、稳定 URL 或 commit hash 可以支持日后审计。`/tmp` 路径、缺失的截图或单次会话结果做不到；要么把它标成临时观察，要么保存产物。
- **记下 why**，不只是 what：权衡、被否掉的替代方案、已知的坑。以原理或直觉开头。
- **写到协作者无需阅读整个代码库也能行动。** 先写当前结论与适用范围；必要时再补理由、证据和重新考虑它的条件。
- **不设固定格式——有意如此。** 一条记录就是传达 why 的散文。更严格的形态可能从真实使用中长出来；不要预先强加。

---

[adr-hub]: https://adr.github.io/
