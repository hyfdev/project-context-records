# Project Context Records（PCR）

[English](./README.md) · **简体中文**

> 把项目的判断——那些*为什么*、决定、意图——作为随代码版本化的档案存进仓库，让每个 session 都失忆的 AI 协作者继承它，而不是重新推导它。又因为档案里保存着人明确盖章认可的方向，它同时是一副缰绳：agent 可以长时间无人值守地跑，而人始终握着方向盘。

## 目录

- [核心想法](#核心想法)
- [采用 PCR](#采用-pcr)
- [日常的 context 实践](#日常的-context-实践)
- [无人值守的 loop 实践](#无人值守的-loop-实践)
- [为什么](#为什么)
- [它在哪一层](#它在哪一层)

## 核心想法

LLM 的输出是其上下文的函数。这句话真正要紧的地方在于它的不对称性：缺了那条决定答案的上下文，工作就会出错——自信地、貌似合理地出错——多强的模型能力都补偿不了。对的上下文越充分，工作的上限越高；缺了决定性的那条，上限被硬生生封死。

决定答案的上下文大多是判断，而代码承载不了它。代码记录的是结果状态——系统最终长什么样——并结构性地丢掉其余：哪些路径被否决、为什么，一个选择是定论还是权宜之计，一个判断建立在什么之上。这一层过去住在维护者的头脑里，靠连续性传递：code review、传帮带、"去问写它的人"。AI 协作者没有连续性。每个 session 都是一个失忆的、能干的、自作主张的新人，隐性知识对它来说等于不存在。

PCR 就是把这一层作为显式工件、随代码一起版本化的实践：

- **记录（records）** 随工作廉价积累，纯 Markdown——没有强制格式，没有仪式。
- 人对应当持续起作用的记录**盖章（vouch）**。一个章，一个比特——人接受的方向，或可自由质疑的 AI 笔记。这是方法论唯一的硬机制。
- **蒸馏（distillation）** 让档案保持可读：agent 起草删什么、合什么、提升什么；人来裁决。
- 结构是**渐进的**：具名文件、格式、索引只在使用需要时出现，绝不预先强加。

同一份档案也正是让长时间无人值守运行可驾驭的东西：有章的记录是护栏，记录是循环跨迭代的记忆，run 结束时留下一个回来的人读得懂的状态。Context Engineering 是指导思想——模型看到什么决定它做什么。PCR 是这个思想在项目尺度上的实践。loop 是它兑现的地方。

## 采用 PCR

**用 setup 技能**（推荐）：

```
npx skills add hyfdev/project-context-records -g
```

然后在任意项目里运行 `/pcr-setup`。之后要更新一个已采用的项目，先刷新技能，再重新运行：

```
npx skills update pcr-setup -g
```

`npx skills` 拉取最新的方法论；在项目里运行 `/pcr-setup` 把它应用进去。（技能安装由 [skills.sh](https://www.skills.sh) 提供。）

**或者手动**：把下面的块粘贴进项目的 `AGENTS.md`；如果你的 records 目录不在默认位置，把 "Where records live" 一条指向你的目录。

这个块就是**全部的采用面**。已采用项目的 agent 每个 session 都读 `AGENTS.md`，并且从不抓取本仓库：必须到达它们的内容都在块里，此外的一切都是写给人的。因此块为完整性优化，而不是为简短——agent 必须遵守的每条规则都以完整力度住在块里，因为不存在其他通道。块里点到的一切——地图、印章、决定台账、loop 文件——在后面的章节都有解释。它特意住在 `AGENTS.md`——正在成形的跨工具 agent 指令标准——一个文件到达所有 agent；把 `CLAUDE.md` 及其同类保持为指向它的符号链接。marker 划定所有权边界：重新运行 `/pcr-setup` 只替换 `<!-- PCR:START -->` 与 `<!-- PCR:END -->` 之间的文本，继承你的 records 目录路径，并且从不修改已有记录——它仅有的两个记录侧动作（向空目录播种草稿、把遗留的 `goal.md` 更名为 `intent.md`）都只在你批准后发生。项目自有规则放在 marker 之外。

```
<!-- PCR:START -->
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyfdev/project-context-records. PCR keeps the project's durable judgment — the *why*, the decisions, the intent — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where records live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links.
  - A `README.md` there is the **map**: it routes code areas or hotspots to the exact record or heading, one-line gist per route. Create it when retrieval stops being a glance or one record grows into a long ledger.
- **Read first.** Start from the map if present, else scan the folder. Open the records or headings that cover an area before changing or answering for it; if the area has a decision ledger, read it first.
- **Use the strongest durable form.** Machine-checkable constraints go in types, tests, lints, or CI; rules that must bind every session go in the agent-instructions file, outside the markers; single-spot rationale goes beside the code with a link; records carry the cross-cutting judgment, intent, and context that must stay prose.
- **Record as you go.** Capture context when a decision lands, a trap costs you, a human corrects you, or a human asks — anything true about this project, not durable in a stronger form, and useful beyond the moment.
  - Report what you record so a human can review or vouch it.
  - Records are as public as the repo: keep secrets out, and ask before recording rationale from private context.
- **Write to be acted on.** Lead with the current conclusion and where it applies; capture the why — trade-offs, alternatives rejected, known pitfalls. Keep each topic's current truth in one fresh place, updated in place: evolution belongs to git, never to supersede chains.
- **Keep it fresh.** Update affected records in the same change that touches their subject.
  - When code and a record disagree, decide which side went stale and fix that side.
  - Back facts with durable evidence — tests, reproducible commands, committed artifacts, stable URLs, commit hashes — not ephemeral paths or one session's output.
- **Provenance.** Unstamped text is AI-accumulated: challenge and verify it freely. `[VOUCHED @handle YYYY-MM-DD]` means the named human explicitly accepted the covered words as current project direction.
  - A vouch is direction, not proof: facts keep needing durable evidence. Don't reopen vouched direction for its own sake — only on new evidence, a changed constraint, or the human's say-so.
  - When evidence argues with vouched direction, record the conflict and surface it to a human; stay inside the direction unless progress becomes impossible. Silence is not an option.
  - Scope: at a non-heading line's end, the stamp covers that line; alone on the first nonblank line below a heading, that section until the next heading of the same or higher level; alone below the document title, the whole file. Never in heading text — link anchors derive from headings.
  - Add a stamp only on explicit instruction. A stamp added by work under review counts only once the named human confirms it; an unchanged stamp on the target branch is inherited project state.
  - The stamp binds the exact covered words. Any edit that changes them — or changes which words the scope covers — removes the stamp until the human re-vouches; a change that leaves the covered words identical keeps it.
  - Legacy stamp forms (undated, before the title, inside a heading) stay valid with their original scope; never move, re-date, or reinterpret one without the human's approval.
- **Decision ledgers.** When the human declares that an area records decisions, keep that area's judgments in `<area>-decisions.md` and register new judgments there.
  - Placement: beside the area's derived document (`DESIGN-decisions.md` beside `DESIGN.md`, typically both in the records folder); with no derived document, in the records folder — a map route either way.
  - You may propose opening a ledger; only the human opens one.
  - The register contract, stated at the top of the file: only judgments the human actually expressed enter — a finished implementation, a passed review, resemblance to a reference, or silence is not acceptance. Never invent a rationale: if no reason was given, the entry says so.
  - Record the act of judgment, not the chosen thing's full content — exhaustive detail lives in the area's own document, linked. Edit entries in place; git keeps history.
  - Entries sit under **Decided** or **Open**. An Open entry marks a known-undecided question — current behavior is not a choice — with any stopgap and what would settle it. A Decided entry carries:
    - a short stable topic heading — map routes and stamp scopes anchor to it;
    - **Ruling:** one plain sentence, its force in its own wording — must / never / prefer / default to; no status field;
    - **Limits:** what it does not govern, what may change without reopening it, what would reopen it — a stopgap is a ruling plus its reopen condition;
    - **Why:** premises, alternatives compared, rejections — exactly as the human gave them;
    - **Source:** who expressed it, when, a durable pointer; for "accept the reviewed thing as a whole", pin the thing (commit hash, spec section) instead of transcribing it;
    - the vouch stamp, once the human vouches the entry, alone under the entry's heading — covering the whole entry.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human pass, and you draft it.
  - Propose: prune what is contradicted or dead, merge near-duplicates, promote buried context, fix map drift. Unattended, apply this to your own unstamped layer as you go — never the vouched one.
  - Flag: unstamped direction that has become load-bearing, factual claims whose evidence no longer holds, vouches plausibly affected by changes to what they cover.
  - The human decides and vouches.
- **Suggested topics.** Draft the missing ones that apply; when an existing doc already covers a topic, enroll it — a map route pointing at it where it lives, held to these same rules — instead of drafting a twin:
  - `intent.md` — what this is trying to be, for whom, and the non-goals; enroll the README instead if it truly covers them.
  - `technology-stack.md` — why tools, restrictions, and pins exist; not a manifest dump.
  - `architecture.md` — units, boundaries, and why the lines are where they are; when structure isn't glanceable.
  - `gotchas.md` — traps already paid for, each with its why; only real paid lessons.
  - `DESIGN.md` — only for a visual surface; follow https://github.com/google-labs-code/design.md (records folder by default — the spec fixes no location), enroll it in the map, and suggest wiring its linter into the project's own checks with the file's actual path (e.g. `npx @google/design.md lint .agents/docs/DESIGN.md`; platform variants in the spec).
  - `loop-goal.md` — only for an unattended run: the run's contract — goal, boundaries, finish criteria. You may draft it; the run starts only once the human has vouched the whole file (stamp below the title), and a human edit plus re-vouch re-baselines it. Never edit it yourself; if the contract itself blocks progress, stop and surface the conflict rather than stepping outside it.
  - `loop-status.md` — only for an unattended run: the run's memory — done, in flight, next, blocked — overwritten in place each iteration; its final overwrite is the handover to the returning human (what landed, what to vouch, what to prune, conflicts included). Both `loop-*` files die after the human's distillation pass over that handover; git keeps them.
<!-- PCR:END -->
```

然后就正常干活：自由积累，review 时蒸馏，给应当持续起作用的方向盖章。

## 日常的 context 实践

### 记录：自由底座

记录住在仓库里——默认 `.agents/docs/`——一事一文件，用相对 Markdown 链接互联。一条记录就是承载"为什么"的散文；没有强制格式。

什么配得上一条记录：关于这个项目为真、代码本身说不出、没有更强的家可去、且在当下之后仍然有用的任何东西——带着被否决备选的决定、架构理由、对生态默认的有意偏离、付过学费的陷阱、进行中的计划。

"没有更强的家"是一道真实的测试，先做：

- 机器可查的约束放进类型、测试、lint 或 CI。记录可以解释约束为何存在；它不是执法者。
- 只关乎一个代码热点的理由放在那段代码旁边，完整推理太大时链接出去。
- 临时执行状态放进 issue 或一份可整体替换的活计划。
- 剩给记录的：横切的判断、意图、必须保持散文形态的上下文。

同一道测试从另一侧检验 agent 指令文件（`AGENTS.md`）。那个文件是推送——每一行每个 session 都进入模型上下文，不管用不用得上。记录是拉取——工作触及时才读。所以指令文件的每一行要过一道更严的门槛（*这条必须每个 session 都被遵守吗？*），过不了这道门槛但仍然要紧的内容都下沉为记录。PCR 也是指令文件的泄压阀。

捕获是宽的、便宜的：决定落地时、陷阱让你付出代价时、人纠正你时、人要求时，随手记。让记录在触及其主题的同一个变更里保持新鲜——过时的记录比没有更糟，因为 agent 会带着全部自信执行它。代码和记录不一致时，判断哪一侧过时了、修那一侧；记录带章时，把冲突呈给人而不是悄悄推翻。证据要耐久：测试、可复现命令、已提交工件、稳定 URL、commit 哈希——不是临时路径或一次 session 的输出。

两条边界。记录与承载它的仓库同样公开：秘密不进记录；当理由依托私密上下文时，先问再记。而已经承载这一层碎片的仓库——根部的 `ARCHITECTURE.md`、`adr/` 目录、内部文档——**登记（enroll）**它们于原地，用一条地图路由指向确切的文件或标题（见[地图](#地图)），而不是迁移它们，或起草一对会互相漂移的双胞胎。

### 建议话题

空文件夹给不出第一步。这些名字消除"该建什么文件"的开销；每个都带着适用条件，跳过是正常的。它们是提示，不是 schema：

- **`intent.md`** —— 这个项目想成为什么、为谁、以及让范围保持诚实的 non-goals。几乎每个项目都适用；README 真的都讲了就登记 README——它通常向用户推销，而 intent 面向协作者。
- **`technology-stack.md`** —— 为什么是这些工具而不是被它们取代的默认、什么不许引入、什么被钉住及其原因。存在工具判断时适用；绝不是清单转录。
- **`architecture.md`** —— 单元、单元之间的边界、以及线为什么画在这里。当结构无法从代码一眼看穿时适用。
- **`gotchas.md`** —— 付过学费的陷阱，每个带着为什么。只收真实教训；宁可没有这个文件，也不要编造的"常见坑"。
- **`DESIGN.md`** —— 仅当项目有视觉面：面向 coding agent 描述的视觉标识，按 [design.md 规范](https://github.com/google-labs-code/design.md)——登记进地图，该生态自带的 linter 可用于项目自己的检查。规范不规定位置；records 目录（默认 `.agents/docs/`）是惯常的家，有 design 台账时 `DESIGN-decisions.md` 与它成对放在一起。

### 地图

只有在对的时刻打开对的记录，记录才有用。文件夹还小时，文件名就是索引。一旦检索不再一瞥可得——文件多了、某条记录长成长账、被登记的记录在文件夹之外——就蒸馏出一张**地图**：`.agents/docs/README.md`，把每个代码区域或热点路由到确切的记录或标题，每条路由配一行要旨。地图只路由；内容留在记录里。它也是一条普通记录：新增或更名被路由的记录时，在同一个变更里更新地图。狭窄热点用代码里的一行面包屑（`// why: see .agents/docs/<topic>.md#<heading>`），在恰好的时机触发。第一天不要地图——给三条短记录配地图是仪式。

### 印章

在一份由 AI 维护的档案里，文本是廉价的、默认由 AI 写成。稀缺的动作——唯一只有人能做的——是明确为方向承担责任。印章就是这个动作，而且只有一个比特：

- **无章** —— AI 积累层。默认基底：随意质疑、验证、改写。
- **`[VOUCHED @hyfdev 2026-07-08]`** —— 具名的人明确接受被覆盖的文字为当前项目方向。视为地基：不无故重开——只在新证据、约束变化或人发话时重开。

盖章关乎方向，不关乎真伪。它不使一个事实断言得证；事实始终需要耐久证据。日期记录人最后一次接受方向的时间——看得见的年龄，而非可假定的新鲜。

作用域一口气说完：行尾的章盖住那一行；标题下第一个非空行独占的章盖住那一节；文档标题下独占的章盖住整个文件。它永不进入标题文本，因为链接锚点由标题派生。编辑被覆盖的文字会取下印章、直到人重新盖章——只有让文字一字不差的修改才保章；否则 agent 的新词就会戴着人没给过的印。agent 需要的完整操作规则——新章何时算数、遗留章如何对待——随[采用块](#采用-pcr)走，不在这里。

为什么只有一种章：AI 维护的档案最坏的失败，是 AI 自己的提议被误当作人接受过的方向、然后被继续构建。印章画的正是这条线——明确接受过，或没有。更细的区分（决定还是观察、已定还是暂定）属于条目自己的文本。从一个比特开始；只有真实使用证明需要时才增加。

### 决定台账

有些领域的人类判断以流的形式落下——选择、接受、否决，一次评审接一次评审——同时 AI 把结果综合成规范与实现。这些判断值得一本登记簿，让综合物有处可对账。这本登记簿就是该领域的**决定台账**：`<area>-decisions.md`。

台账**按领域、选择性开启**。只有当人声明该领域要记录决定（"从现在起 design 的决定要记录"）之后它才存在。注意到某领域判断密集的 agent 可以提议开一本；只有人能开。

它的立身纪律是写在文件顶部的**登记契约**：只有人实际表达过的判断才可进入。完成了的实现、通过了的评审、与参考的相似、无人反对，都不是接受。理由永不编造：人没给理由，条目就说没给。

条目分两个区——**Decided**，以及收留已知未决的 **Open**。一条 Open 条目标记"当前行为不是选择"——这恰恰是 agent 无法从别处得知的——并携带问题本身、任何权宜处置、以及什么能了结它。一条 Decided 条目保持一个基本形状，形状之内自由：

- 一个简短、**稳定的议题标题**——稳定是因为地图路由和印章作用域锚定在它上面；
- **裁定**在先：一句白话，力度在措辞本身——*must*、*never*、*prefer*、*default to*。没有 status 字段去复述句子已经说了的事；
- 它的**界限**——它不管辖什么、什么可以改而不算重开、什么会正当地重开它。权宜之计不是特殊状态：它就是一条裁定加上它的重开条件；
- **理由**——前提、比较过的备选、否决——严格按人给出的样子；
- **出处**——谁表达的、何时、有耐久指针就给。当决定是"整体接受评审过的那个东西"时，钉住那个东西——commit 哈希、规范章节——而不是抄录它。

人给条目盖章时，章独占一行放在条目标题之下、盖住整条——所以对任何被盖住部分的编辑都会取下印章，直到人重新盖章。

一条长度纪律防止台账膨胀成第二份规范：**它记录判断这个动作，不记录被选中之物的内容。** 详尽参数住在该领域自己的文档里，从条目链接过去。

没有 superseded 状态。裁定变化时，在同一个变更里就地改写受影响的条目；git 保存演化。

台账常与一份由 AI 维护现势的派生文档**成对**出现：台账保存人裁定过什么；文档保存综合出的当前真相，可对着台账核验。这对配对的视觉实例是 `DESIGN.md` 旁边的 `DESIGN-decisions.md`，通常都在 records 目录里。台账挨着它的派生文档住；没有派生文档时，住 records 目录。无论哪种，地图都路由到它。

这个模式有一个公开的真实前身：见 [musubi 的 `DESIGN-decisions.md`](https://github.com/hyfdev/musubi/blob/v2/DESIGN-decisions.md)——台账正是从这个文件提升而来。它早于上面的格式，而它身上可见的漂移——五值 status 词表在实践中塌缩成一个值、条目膨胀进规范细节、文件底部一段自我发明的格式说明——正是这个格式存在的原因。

### 积累与蒸馏

- **积累** —— 便宜、默认、agent 来做。随手记、保持记录新鲜、并说出你记了什么——人无法修剪或盖章他们从未见过的东西。噪音是预期内的；量大没关系。
- **蒸馏** —— 阀门，人所有、agent 起草。agent 对记录起草一轮可审的处理：删什么、合什么、提升什么；哪些章可能在老化；哪些无章方向已经承重；哪些事实断言失去了证据。人编辑、裁决——并只对自己明确接受的方向盖章。蒸馏是"沿途记下的笔记"变成"留下来的东西"的地方。

## 无人值守的 loop 实践

PCR 服务的最严苛读者不是一个 session，而是一次 run：agent 一轮轮迭代——计划、构建、测试、修复——中间没有人。失忆频率最高，监督最少。这也是实践回报最大的地方：人出现在决定处，缺席于劳动处。

一次 run 由两个文件承载，都在 `loop-` 前缀之下。前缀是生命周期标记：`loop-*` 文件随 run 开始出生、随它的蒸馏死亡——run 范围的状态，与它们身边的项目级记录一眼可分。git 保存它们的历史。

- **`loop-goal.md` —— 契约。** 这次 run 必须达成什么、边界在哪、什么算完成。agent 可以代拟，但 run 只在人对整个文件盖章之后才开始——契约就是有章方向，由与其他一切相同的那种章承载，不是第二条授权通道。**循环永不编辑自己的契约。** 只有人改它，改过并重新盖章的契约使 run 重新立约；若契约本身挡住了进展，循环停下、呈报冲突，而不是越出契约行事。
- **`loop-status.md` —— 记忆。** 做完的、在做的、下一步、卡住的——每次迭代就地整体覆写：一个文件，永远是当前的。第 N+1 轮通过这个文件和记录继承第 N 轮，否则什么都继承不到。

于是启动可以只有一行——*执行 `loop-goal.md` 里的契约*——因为权威在文件，不在提示词。任何能重新唤起 agent 的驱动器都能跑同一个 loop。

一次 run 有三幕：

**跑前，人靠盖章掌舵。** 必须活过一百轮迭代的方向在第一轮之前写下并盖章：`intent.md`、架构赌注、任何已开台账里的裁定、以及 `loop-goal.md` 里的契约本身——同时硬性的 every-session 规则进指令文件、机器可查的约束进 CI，各归其更强的家。边界两面都锋利：有章记录是循环不得翻案的方向，而保持无章的部分是明确的授权——归循环自己决定与修订。

**跑中，记录是唯一的记忆。** 循环读它们、保持它们新鲜、并整理自己的无章层——合并重复、剪除死笔记——但绝不碰有章层。当证据与有章方向相抵时，它记下冲突并留在方向之内，除非进展变得不可能；沉默是它唯一没有的选项。

**跑后，出口是给回来的人的一份视图。** run 的最后一个动作是把 `loop-status.md` 覆写成交接：落了什么、什么值得盖章、什么该删、现实在哪里与有章判断相抵。这最后一次覆写就是文件形态的蒸馏草稿——回来的人读一份判断的 diff，而不是两百份 transcript。没有单独的交接工件；记忆的终态就是交接。

任何 run，无论多长、多绿，都不产生章。验证是关于断言的证据——值得写下。章是人在承担责任，它等的是一个人。

一个 checkout 同时跑一个 loop；并行的 run 各居各的 worktree。

这些文件从中蒸馏出来的那种 run 形态是公开的：[musubi](https://github.com/hyfdev/musubi) 就是这样重建的——人的部分是几十条台账裁定和一声开始；agent 的部分是其间的一切，跨越长时间的无人值守，记录作记忆，每次返回都有一份出口状态。

## 为什么

### 为什么代码不再够用

核心想法一句话点过诊断；这里展开说。代码保存结果状态，丢掉协作者需要的三样东西：

1. **被否决的路径。** 代码显示"我们选了 A"——从不显示"B 和 C 被考虑过；B 死于 X"。下一个协作者看见 A，问"为什么不用 B？"，试了 B，撞进同一堵墙。
2. **选择的状态。** 一个深思熟虑、已经关闭的决定和一个等待复审的权宜之计，在代码里长得一模一样——而两者要求相反的行动。
3. **判断建立在什么之上。** 约束会变。一个决定是否应该重开，取决于它悬在什么上面——只有当初有人记下，才找得回来。

AI 之前，丢失的这一层仍然运转，因为团队是连续的：评审、传帮带、去问作者，让隐性知识不断线。AI 协作者掐断了这条链——而且它不问；它自己推理、自己怀疑、自己行动。所以这层一直存在的判断必须变成显式工件，否则它就一次次蒸发，每个 session 一次，永远如此。

### 握住方向盘

AI 迭代得比任何人能评审的都快。每一步都评审，你就是瓶颈，速度被抹掉；什么都不评审，工作就悄悄漂离你想要的。PCR 的回答：人在少数耐久的点上设定方向——那些有章的记录——AI 在其中快跑。控制从"评审每个动作"（不可扩展）移到"持有方向"（可扩展）。盖过一次章的决定持续塑造工作，一个 session 又一个 session，而不是每次被重新争论。

### 在 ADR 之上

PCR 承自 [Architecture Decision Records][adr-hub]——Michael Nygard 2011 年的约定：每个重要决定一个小的、编号的、版本控制的文件；已定的记录从不编辑，只被更新的记录取代（supersede），留下只增不改的轨迹。PCR 保留 ADR 最好的本能——知识住在仓库里，随代码评审与版本化，不在 wiki 里——并为新读者改了四件事：

1. **决定 → 上下文。** ADR 记录决定。PCR 把单位放宽到整个判断层：架构、心智模型、有意偏离、陷阱、意图、进行中的计划。
2. **不可变堆叠 → 单处保鲜。** 让失忆的 agent 重读一条 supersede 链去找今天的答案是纯浪费。PCR 把当前结论保存在一个新鲜的地方；git 持有演化。
3. **读者是人 → 读者是自作主张的失忆 agent。** ADR 只描述，因为人会读后果、自我约束。agent 会"发现"一个已定之事然后对它下手——所以记录可以携带行动指令（"有意排除在范围外；不要再标"），不只是描述。
4. **决定文件回归，但形态已变。** 当关于一个领域的判断以流的形式到来时，PCR 的决定台账就是被前三条改造过的 ADR：按领域而非按决定立文件、就地编辑而非 supersede、登记人实际表达过的判断而非记录每一个选择。

### 渐进是设计原则

PCR 只在使用需要时增加结构。各层按出现顺序：

1. **自由底座** —— 永远在场：想记什么、怎么记都行，纯散文。
2. **建议话题** —— 消除第一步开销的名字，各带适用条件。
3. **选装模式** —— 决定台账（人声明时）、设计配对（有视觉面）、地图（检索不再一瞥可得时）、`loop-*` 文件（run 开始时）。每个都带着真实使用证明必要的最小格式到来——而且格式随文件下发，不是预先的规则手册。
4. **提升** —— 增长机制本身：在真实项目中反复出现的写法被提升为建议话题或选装模式。决定台账就始于一个项目的 `DESIGN-decisions.md`。没有什么因为"会很好"而进入；见 [CONTRIBUTING](./CONTRIBUTING.md)。

而整个规范保持为散文。采用就是粘贴一个块；PCR 不要求任何软件——没有必装的 CI、bot、解析器、front matter 或 schema。标准靠易于采用而传播——ADR、Conventional Commits、semver——加进规范的每个机制都在给这一点上税。工具可以消费记录，就像 adr-tools 消费 ADR 那样，而约定永不依赖它们。

## 它在哪一层

```
指导思想    Context Engineering —— 模型看到什么决定它做什么
    └ 方法论    Project Context Records —— 项目的那一份：持久化、版本化、可盖章
            └ 机制    the provenance stamp —— 只有人能添加的那一个比特
```

Loop engineering——运行上面的无人值守循环——坐在其上，是回报所在：由有章层驾驭、由记录承载记忆的 run。

[adr-hub]: https://adr.github.io/
