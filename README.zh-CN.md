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

然后在任意项目里运行 `/pcr-setup` 即可采纳 PCR——以后随时重跑即是更新：它会把 block 同步到最新版本，并且绝不碰你的 records。全局安装（`-g`）让这个命令在你所有项目里可用。（技能安装由 [skills.sh](https://www.skills.sh) 提供。）

**或者手动来**——把下面这段粘贴进你项目的 `AGENTS.md` / `CLAUDE.md`（把路径改成你实际存放记录的目录）：

```
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyf0/project-context-records. PCR keeps the project's durable design context — the *why*, the decisions, the architecture — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where they live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links (`[name](./name.md)`). A `README.md` there is the **map** — each record listed with the code it covers, kept in sync with the folder; once the folder outgrows a glance, distill one.
- **Read first.** Start from the map if there is one, else scan the folder. Open what covers an area before you change it — or answer for it.
- **Record as you go.** Write down context worth keeping the moment it appears — a decision lands, a trap costs you, a human corrects you — and whenever a human asks. No required format, no fixed list of what qualifies: if it's true about this project, not visible in the code, and useful beyond the moment, it's worth a record. Mention the records you add or change — what a human never sees never gets vouched.
- **Keep it fresh.** If your change affects a record, update it in the same change — a stale record is a trap, not an asset. When the code contradicts a record, fix the record; if it's vouched, surface the conflict instead of silently overriding.
- **Provenance.** An unstamped line is AI-accumulated: challenge and verify it freely. A `[VOUCHED @handle]` stamp (on a line, or at the top of a file) means a human vouched for it — treat it as settled; reopen or re-verify only on new evidence, a changed constraint, or a human's say-so. Add a stamp only on a human's explicit instruction, and date it when you do (`[VOUCHED @handle 2026-07-08]`); reading past a line, or not objecting, is not a stamp. A stamp covers the words it sits on: materially edit a vouched line and the stamp comes off until a human re-vouches; formatting-only changes keep it.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human review pass. Draft it for them: propose what to prune, merge, or promote, and flag vouches older than the code they cover — the human approves and vouches. Finding is yours; deciding is theirs.
- **Unattended.** With no human between iterations: keep the running plan as one live record, overwritten as truth changes; tidy your own unstamped layer — merge duplicates, prune dead notes — never the vouched one; when evidence argues with a vouched call, record the conflict and stay inside the call unless progress becomes impossible; end the run by drafting the distillation for the human who returns, conflicts included. No run, however long or green, vouches anything.
- **The basics.** The one fixed list — nearly every project needs these; draft the missing ones that apply:
  - `goal.md` — what this project is trying to be, for whom, and what it deliberately is not (the non-goals). The most upstream record; if the README already states it all, give it a map row instead of writing a twin.
  - `technology-stack.md` — why these tools over the defaults, what must not be introduced, what is pinned and why; not a manifest dump.
  - `architecture.md` — the units, the boundaries between them, and why the lines are where they are.
  - `conventions.md` — deliberate departures from ecosystem defaults, so they read as decisions.
  - `gotchas.md` — traps already paid for, each with its why.
  - `DESIGN.md` — only for a project with a visual surface: its visual identity for coding agents — design tokens plus their why — per the design.md spec (google-labs-code/design.md); lives at the root, enrolled in the map.
```

这一段就是采纳的全部。它把每位协作者——人或 agent——引到 records，并写明必须遵守的规则。它有意写得很薄：agent 每个会话都会自动读取 `AGENTS.md`，但**不会**去抓取 URL，所以写进来的只有每个会话都必须遵守的规则——外加少数几个否则永远到不了采纳项目的引导触发器（蒸馏出一张 map、从基础记录写起）；其余内容都留在一个链接之外，agent 无需抓取也能正确工作。这个 block 还属于方法论、不属于项目：重跑 `/pcr-setup` 会整块覆盖它（只有你的 records 目录路径会被保留），所以项目自己的规则要放在 block 外面——你的 records 永远不会被碰。

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

对 PCR 最严苛的检验是循环（loop）：让 agent 按迭代运行——计划、构建、测试、修复、重复——迭代之间没有人介入。每次迭代都从失忆开始；没有人中途纠偏。这不是方法论勉强容忍的特例——这是它的读者的极限形态：失忆频率最高、自主行动监督最少。有三件事因此改变形状。（agent 在这种情况下的规则住在 block 的 **Unattended** 条目里——那是采纳项目的 agent 唯一读得到的文本；本节是 why，以及人的那一半。）

**循环开始前，人靠背书来转向。** 必须在一百次迭代中存活的方向，在第一次迭代前写下并背书：goal 记录——它要成为什么、以及 non-goals——架构赌注写成 `architecture.md`（一条以赌注形态出生、随代码成长为描述的记录），硬约束写进 block 之外的指令文件，在那里它们每个会话都生效。在一个全新的空仓库上，这些方向本身就是种子；`pcr-setup` 会从你的简述里起草它们。此后由既有规则完成转向：已背书的记录即已定案，循环不得翻案。盖章机制正是为此而造——设好轨道，然后放手；而且这条边界双向生效——你没有盖章的，就是你授权的：未背书的地带明确属于循环自行决定和修改。如果循环发现证据与某条已背书的判断相悖，它把冲突记录下来留给人，并继续留在轨道之内，除非那条判断让推进变得不可能；它唯一不许选择的是沉默。

**循环进行中，records 是循环的记忆——而未盖章层归它自己保养。** 第 N+1 次迭代继承第 N 次的判断，只能通过 records，否则就无从继承。把当前计划保持为一条鲜活的记录，随真相变化原地覆写——这是"单一且新鲜"规则应用于循环状态；历史交给 git。而因为一段时间内不会有人来修剪，循环自己整理自己的未盖章层——合并重复、删除废弃笔记、保持 map 诚实。已背书的层它绝不触碰：整理自己的工作记忆不僭越任何权威；改动人盖的章则不然。

**循环结束后，records 是审计轨迹。** 循环的退出动作是提炼草稿：你不在时决定了什么、它建议背书什么、提议修剪什么、现实在哪里与已背书的判断起了争执。回来的人读的是一份判断的 diff，而不是两百份会话记录——下一次运行从提炼过、部分已背书的地面起步。

有一条线不动：**再多的循环也不产生任何背书。** 一个被五十次绿色运行验证过的断言仍然是 AI 积累——这是强证据，散文里应当写明——但盖章不是置信度的度量；它是一个人为此负责，而循环里没有人。

---

## 它在整体中的位置

```
Guiding philosophy   Context Engineering   — curate what's in the model's context
        └ Methodology   Project Context Records   — persist the project's slice of it
                └ Mechanism   the provenance stamp   — mark who stands behind a claim
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

负定义往往更锋利：**关于这个项目为真、代码却无法告诉你、且在当下之后仍然有用的任何东西。**

同一个测试也从另一侧作用于项目的 agent 指令文件（`AGENTS.md`）。那个文件是 **push**——每一行在每个会话都会进入模型的上下文，不管用不用得上；records 是 **pull**——工作触及时才被读取。所以指令文件的每一行要过一个更硬的测试：*这条必须每个会话都遵守吗？*过不了这个测试但仍然重要的东西——规则背后的 why、架构、历史、坑——下沉为一条 record，在相关时被读取。PCR 顺带也是指令文件的泄压阀：那些不断堆积的解释，本来就想去那里。

大多数仓库已经握有这一层的碎片——根目录的 `DESIGN.md` 或 `ARCHITECTURE.md`、一个 `adr/` 文件夹、内部文档。它们在所有要紧的意义上都是 records：一条 record 由它遵守的规则定义——保持新鲜、可以盖章、能被找到——而不是由它住在哪个文件夹定义。**登记（enroll）它们**：在 map 里给每一个一行、指向它住的地方，让它遵守同样的规则，不要搬动它——更不要起草一个与它渐行渐远的孪生副本。records 文件夹是你接下来要写的东西的默认家，不是圈住既有内容的墙。

捕获是**宽口径**的——顺手、便宜地记下任何可能有用的东西，包括转瞬即逝的计划和进行中的推理。价值在之后的**提炼**（见下）时评判，不在捕获时评判：留下来的是在当下之后仍然有用的残余。有一条边界：records 与承载它的仓库同样公开。人在会话里说的话不自动等于可发表——秘密不要写入；当理由依赖私密背景（未发布的计划、涉及的人、商业约束）时，先问再记。

---

## 起手记录集

"记下任何值得保留的东西"没有给新采纳者第一步棋，而一个空的 records 文件夹在第一天毫无回报——那恰恰是采纳者决定这套实践值不值得坚持的时刻。但有几个主题几乎在每个项目里反复出现：一个失忆的协作者在第一个会话就希望知道的事。在采纳时就把它们种下，别等它们自己冒出来：

- **goal**——项目要成为什么、为谁、以及刻意不做什么：让范围保持诚实的 non-goals。这是元层里最上游的判断——其余一切服务于它的意图。它的家是一条 record，而不是 README：README 面向用户做说明；goal 记录面向协作者说话，装着用户不需要的部分——拒绝、优先级、why。如果 README 已经把这些都写全了，就[登记](#记录哪些内容)它，别写孪生。
- **technology-stack**——项目用什么构建，以及围绕它的约束。清单本身已经在 manifest 里；让这条 record 挣得位置的是 manifest 说不出的部分：为什么选这些工具而不是它们取代的默认项、什么不许引入、什么被锁定、为什么。record 保存 why；由它支撑的一行式规则（"用 pnpm"、"永不引入 X"）是每会话生效的材料——属于指令文件，由指令文件链接到这里。
- **architecture**——维护者心中系统的形状：单元、单元之间的边界、以及边界为什么画在那里。
- **conventions**——这个项目刻意偏离生态默认的地方，让偏离读起来是决定，而不是等着热心新人来修的事故。
- **gotchas**——已经付过代价的坑：看起来安全其实不然的东西，每个都带上 why。

还有一个条目取决于项目形态：**`DESIGN.md`**，面向有视觉表面的项目。它是向 coding agent 描述的视觉身份——front matter 里机器可读的 design token（颜色、字体、间距、组件），加上其后解释缘由的散文——遵循 [design.md 规范](https://github.com/google-labs-code/design.md)。按该约定它住在仓库根目录：把它[登记](#记录哪些内容)进 map，不要搬动。它的生态自带 linter（`npx @google/design.md lint DESIGN.md`——检查 token 引用、WCAG 对比度、schema 键）；文件存在时保持 lint 干净。没有视觉表面的项目则完全跳过这个文件与 linter。

agent 可以在采纳时从代码库、manifest 和 git 历史起草其中适用的部分——只起草既有文档没有覆盖的：仓库已有的 `ARCHITECTURE.md` 或 `adr/` 走[登记](#记录哪些内容)，不做重复。产出是第一批积累，交由人纠正、并为站得住的部分背书：第一天结束时你得到的是一具已审阅的骨架，而不是一个空文件夹。

这些是提示，不是模式：不适用的跳过，超出单个文件的拆分，命名随意。这份清单的增长方式与 PCR 中一切的增长方式相同——一个主题加入清单，是因为真实使用不断要求它，而不是因为它看起来应该在。

---

## 找到那条记录：map

records 只有在读者于正确时刻打开正确那条时才有用。文件只有几个时这是小事——文件名就是索引，agent 扫一眼文件夹、读完短短几篇即可。到几十个时就不是了：agent 不会每个会话读完所有记录，而"读覆盖你所动区域的那条记录"悄悄假设 agent 已经知道是哪条。它并不知道。这个缺口——从你面前的代码到与之相关的那条记录——就是检索问题，它区分了一套在五条记录时可用的方法论和一套在五十条时依然可用的方法论。

回应是一张 **map**——但仅当文件夹需要时。当找到正确记录不再是一眼的事——十来个文件左右，或者登记的记录住到文件夹之外的那一刻——就蒸馏出一张 map：`.agents/docs/README.md`，每条记录列一行，写明它覆盖的代码区域和一句话要点。只做路由，不装内容——内容留在记录里；map 只负责指。此后 agent 从 map 出发，把面前的工作——要做的修改，或要回答的问题——对到 map 上，打开覆盖它的记录。"先读"从一个愿望变成一次查表。

map 由外向内路由；代码可以由内向外路由。当一条记录解释了一段代码自己说不出的东西时，在那个位置留一行指向记录的注释（`// why: see .agents/docs/<topic>.md`）。它恰好在有人——人或 agent——读那段代码时触发，比任何索引都更精准：map 覆盖区域，面包屑覆盖热点。

map 本身也是一条记录，但它是提炼出来的，从不用于堆积：你不往里倒笔记，而是在一条记录挣得位置时把它的一行提升进来。它可以像任何记录一样被背书——一张已背书的 map 是很强的转向装置，是维护者自己的"什么重要、在哪里"的索引。

它的维护属于便宜的那种漂移。一条散文记录会无声地腐烂——你只有拿它对照代码重读才发现它错了。map 只会在两条轴上腐烂——记录存在但未列入，或某行指向被改名、被删除的记录——两者都能靠机械地把 map 与文件夹对照来发现。昂贵的漂移留在记录里；map 的漂移是一次 lint。

而且第一天没有 map，这是设计使然：给三条记录配一张 map 是仪式——在结构产生回报之前先付结构税。这是 PCR 自己的规则应用在自己身上——结构在真实使用提出要求时加入，而不是提前。

---

## 机制：盖章（provenance stamp）

这是唯一的硬通货，它建立在一条第一性原理上：

> 在 AI 时代，文本是廉价的，**默认是 AI 写的**。稀缺而有价值的动作，是**一个人为一个断言盖上自己的章。**

所以规则是单个比特：

- **没有章 = AI 积累。** 默认基底。视为可挑战——尽管质疑、自由验证。
- **`[VOUCHED @handle]` = 有人为它背书。** 视为地基：不要为验证而验证、为重开而重开——只在新证据、约束变化、或人发话时才做。章可以标在单独一行上（行尾），或整个文件上（文件顶部），它代表明确的人类背书：由人亲手输入，或由 agent 仅在人的明确指示下加上。人读过一行而没有反对，永远不算背书。

```
Timestamps are stored as UTC, converted only at the edges — settled after a DST bug.   [VOUCHED @hyf0]

Raising the cache TTL to 1h is probably safe.   ← no stamp: AI-accumulated, verify freely
```

**章盖在它所在的字上。** 实质性修改一条已背书的行会让章脱落，直到有人重新背书——否则 agent 可以改写断言、让新的字戴着人从未给过的章。仅格式层面的修改不影响章。

**章带有日期。** `[VOUCHED @hyf0 2026-07-08]` 记录背书发生的*时间*。它仍然是同一个比特——是打在比特上的时间戳，不是一种新章。它买到的是比特本身答不了的问题：不只是*有没有人背书过*，而是*那次背书现在还算数吗？*一年前盖的 `[VOUCHED]`、盖在一个此后重写过两次的模块上，是过期记录陷阱的最坏形态——看起来已定案，还戴着人的章。日期让[提炼流程](#工作流程积累--提炼)可以机械地标出它——章上的日期对照代码的最近变更——而不靠主观判断。而且它几乎免费：大多数章是 agent 按人的指示敲进去的，agent 知道日期——所以 agent 落章必带日期。人手敲时可以省略；git 之后也能查回来，但读者不该需要考古，想得起就带上。

**人的章是可选的——为了延续，不是为了控制。** agent 积累的基底本身已经承载记忆：agent 继承已记录的内容，无论是否被背书。章额外提供的是[把住方向盘](#把住方向盘)里的那个 harness——跨会话保持的人类方向。所以在值得的地方背书，其余保持诚实的默认状态。

**为什么是章，而且只有一种。** 一个由 AI 维护的知识库最糟的失败方式，是 AI 自己的猜测被当成人确认过的事实——后来的 agent 把机器造出的假设当作定论并在其上继续搭建。章画出的正是这条线，也只有这条线：**有人背书，或者没有。** 更细的区分——*是决定还是观察？定案了还是暂定？*——属于条目自身的文本，不属于更多种类的章。从这一种开始；只有真实使用证明需要时才增加。

---

## 工作流程：积累 → 提炼

- **积累**（便宜、默认、由 agent 做）：上下文出现的那一刻就记下——一个决定敲定、一个坑让你付了代价、一个人纠正了你——以及每当有人要求时；你的修改触及既有记录时保持其新鲜。数量没关系；噪音在预期之内。记了什么要说一声——人看不见的东西，人无法修剪也无法背书。
- **提炼**（稀缺、人主导）：一次审阅——**提升**有价值的、**修剪**错误和过期的、为站得住的**背书**——背书是 agent 无法代劳的那一部分。这是人的章作为一种周期性实践的形态，也是"临时跟踪的实施计划"变成"留下来的有价值之物"的地方。

提炼是人的动作，但不必从零开始——也不应该，因为人的注意力正是 PCR 要节约的稀缺品。一次要求忙碌的维护者坐下来亲自撰写完整审阅的提炼，是一个会锈死的阀门，然后 records 长成一堆未修剪、未背书的存货：带文件夹的噪音。所以那个负责积累的 agent 同样可以**起草提炼**——对 records 过一遍，产出一份供人批准的 diff，按人靠手工很难找全的动作分类：

- **被代码打脸的**——与其描述的代码不再相符的记录（靠逐条对照代码重读发现）；
- **重复的**——应当合并的近似重复；
- **被埋没的**——躺在积累堆里、值得提升的有价值内容；
- **map 漂移**——缺席于 [map](#找到那条记录map) 的记录，或指向已移动记录的 map 行；
- **承重但未背书**——被其他记录或代码依赖、却未盖章的断言，拎出来请人背书或否决；
- **老化的背书**——代码在章上日期之后又变过的已背书记录。

agent 起草；人在一轮里批准、修改、背书。这是把[方向盘](#把住方向盘)调转对准 records 本身：人依然持有方向，但提炼从*撰写*降为*审阅*——这是一个会真实发生的实践与一个停留在良好愿望之间的差别。*谁来背书*没有任何变化：章依然只在人明确加上时才算数。无人值守时——迭代之间没有人——agent 自行整理未盖章层，其余排队等人；见[无人值守的运行](#无人值守的运行)。

---

## 写作约定

- **一个主题一个文件。** 相关条目用标准的相对 Markdown 链接互链（`[other-topic](./other-topic.md)`）——在 GitHub 上可点击、无歧义、与工具无关。
- **一旦有了 [map](#找到那条记录map)，保持它完整。** 找不到的记录就是没人读的记录：新增或改名一条记录时，在同一次修改里更新它在 map 里的那一行。
- **保持当前真相新鲜。** 漂移是致命风险：一条与现实不再相符、却依然自信的记录，会从资产翻转为**陷阱**——agent 会满怀信心地照它行动。过期的记录比没有记录更糟。你的修改影响某条目时，在同一次修改里更新它；代码与某条目相悖时，修正该条目——已背书的除外：把冲突摆到人面前，而不是无声地覆盖。
- **记下 why**，不只是 what：权衡、被否掉的替代方案、已知的坑。以原理或直觉开头。
- **写到协作者不读代码内部也能看懂。** 条目作为散文自成一体；agent 读了就能*领会*。
- **不设固定格式——有意如此。** 一条记录就是传达 why 的散文。更严格的形态可能从真实使用中长出来；不要预先强加。

---

[adr-hub]: https://adr.github.io/
