---
name: ml-paper-writing
description: 用导师 Hao Zhu 顶会论文风格写作或修改机器学习算法论文，尤其适用于整合导师反馈和修订已有稿件。提供 Abstract、Introduction、Related Work、Method、Experiments 和 Conclusion 的逐句蓝图、三层关系语法、图表引用规范与模板句库；硬件/系统架构论文的证据、版面与投稿审计优先使用 research-paper-writing。
---

# 使用方法

这是从 Hao Zhu(Data61@CSIRO)9 篇顶会论文逐句解剖出的写作规范。被调用时:

1. **先确认任务对象**:用户在写/改哪个 section?→ 查下文对应蓝图(§1–§6),按"句位|功能|词数|关系"表逐句构造或诊断。
2. **写每一句前过三问**(§0 句子经济学):删掉损失什么?相对上句做了什么动作?推进结论了吗?严禁三样:正确的废话、过度防守 claim、逐格念表。
3. **段落层面**:按 §8.2 的装置分区律排段(Intro 用算子/回指,RW 用段头,Method 用公式回指+组件舱,实验用段头+表锚);因果拐点必须显式化,并列可免算子。
4. **全文层面**:按 §8.3 检查——每章开门 roadmap(Method 必有,Intro/RW 禁用)、欠账全部兑付、主旋律 ≥5 处变奏且换分辨率、结论零数字并复奏一次破立转折。
5. **改稿模式**:先给逐句诊断表(句子|现功能|问题|改法),再给改写;引用本 skill 的规则编号说明理由。
6. 需要逐字例句或完整统计时,读同目录 `references/01–07.md`(01=SSGC+GFB、02=COLES+GLEN、03=CVPR三篇、04=COSTA+SFA、05=Abstract/Intro逐句标注、06=Method/实验逐句+图表引用普查、07=段间关系+跨章缝合+Conclusion)。

规则是通用的;英文例句只是证据,不要照搬图学习领域内容。以下为完整规范。

---

# 论文写作 Skill(通用版)

> 语料:Hao Zhu 9 篇顶会论文(ICLR/NeurIPS×2/CVPR×3/KDD/AAAI/arXiv)的逐句解剖,163 条图表引用句、106 条 caption、约 300 句逐句标注的定量统计。
> 用法:写作时按 section 查对应蓝图;每写一句,先问它的**功能岗位**是什么、与上下句的**关系**是什么。规则是通用的;英文例句只是证据,不要照搬领域内容。
> 逐篇证据与完整例句库在 `references/01–07`(07=段间关系普查+跨章缝合+Conclusion 逐句)。

## 既有稿件修订：先守住版本与改动范围

以下规则只约束已有稿件的修订，不取代用户另行要求的数学审计或研究流程。用户和导师针对当前稿件的明确指示优先于本 skill 从论文语料归纳出的模板。

- **锁定底稿并保护已审阅内容。**先辨认当前稿、导师最新修改稿和工作副本。若导师已改主稿，原样保留该版本，在副本上工作；默认不重写导师已改的论述、结论、结构或格式，除非用户明确授权，或任务明确要求补实验、补结果。用差异对照区分既有修改、用户要求和本轮新增内容。
- **以老师更新的稿件为依据。**老师改过的正文、结构和结论保持原样；按用户要求补实验与结果，并核对这些结果与稿件论断的对应关系。
- **完整列出实验及结果。**逐项写清实际完成的实验及结果，保留已经对上的项目；尚未完成的实验明确标出，不因压缩篇幅而漏列。
- **按用户指定的先后顺序工作。**若任务要求先补齐推导、实验或结果，就先完成并核实这些内容，再写论文 prose、做版式压缩和冗余删减；不要先追逐页数，也不要把尚未执行的检查报告成已完成。明确给出范围后，不为常规可逆选择反复停下来询问；只有底稿或改动边界存在实质歧义时才澄清。
- **以可读性为目标，不掏空论证。**确有重复再删，保留必要的证明链、中间步骤和反例；若用户要求合并附录结构但保持内容，就按要求整理层级并补导航段，不顺手改写技术内容。不要在冗余审查前硬压页数；格式调整后检查引用是否意外减少，并报告重要的页数或引用数变化。用户明确说可放过小问题时，不用为无关紧要的细节扩张修改范围。
- **项目级版式反馈要落到稿件里。**按语义组织图组、收紧过大的留白，避免把太多面板塞进一图，也避免信息量很低的单曲线图；3–6 个相关面板可作常用范围，但不为凑数合并，信息过载就拆开。若用户要求，用 `\noindent\textbf{}` 统一段头；单个公式若无需编号或交叉引用，优先考虑行内或无编号展示。此类偏好服从当前稿件的明确指示，不是所有 venue 的硬规则。


---

## 0. 第一原则:句子经济学

**每一句话必须有存在的理由。"正确"不是写它的理由,"推进论证"才是。**

写完任何一句,问三个问题:
1. 删掉它,读者会损失什么?(答不出→删)
2. 它相对上一句做了什么动作?(支撑/转折/递进/归因/引出……答不出→它是孤儿句,删或重写)
3. 它把读者往结论推近了一步吗?(没有→它在原地踏步)

**三条禁令**(全部有语料量化背书:9 篇正文合计,真废话短语≈0 次、防守性表达≈0 次):

| 禁令 | 禁止形态 | 语料证据 | 替代做法 |
|---|---|---|---|
| **禁"正确的废话"** | "It is worth noting that…"、"As we can see…"、"It can be observed that…"、"众所周知"式铺垫 | 163 条图表引用句中 "we can see" 仅 1 例,且出自唯一没发表的 arXiv 稿;"it is worth noting/obviously/as is well known" 全语料 0 次 | 动词直接落在主语上:"Table 3 shows that…";结论直接开句 |
| **禁过度防守 claim** | "we acknowledge…"、"one limitation is…"预防性道歉、层层限定把结论削没 | "we acknowledge/we do not claim" 全语料 0 次;诚实的对冲集中在附录("The above approximations may be loose…"),**正文强攻、附录坦白** | 防守做成**结构**而非语气:划界句("X, not studied by us, is complementary")、窄域 first 声明、精确等价条件。主干结论不打折,hedge 只花在量词副词上("often significantly outperforming") |
| **禁过度数值解析** | 逐格念表、绝对值成串搬进正文、同一口径反复交代 | SSGC 整个实验章正文只出现一个数字("over 66×");协议/单位/CI 全文只声明一次 | 正文只报**方向+粗化增量**("between 3% and 6%"、"13%"、"10× faster");绝对值+± 只留给不在表里的对手;胜负交给表格加粗 |

唯一被允许的元话语是**有指向功能的指路牌**:"Note that"(此处有非显然事实,9 篇约 37 次)、"Below, we…"(节首路标)。它们不是废话,因为它们改变读者的注意力分配。

---

## 1. Abstract 蓝图

**总预算:8–9 句,180–195 词(实测 183/186/193,恒定 185±10),平均每句 20–23 词。零实验数字、零引用。**

功能序列(四年三个 venue 不变的脊柱):

| 句位 | 功能 | ~词数 | 与上句关系 | 为什么要写这句 | 骨架 |
|---|---|---|---|---|---|
| 1 | **共识背景**:一句话封圣研究对象/任务 | 11–26 | 开篇 | 让读者站上共同地面;只给一句,不绕远祖 | "X are leading methods for Y." / "X requires models to ___ while maintaining a balance between ___ and ___." |
| 2 | **问题暴露**:However 转折点出公认痛点 | 14–19 | 转折反驳上句 | 制造张力;痛点必须是领域承认的,不是自造的 | "However, without ___, the performance of X degrades quickly with ___." |
| 3 | **现状描述**:前人如何应对(可内嵌二分定位) | 18–35 | 因果承接(针对上句的已有应对) | 承认前人努力,同时把叙事框架抓在自己手里(先立设计原理,再把前人写成该原理的执行者) | "As ___ and ___ are two orthogonal aspects of ___, several methods focus on ___." |
| 4 | **缺口锁定**:第二个 However,前人修了但没修好 | 14–31 | 转折反驳上句 | **双 However 漏斗**完成两级收窄;缺口最好双维度(效果+成本);高配版直接点名头号竞品 | "However, these methods still ___, and suffer from ___." / "However, existing methods such as [竞品] face fundamental limitations, i.e., ___." |
| 5 | **方法宣告**:In this paper/Thus, we propose + 命名 | 17–38 | 因果承接(补缺口) | 全文唯一的"登场句";动词选 **derive/extend**(从有名字的理论对象推导)比 design/propose 格调高;必带缩写品牌 | "Thus, we use a modified [理论对象] to derive a variant of ___ called [NAME]." |
| 6 | **机制概述/核心洞察**:方法怎么运作,一句话版 | 18–36 | 支撑上句(Specifically) | 给审稿人一个可复述的机制记忆点 | "Our key insight is that by ___, we can achieve ___ , eliminating the need for ___." |
| 7 | **理论声明**:证明了什么性质(0–2 句,按 venue 调) | 24–32 | 递进深化 | 宣示"这不是 trick";显式报数("two theoretical claims")建立理论存在感;可带大 O 量级——摘要里唯一允许的"数字" | "We provide theoretical guarantees that this approach reduces ___ from O(___) to O(___), ensuring ___ without ___." |
| 8 | **定性战绩**(1–2 句) | 15–21 | 并列展开(理论→实验) | 只报比较维度+对手名单/基准名单,**不报数字**;claim 强度与证据强度对齐:主战场 "competitive/outperforms",次战场降档 "comparable" | "Experiments on ___ show that NAME outperforms ___, and is complementary with ___ and compatible with ___." |
| 9 | (可选)**资源指引** | 6 | 并列 | 2025 惯例:代码链接进摘要 | "The code is available at: ___." |

**Venue 微调**:理论会议(ICLR/NeurIPS)理论句 2–3 句且放实验前;视觉会议(CVPR)可压到 0–1 句、把预算给机制句;摘要句 7 的理论声明若是借来的定理,注明出处(语料里 SFA 没注明——这是该学的反面)。

---

## 2. Introduction 蓝图

**总预算:410–830 词正文 + 100–115 词贡献列表。理论会议 5 段~830 词(多出的全花在逐个点评竞品);视觉会议 3–5 段 410–530 词。平均句长 23–27 词。零实验数字。**

### 2.1 段落级结构(每段一个修辞动作,3–11 句)

| 段位 | 功能 | ~词数 | 段间衔接(下段首句如何接) | 为什么要有这段 |
|---|---|---|---|---|
| P1 | **重要性与价值**:研究对象为何值得研究,展开与本文直接相关的 1–2 个优势及应用 | 52–118 | 下段以缺口转折接("Yet exploiting this advantage requires…") | 先回答 why important,再补必要定义。定义、代际标签或“与传统方法不同”本身不是价值;每个优势必须能接到本文所研究的机制与实际用途 |
| P2 | **知识缺口 + 应用风险**:缺少什么判断,它影响哪些选择,弄错有何代价 | 62–170 | 段尾或下段转入精确问题("We therefore ask…") | 递进链模板:缺少的知识/判据 → 受影响的应用或设计决策 → **双向风险**(把无用机制当必要 / 把必要机制当无用)→ 精确研究问题。不能只说“尚未研究”,必须说明不知道会造成什么错误 |
| P3 | **二分定位 + 竞品交锋**(理论会议)或**收窄到子领域**(视觉会议) | 96–269 | 下段并列(继续盘点)或因果(引出方法) | 二分是最强的定位工具:"The two existing classes of methods, ___ and ___, have the disadvantages of ___ and ___, respectively."——先把全领域切成两族,一句话各判一罪,自己站在正交位。逐个点评竞品时用**批评-自我对照对**:"Although [竞品] relieves ___, it employs ___ which requires costly ___. In contrast, we show that our approach enjoys ___."(批评与 In contrast 卖点在同段成对出现,不等到贡献段) |
| P4 | **礼节收尾/靶子段** | 96–114 | 因果接方法段 | 两用:(a) 打包挂名相关方向("Noteworthy are also orthogonal research directions of ___; ___; ___ which improve ___ by ___, ___, and ___, respectively."——一句话还三笔人情债);(b) 单靶策略:点名头号竞品,缺陷编号 (1)(2),量化其上限,后文重复锤打三遍 |
| P5 | **方法宣告 + 贡献预告** | 127–196 | — | "To tackle the above issues, we propose ___" 收束全部铺垫;机制一句 + 性质/直觉若干句("We explain that ___ limits ___ while preserving ___.")+ 战绩句收尾(性能+速度双卖点) |

**段间衔接铁律**:每段首句显式回指上段(让步/因果/对比算子),**从不无预警跳话题**。段尾不做预告(预告是首句的工作)。

### 2.1a 机制/判据论文的开篇相关性门(导师实批补充,2026-09-18)

当论文追问“某种能力是否真的被模型使用”“何时一种机制不可约”或“给定模型属于哪种机制状态”时,Introduction 必须依次完成:

`对象的重要性与相关优势 → 缺失的知识/判据 → 与应用决策的连接 → 不理解该问题的双向风险 → 精确问题 → 本文如何研究 → 答案与结果`。

- **P1 价值先行**:先展开为什么该对象重要,但只写与本文问题有因果关系的优势。不能以分类史、代际标签或教科书定义代替价值主张;“输出形式不同”“表示更丰富”也不是优势,除非下一句说明它改善了什么应用。
- **P2 风险落地**:把抽象缺口挂到具体选择(如转换、训练、推理时长、读出或评估)。至少写清两种误判各自的代价:冗余机制被当成必要会浪费什么,必要机制被当成冗余会丢失什么。
- **转入本文**:精确问题出现后,后续段落只能承担三类工作:解释现有证据为何不能回答、说明本文采用的判据/研究方式、报告条件化答案和关键结果。不要再回到泛背景。
- **主语具体化**:用“方法/模型/研究者 + 动作”代替无边界集合名词,例如用 “ANN-to-SNN conversion methods map…” 代替 “the conversion literature makes…”。
- **“AI words” 必须做语料审计,不能凭词形判断**:先查本 skill 的导师论文语料；导师语料已有且承担明确逻辑功能的表达不得仅因“像 AI”而删除。无语料依据的装饰性评价、空泛主语和元话语,再到同领域原始论文核对术语与搭配,改成“领域对象 + 可验证动作/结论”,例如用 “short horizons introduce conversion error” 代替 “later work sharpens the correspondence”。普通功能词不逐字追溯,但所有可替换的判断词和领域搭配必须有导师语料或同领域论文依据。

开篇自检:删去方法名与领域名后,若 P1 仍可套用到任意论文,则价值陈述过泛;若 P2 没有出现受影响的实际决策和误判代价,则缺口尚未成立。

### 2.2 Contributions 列表

- 罗马数字 i./ii./iii.(/iv.),引导句固定:"Our contributions are as follows:" / "In summary, our contributions are threefold:"
- **3–4 条,每条 23–41 词(均值 ~30)**;全部动词开头(propose/introduce/derive/provide/demonstrate)。
- 槽位配方(选一):
  - 三件套:**诊断/假设 → 主方法 → 实验**(把"指出问题"或"提出假设/先验"本身列为第一贡献——轻方法的升格手法)
  - 四件套:**方法 → 理论 → 实现 → 实验**(末条永远是实验)
- 每条**只写机制不写效果**(效果留给实验);唯一例外:理论条可带量级对比从句。
- 次要组件显式自降权:"As a minor contribution, we propose ___"——主动定级反而稳,防"增量拼盘"质疑。
- 列表后可加一句**窄域 first 声明**:"To our best knowledge, this is the first work which considers ___ (in the ___ setting) in ___ with ___."——用多层限定词把 first 缩到不可证伪的窄域。
- ICLR 风格可用散文式贡献段代替列表(8 句 we-动词级联)。

---

## 3. Related Work 蓝图

**位置(按 9 篇实测修正,2026-09-02)**:**默认 §2(引言后)——9 篇中 7 篇如此**(GFB/GLEN/EASE/protoLP/BiLoRA/COSTA/SFA);后置到"方法与理论之后、实验之前"只有 COLES 一例(方法+理论两章很长、不想在前 6 页打断推导时才这样做);取消独立节只有 SSGC 一例(方法极简:拆进 Intro 交锋段 + Preliminaries 迷你综述 + 方法节 "Relation to X" 段)。续作必须放 §2——先重写前作史观,立论才能展开。**不确定时放 §2。**

**组织**:2–4 个粗体行首段(非子小节),按"任务轴/载体轴/机制轴"分族,由远及近。每段 = "一句一方法"目录体(方法名+引用+一个从句讲机制)+ **段尾一次性转折划清界限**。批评打族不打单篇(单篇只留给头号竞品)。

**批评句式五型**(每型一个存在理由):

| 型 | 骨架 | 用途 |
|---|---|---|
| 让步-转折-成本 | "Although [X] relieves ___, it employs ___ which requires costly ___." | 承认有效,否决代价 |
| 链式推进 | "[X] ignores ___, that is, [大白话复述]. To alleviate the above shortcomings, [Y] uses ___." | 批评句同时是过渡句,一石二鸟 |
| 三段炮 | "However, such methods often require ___. In addition, many ___ have ___ w.r.t. ___. In contrast, our method does not ___ but ___, and thus saves ___." | 连击后立即自比收束 |
| 全称否定靶心 | "However, no ___ methods use ___ by considering ___." | 声明空白地带(放分族段结尾) |
| 借刀 | 引用对手论文原文自证其弱:"[作者] explain that '[对手原句]'." | 最不可辩驳的批评 |

**划界免战句**(防审稿人要求补实验,这是"结构化防守"的正确形态):"___-based methods, not studied by us, are complementary to NAME." / "We do not study ___ as it requires ___."

---

## 4. Method 蓝图

### 4.1 章级结构
1. **开场 = 复述领域最经典的公式**(Preliminaries):把 ProtoNet/LoRA/基础模型的 Eq.(1)(2) 原样写一遍,然后把自己的方法呈现为**对经典公式的一处外科手术**("one can define ___ and insert it into Eq. (2), leading to:")。新方法永远是"最小编辑",这让 novelty 可定位、审稿人可验证。高配版:把头号竞品的公式也当预备知识复述("Existing Solution." 段)——靶子钉在自家地盘上打。
2. **Notation**:一个粗体 "Notations." 段,Let-连珠体一次建全,之后**旧符号永不重复解释**。
3. **推进引擎 = "However [缺陷] → Thus, we [修复]" 渐进修复链**:每小节结尾的缺陷句就是下一小节的动机句(SSGC 中 Thus×16、However×8)。roadmap 段甚至预告每步的缺陷("In Section 4.1, we outline ___ whose ___ is unacceptable due to ___. In Section 4.2, we introduce ___ which lets ___…")。
4. **节首路标**:每个 section/subsection 用 "Below, we…" 一段无编号 roadmap 开场。
5. 方法节末尾:**Complexity Analysis 小节**(forward/backward 分开的 big-O + 一个 wall-clock 数量级金句"over 66× slower")——效率是恒定的第二卖点。

### 4.2 公式三件套(铁律:没有裸公式)

每个编号公式的标准句链,逐句功能与词数:

| 句位 | 功能 | ~词数 | 存在理由 | 模板 |
|---|---|---|---|---|
| 前 | **前导句**(必有,常以冒号结尾) | 6–38 | 公式没有主语,前导句给它语法身份和来源 | 五模板:"X is defined as:" / "Given ___, ___ can be quantified as:" / "By defining ___, we reformulate Eq. N as:" / "Thus, we ___, and we obtain:" / "We generalize Eq. N as:" |
| 前(可选) | **Given/Let 批量定义句** | 15–55 | 新符号 >3 个时,不写长 where,改在公式**前**一次性定义 | "Given a cost matrix M ∈ R^{…} and M_ik = ___, the cost of mapping r = ___ to c = ___ using ___ P can be quantified as:" |
| 后 | **where 句**(仅当公式引入新符号) | 10–24 | 只解析**新**符号,1–3 个(众数 2),按公式内从左到右;内容 = 符号+系动词+类型/形状+至多一个角色短语 | "where ___ is a learnable orthonormal matrix learnt during the test time." 直觉塞括号:"(think the conditional probability p(y=k\|h))" |
| 后 | **直觉句**(重要公式必配) | 14–38 | 把数学译回人话,决定审稿人"懂没懂" | 信号词:"Intuitively," / "In other words," / "That is," / "One may think of the above process as a ___ on a ___." / "___ can be regarded as ___" |
| 后(可选) | **退化检查句** | 10–20 | 建立与经典的连续性,回答"这和 X 什么关系" | "Clearly, if ___ = 0 and ___ are free, Eq. N reduces to standard [经典方法]." |
| 后(可选) | **性质/求解句** | 9–26 | 闭式解 + 挂学名抬格调 + 防错细节 | "The optimal ___ can be found by selecting top-k (not bottom-k) eigenvectors of ___ (the so-called [学名] problem)." |

统计基准:每个编号公式平均配 **2.5–2.7 句**文字;公式密度 2.7(单栏)–4.2(双栏)个/页。

### 4.3 理论装置的标签经济学

| 装置 | 用途 | 规则 |
|---|---|---|
| **Theorem** | 只给两类:借来的定理(注明出处,用来打 baseline 或当天花板);自己最硬的 guarantee | 卖 guarantee 才用 Theorem;命名定理("Theorem 1 (Frequency Separation)")便于全文回扣 |
| **Proposition/Lemma/Claim** | 自己的分析结果**降格陈述** | 标准结论的改述用 Lemma;原创分析用 Proposition;启发式论证用 Claim——享受"theoretical claims"的话语权,躲开定理级审查 |
| **Condition/加框段/小节标题** | 无编号环境的替身 | 小节标题当命题用("4.1 NAME is ___-based ___");关键结论排成编号公式+彩色框,获得定理般的视觉权重 |
| **Remark/翻译段** | 定理后必接白话 | 三拍:界说了什么 → 实际中多大("Consider a practical example with d=1024, k=32: the probability is at least 99.9%")→ 工程含义/生活化类比("This is analogous to randomly placing k items in a d×d grid versus a 1D array") |

**理论的四个实际用途**(理论不是装饰,每一处理论都要有岗位):预判实验赢家(比较阶梯的终点=自己的选择)、**钦定超参**("The best effect is achieved for k=1. Thus, in all experiments, we set k=1."——审稿人无法再问超参怎么调)、解释败局(输的地方用自家理论自洽)、抬升命名(把性质名写进标题)。

**证明位置**:能压到 3–6 行的内联,长推导一句话外包("Proof. See Appendix A.");**Method 章预指实验表**("This is substantiated by Table 8, where ___")——理论声明与证据短接,不让读者悬着。

### 4.4 对照段("Relation to X")

三步模板:[对方做法 1–2 句,可引原文] → [In contrast, 我方 1–2 句] → [Thus 结论 1 句]。高配收束二选一:**精确等价条件**("In fact, NAME and [X] are only equivalent if α=0.5, K=1 and f is linear."——用充要条件切割相似工作,比"我们不同"高一个级别)或**增量数字压轴**("Across all datasets, A+B was consistently better than A+C by 0.3–0.4%.")。

---

## 5. Experiments 蓝图

### 5.1 章级结构
1. **协议段**(章首,6–8 句):数据集句(引文证明基准通用性)→ 批量表 roadmap("The results are summarized in Tables 1–6, and discussed below.")→ **数字口径句**(单位/CI/runs,全章只声明这一次)→ 协议细节(括号处理例外)→ backbone/实现来源 → 附录指引。**口径集中声明是"不过度数值解析"的前提**。
2. 主结果小节(按任务或按对手族切)→ 消融小节(段落式或编号小节)→ 效率段收官。
3. **Baseline 分类学列举**:不平铺名单,先建 taxonomy 再填名字("We compare NAME with three variants: (i) methods that only use ___, ie., ___; (ii) ___; and (iii) ___.")。全名单只在首提枚举一次。
4. **"X vs. OURS" 粗体块**逐类对手歼灭(NeurIPS 风格);或 RQ1–RQ4 研究问题结构(KDD 风格;RQ1 可以是"把 motivation 定量化"的诊断实验)。
5. **Ablation = 理论回验,不是调参扫描**:每个消融表对应一个理论声明/设计选择,行名直接写数学身份("Geometric (M0)"),扫描表的峰值位置就是理论预言的可视化。超参声明主动免疫调参质疑:"we fixed K=16 and α=0.05 across all datasets so K and α are not tuned to individual datasets at all."
6. (2025 风格)**理论验证专节**:模拟曲线对齐定理预言("The experimental results closely match our theoretical predictions"),配"解析与仿真吻合"图。
7. **图表:文字面积比 ≥ 2:1(用户硬标准,2026-09-02)**。证据:老师 SSGC 实验章 8 张表 + 1 张图,表格结构本身完成论证(references/06 任务 A);正文只做"表引用句 + 结论切片 + 归因"。执行:实验章文字压到该章篇幅的三分之一以内,每段文字必须挂在一张表或图上,正文不复述表里能读出的东西;版面不够时删文字、把不产生说服力的表下放附录,**绝不缩图**。
   **修正方向(2026-09-10 用户纠正)**:正文超过实验章 1/3 ⇒ 判不过,**先把每个结果块重写成 §5.2 的三句**;不许先挪图表去附录或缩图——那只会让图表:文字比变得更差。挪到附录的只能是公式、完整对照网格、原始数值、协议细节,不能是承载结论的图。

### 5.2 结果块:三句契约(硬约束;整合自 codex `research-paper-writing/references/experiments.md`)

**每个实验结果块恰好三句正文**。图表环境、caption、小节标题不计句数。

| 句 | 唯一职责 | 词数 |
|---|---|---:|
| **S1** | 最短的完整、可证伪结论——直接回答这个实验的问题 | 14–30 |
| **S2** | 指向图/表,在点名的对照与条件下给**一个聚合值 + 至多两个决定性锚点** | 25–55 |
| **S3** | 这个结果留下的下一个问题,以及回答它的实验;最后一块改为闭合证据链、交给结论 | 16–32 |

- **不许有第四句**(解释、范围、小结都不许加)。必要的范围限定挂在 S2 尾部,或整条挪去附录;绝不放进 caption。
- **不许逐面板/逐格叙述**;图表里看得见的数不在正文重复。
- 控制网格、指标公式、轨迹定义、剔除规则、原始测量、实现细节 ⇒ 协议表或附录。
- 协议段(setup)也是三句:E0-S1 被评对象/规模/对照边界;E0-S2 指协议表、只给读后文所需的固定条件;E0-S3 公式与完整对照推给附录,点出第一个实验问题。
- 块的顺序按"挑战—设计—证据"矩阵排,不按跑实验的时间顺序;每个 S3 制造下一块的需要。
- **禁过程史(2026-09-10 用户纠正)**:"我们第一次跑有缺陷""早先的数字漏了两组""修 bug 后结论反转"这类调试史是台账内容,**不进论文任何一处**。论文只报最终测得的东西;缺陷与撤回记在论文外的台账。

### 5.2b 证据工种清单(只决定三句里放什么,**不决定句数**)

以下旧版"段长 4–9 句"的句链保留为**工种清单**:用它挑出这个块最该说的结论、锚点和转折,再压进 S1/S2/S3。它不再决定输出句数。

| 句位 | 功能 | ~词数 | 存在理由 | 模板 |
|---|---|---|---|---|
| 1 | 设置句 或 **结论先行总起** | 8–33 | 强断言段(约 1/3)用结论开头("Our method is insensitive to the feature extractor.",8 词);其余设置先行 | — |
| 2 | **表引用句** | 9–19 | 挂表+一个结论切片(见 §7) | "Table N shows that NAME (best variant) outperforms all the previous SOTA." |
| 3 | **结论+范围+粗化增量** | 19–34 | delta 用范围/整数,不用点值 | "As shown in Table N, our method is superior in all settings by a significant margin, e.g., the gain varies between 3% and 6% on ___." |
| 4 | **机制归因句** | 15–23 | 赢要说出为什么赢,否则只是运气 | "This can be attributed to ___." / "…, which shows that NAME has an advantage over the [对照所属框架]." |
| 5 | 复证句(第二骨干/第二数据域) | 20–24 | 一次胜利是个例,两次是规律 | "With the backbone of ___, our method also outperforms ___, e.g., between 1.3% and 3.5% on ___." |
| 6–7 | **负结果+归因**(有就必须写) | 12–30 | 诚实是策略:自曝弱点并归因,好过被审稿人发现 | "On ___, our method cannot outperform ___ . Thus, we argue that ___ plays a more important role here than ___." |
| 8 | 收尾对比/小结 | 11–20 | 点名 1–3 个对手,不念全表 | "The proposed method also outperforms ___ such as [A], [B] and [C]." |

**败绩转化三段式**(最值得学的一招):承认("cannot outperform")→ 归因("Thus, we argue that ___")→ **验证实验反杀**("To prove this point, we also conduct an experiment (NAME+MLP) for which we ___, and we obtain a more powerful variant.")。变体:输局解释回扣自家理论("输恰恰因为那里没病可治":"datasets on which NAME does not achieve SOTA have ___, meaning less ___ is introduced")+ 效率安慰收尾。

**对手数字不在表里时**:文中直报绝对值+±("MCT yields 71.95% and 81.06% vs. our 71.5% and 81.37%"),先口径辩护("However, we use the ___ protocol for the common testbed")再对比。

**"惊讶—解释"两段式**(主动暴露反直觉点):"It is somewhat surprising that although ___ is not the optimal solution to ___, it still outperforms ___. Such a good performance comes from the following facts: (i) ___; and (ii) ___."

### 5.3 表格设计语法
- mean±std 必带(±规则:表内 1–2 位小数;CI 含义只在协议段说一次)。
- 按方法族/backbone 分组横线;组标签竖排;自家变体压组底标 "(ours)";自家行统一着色(全文一个品牌色,与公式高亮框同色)。
- **粗体 = 每列最优,包括别人赢的格**(不藏拙;要豁免反例,用正文一句话说理由,不动粗体)。
- 元信息列替读者做分类(Input: Feature/Graph/Both;Setting: Supervised/Unsupervised)——**表格结构本身完成论证**("No Learning 组打平 Supervised 组"一眼可读)。
- 上下界夹逼行(Joint Training / Sequential 夹住所有方法)让"贴近上界"话术有视觉支撑。
- OOM/#Params 列当修辞武器;SOTA 表兼任消融表(多变体行一表两用)。
- 必有效率表:每 epoch 秒数或推理时间,配数量级金句。

---

## 6. Conclusion 蓝图

**总预算:单段、5–9 句、120–200 词,无小节无编号。零数字、零数据集名(战绩只用比较级+范围词——数字全部留在实验章)。无独立 Limitations/Future Work 节。**

| 句位 | 功能 | ~词数 | 与上句关系 | 存在理由 | 模板 |
|---|---|---|---|---|---|
| 1 | **开门句**(三选一) | 16–33 | 开篇 | 定调:工作汇报 / 产品说明 / 宣言 | (a) 汇报式(现在完成):"We have proposed [NAME], a method extending [理论对象] (Section N), whose ___ if ___." (b) 减法式:"Without [别人都要的机制], we provide state-of-the-art results, outperforming ___." (c) 宣言式设问:"This work addresses a fundamental question in ___: how to achieve ___ without ___." |
| 2–3 | 成果/定位重述 | 11–26 | 递进/总分 | 拆件交代("It consists of two components: ___ and ___.")或阐明即插即用定位;组件各配一句分述 | — |
| 中段 | **破立复奏**(必有) | 18–34 | 转折反驳 | 把全文主旋律的对立结构最后复奏一遍——结论不是流水账,是论证的终曲 | "By applying ___, we have shown that [对手机制] yields [坏性质]. However, [OURS] uses ___, which results in [好性质]." / "Instead, we demonstrate that ___ provides a more scalable solution with provable guarantees." |
| 中段 | 理论性质枚举 | 20–29 | 并列(Moreover) | 每条性质一句;可比摘要多收一条战线 | "Moreover, [NAME] takes advantage of ___ whose family is known to ___." |
| 尾 | 战绩重述 或 前瞻 | 20–30 | 并列/新对象 | 汇报式收战绩(现在完成);宣言式收前瞻(慎用修辞通胀) | "We have conducted extensive experiments which show that ___ is competitive frequently outperforming ___ on ___, ___ and ___ tasks." / "Looking forward, this work suggests a shift from ___ to ___." |
| 尾(可选) | **范围限定+外推** | ~30 | 让步后转折 | limitation 的唯一形态:一个 While 从句,且立即外推 | "While our current focus has been on ___, the principles of ___ could ___ more broadly." |

**三条规则**:
1. **与摘要对齐率 ~50–67%,但全部改写措辞**:近义词轮换(neighborhoods→receptive fields→contexts;"limiting severe"→"mitigating"→"suffering less from");关键短语可整句逐字复用**一次**(如 9 词核心串)。
2. 时态三代可选:完成时工作清单(经典)/ 现在时产品说明书 / 现在时宣言体+前瞻三连(2025 风,句数最多但战绩句清零)。
3. 结论是校对盲区(语料里结论节笔误密度最高,连方法名都拼错过)——**成稿后单独核对结论**。

---

## 7. 图表引用规范(写什么 / 不写什么)

### 7.1 引用句式(163 句实测分布)

| 句式 | 占比 | 什么时候用 |
|---|---|---|
| 主语式 "Table N shows that + 结论" | 59% | **首提结果表的默认形态**;回指时换一个结论切片再用(同一表可引三次,每次切不同维度) |
| 从句中置 "…are summarized in Table N" | 23% | 引用是次要成分:协议句挂表、roadmap 批量挂号 |
| 括号式 "(see Table N)" / "(Fig. 1b)" | 7% | 辅助证据、附录表、子面板 |
| 从句前置 "As shown in Table N, …" | 6% | **78% 用于回指**(表已出场,再引时挪到句首状语) |

动词纪律:show 是绝对主力(66/96);**结果表用 "shows that+结论从句",信息表(数据统计/超参)用 "provides/presents + 内容名词"**。变体:冒号引出发现("Table 5 reveals an interesting finding: …")、多表合并判决("Tables 1, 2 and 3 show that …")。

### 7.2 引用句里写什么(六型,每句必居其一)
1. 结论+方向:"Table 4 shows that NAME relies on ___."
2. 结论+范围限定:"… outperforms all the previous methods **on all four datasets / in all settings / with both backbones**."
3. 结论+**增量**数字(delta/倍数,非绝对值):"without ___, the performance drops, i.e., 1.5%, 3.3% and 2.2% on [D1], [D2] and [D3]." / "over 66× slower"
4. 趋势方向(figure 主体):"Figure N shows that results gradually improve until they peak at ___ and then decrease, whereas ___."
5. 机制归因绑定:"Figure N shows that ___, **which confirms our insight that** ___."
6. 对比对象+条件:"Tables N and M show that ___ improves results **especially when** ___."

### 7.3 引用句里不写什么(负空间,五禁)
1. **禁"我们可以看到"**("we can see / it can be observed")——动词直接落在表上。
2. **禁复述表的设置**——协议、单位、CI、episode 数只在协议段声明一次,引用句永不重复。
3. **禁逐行念表、禁点全名单**——全名单只在首提枚举一次,之后 "all the previous SOTA / other methods" 概括,最多点名 1–3 个关键对手;禁止按行列坐标读表。
4. **禁绝对值成串进正文**——正文只报增量/范围/倍数;绝对值+± 只为不在任何表里的对手保留。
5. **禁 caption 写结论**——106 条 caption 无一含 outperform/best/superior;判决词只出现在正文。

### 7.4 Caption 公式
`[指标+单位] + [协议/次数] + [数据集/骨干](必备)  (+黑体/符号规则)  (+分组说明)  (+异常/缺格/来源声明)  (+读法指引)`
- 表 caption 首句中位 12–15 词;含规则句的全 caption 30–45 词(NeurIPS/KDD)或 5–30 词(ICLR/CVPR)。
- 只进 caption 不进正文:单位、"averaged over 10 runs"、"The best accuracy per column is in bold."、"OOM means out of memory."、"Results of other models are taken from their papers."、"CUB 5-shot omitted: no class has the required 70 examples."(缺格解释)。
- 图 caption 两档制:结果曲线图一句话(~10 词);**动机/机制图长 caption(33–90 词,3–5 句)承担论证**,逐面板 (left)/(right) 指引,末句可限定范围("We show a non-exhaustive set of cases.")或前向指路("see Section 4.1 for details")。
- **结果图/表 caption = 一个加粗名词短语(4–12 词),别无其他(整合自 codex `figures-and-tables.md`,取代旧"≤20 词一句话")**:不写面板说明、协议、条件、趋势、数值、机制、注意事项、解释、结论。面板身份放进**图内紧凑标签**(如 "(a) moment gap vs. leakage"),决定性证据放进相邻的三句结果块。表的异构口径标记与简短注意事项写在**表下注**,不进 caption。架构/方法图例外:加粗名词短语 + 至多两句说结构与执行顺序。
- **图内面板标题只写身份,不写结论**:"(b) collapse holds for every ϑ≠0" 是结论,违规;改成 "(b) moment gap vs. ε at five thresholds"。判决词只进正文 S1。
- **终稿尺寸可读性门(整合自 codex)**:每张图审两遍——独立 PDF 一遍、按论文终宽嵌入后一遍。图例不得压任何绘图区、数据点、注记、轴标题、刻度或面板标签;相邻刻度、轴标题、面板标签在终宽下必须互不重叠。优先用面板间预留空隙、直接线标或轴外图例,不许为停图例而开大片空白画布。碰撞检查不过 ⇒ 不许导出。
- **浮动体空白门(整合自 codex)**:编译成功不等于排版过关,逐页渲染看。某栏有大块空白而队列里还有浮动体或后续实验块能填 ⇒ 判不过;先查浮动体计数、放置顺序和 `\FloatBarrier`,再动文字或图尺寸;优先把结果图放在 S1 之后、S2 之前。绝不为藏空白而放大图、拉伸占位或删科学正文。
- **图的尺寸纪律(2026-09-02 补)**:单栏版心内一行最多 2 个面板(2×2 网格优于 1×4 横条);面板打印宽 ≥ 2.5 in、打印后字号 ≥ 6.5 pt;绘图时画布宽不超过打印宽的 1.5 倍再缩放(画 11 in 缩到 5.5 in 会把 12 pt 压成 6 pt 以下)。为省版面把图压成条状是错误:版面不够就删文字或下放表格,不缩图。
- 架构图配色:整条管线灰调,**唯独新模块高亮色**——一眼看出论文动了哪一块。图的最高用法不是画架构,而是当**证据**(真实数据的密度曲线坐实核心指控)或**理论 teaser**(滤波器形状/几何示意)。
- **并排浮动体高度必须相等**(用户反馈 2026-09-02:"一高一低的并排很丑",差 2 行也被打回):两表并排时**行数与横线数都要相等**(一条 \midrule 也差出可见高度),用像素测横线 y 核验;悬殊时不许硬并——改为**一张表拆双栏**(按组把行分到左右两个 tabular,顶对齐,共用一个 caption,如 "500M 消融(左)+ 200M 累加(右)"),或重新配对高度相近的浮动体。并成一张表后正文用 "Table N (right)" 指代。

### 7.5 图的制作工具分工(2026-09-01 注册)

- **数据图**(柱状对比 / 消融 / 趋势曲线 / heatmap / 多面板 / 雷达):**调用 `scientific-figure-making` skill** 制作(figures4papers house style:语义配色 蓝=主方法 / 绿=增益 / 红=对照、无框图例、去顶右脊、300dpi PNG+PDF 双出)。已实测,效果出版级。
- **架构图 / 框图 / 流程示意**:**调用 `academic-figures-drawer` skill**(2026-09-01 定案)——draw.io 可编辑矢量 XML 为源文件,含质量契约/静态校验/截图迭代闭环;可选的 image 概念草稿 pass 走本地 codex gateway(`scripts/imagegen_gateway.py`,gpt-image-2,已验证)。draw.io CLI 已装,直接导出 png/pdf/svg(导出后核对 mtime 新于源文件);字号按印刷尺度定(2400px 画布≈6.5in:正文≥27px、注记≥24px),复合多面板图入稿时拆分。画 NeuronSpark 图时配色向 figures4papers 蓝系靠拢,保持两类图同族。
- 机制类"数据即示意"面板(膜轨迹 / 权重分解曲线)优先从真实 checkpoint 取数绘制;若用合成数据,caption 必须标明 schematic/illustrative。

---

### 7.6 图文术语一体(用户令 2026-09-02)
- **架构图的标签就是正文的术语表**:正文描述自家模型时,每个部件先用图上的名字(粗体/斜体引入),公式作第二行,顺序与图一致;图注、消融表行名、贡献条目用同一套名字。
- 图上用领域概念(本仓库=类脑计算名:synaptic tagging / eligibility trace / lateral inhibition / selective reactivation…)时,正文不得改用等价的通用 ML 名(attention / softmax / write gate / retrieval layer…)描述自家模型;通用名只出现在 "Relation to X" 段给精确等价条件时,或作为公式内算子。
- 写作前 grep 图生成脚本的标签;写完用词频脚本查 method 节的通用名出现处逐条改。图与代码不一致时以代码为准并改图注(先核对代码,再改文)。

## 8. 关系语法(三层:句间 / 段间 / 章间)

> 关系在三个尺度上都必须显式可辨:句与句(段内)、自然段与自然段(同一章节内)、章节与章节。三层用的机制不同,不可混用。

### 8.1 第一层:句间(段内)

每句与上句的关系必居其一,并用显式算子实现(约 1/4 的句子携带转折/让步枢纽):

| 关系 | 实现算子 | 典型岗位 |
|---|---|---|
| 转折反驳 | However / Although / While / Despite / but | 缺口句、修复链关节 |
| 因果承接 | Thus / Therefore / Hence / To this end | 方案句、推论句(修复链的另一半) |
| 对照切割 | In contrast / whereas / rather than / instead of | 与竞品切割、自我卖点 |
| 递进深化 | Moreover / Furthermore / In addition / Importantly | 第二缺陷、第二性质 |
| 支撑展开 | Specifically / that is / i.e. / e.g. | 机制细化 |
| 换言重述 | In other words / That is | 术语版→白话版(同一论点说两遍是允许的,方向必须是翻译不是重复) |
| 实例化 | To this end, [方法名] / For instance | 原理→执行者 |
| 收束 | Overall / In summary / These limitations stem from | 段级结论、根因归一 |
| 指路 | Below, we… / Note that / Notice | 节首路标、非显然事实 |

**修复链主引擎**:"However [缺陷]. Thus, we [修复]."(单篇 Thus 可达 16 次)——方法章的默认推进方式。
**警句技巧**:段级收束句用短句+悖论式表达("It appears that deep GCN models gain nothing but the performance degradation from the deep architecture." / 7 词短句 "As prototypes are being updated, the graph changes." 故意打断长句节奏强调差异点)。

### 8.2 第二层:段间(同一章节内的自然段之间)

**每个自然段交界要回答两个独立的问题:逻辑关系是什么 + 用什么装置显式化。**(4 篇全文 158 个交界实测)

**装置九型**:

| 代号 | 装置 | 例 |
|---|---|---|
| A | 承接算子开段 | "Despite their enormous success…, many of the current ___ use fairly shallow setting" / "In contrast, modern ___ enjoy ___" |
| B | 回指词开段 | "To tackle **the above issues**, we propose ___" / "One solution for **that** is ___" / "**The above theorem** reveals ___" / "such an interference" / 公式号回指("we reformulate **Eq. 8** as:") |
| C | 粗体 run-in 段头 | "**Notations.**" "**Baselines.**" "**Updating Z.**" "**X vs. OURS.**"——段间关系由标题承担,段首句不承接 |
| D | 路标句 | "Below, we present ___" / "In this section, we ___" / "In what follows, we ___" |
| E | 冷启动 | 无装置直接开新话题(数学冷启动 "Let ___/Given ___"、断言式主题句 "Our method is insensitive to the feature extractor.") |
| F | 编号 | (i)(ii)(iii) / Claim I/II / Theorem N |
| G | 词汇链 | 上段的专名/符号原样搬进下段首句作锚:"GDC … further extends **APPNP** by ___"(上段主角是 APPNP) |
| H | 范围状语 | "For [数据集], …" / "In the case of [设定], …" / "On [战场], …"——状语声明并列论域切换 |
| T | 图表锚 | "Table 8 summaries the results for ___"——编号承担排序与衔接 |

**装置分区律**(哪章用什么,实测分布):
- **Introduction 从不用 C**(17 交界 C=1)——Intro 是算子/回指密度最高区,段间必须是论证链;
- **Related Work 是纯 C 领地**(11/14)——族并列靠段头,块内例外只有 H 与 B;
- **Method 是混合区**:推导链靠 B(公式号回指)+ E(数学冷启动),组件切换靠 C,竞品对比靠 A;
- **Experiments 靠 C+T+H**(CVPR 段头覆盖 >85%);无段头风格(ICLR)就用 H("For Reddit, …")+ T 排比("Table 8 summaries… / Table 9 summaries…")。
- 年代演化:段头制份额 27.5%→49% 单调上升;2025 式段间 A 算子归零,全靠**标题分舱 + 回指粘合**("this challenge"/"This approach"/"These results")。

**装置-关系搭配律**(逻辑关系决定装置的自由度):
- **因果拐点(问题→方案)必须显式**(A 或 B)——4 篇的提案句无一例外("Thus, we propose ___" / "To tackle the above issues, ___" / "To address this, ___");
- **并列展开是唯一可"裸奔"的关系**(E/C/H/T 任选,允许零算子);
- 递进深化:数学区用 B(公式/定理回指),叙述区用 G(词汇链);
- 让步后转折永远显式(Despite/Although/While);
- **回环呼应必带坐标**(章节号/定理号/专名/复现短语),从不裸回。

**各章段间逻辑骨架**(速查,写作时按此排段):
- Intro:重要性与相关优势 → 缺失判据及应用风险 → 精确问题 → 现有证据为何不足 → 研究方式 → 条件化答案与结果
- Related Work:族并列 ×N,每族段尾一次性转折划界
- Method:总分(roadmap)→ 推导递进链(B/E)→ **因果枢纽段**("Based on the aforementioned ___, we propose ___")→ 关系并列("Relation to X" ×N,块内 In contrast 转折)→ 成本并列(For 前向/For 后向)→ 表格分总
- Experiments:协议总分 → 主战场并列 → 消融并列/递进 → 效率或无题分总段收尾(四篇完全同构)

**段尾规则**:约 85% 的衔接负担在下段首句;段尾只允许两种钩——**欠账声明**("We will discuss ___ later in the text."——必须兑付,语料 4 篇零坏账)与**定理引渡**(段尾冒号:"This leads to our main result on ___:")。其余情况段尾不做预告。

### 8.3 第三层:章间(跨章节缝合)

**总原则:章与章之间不牵手——18 个章间交接 12 个纯冷切,靠每章自己的开门 roadmap 重启坐标。**

- **roadmap 分布律**:Method 必有(4/4;"Firstly/Secondly/Finally" 或 (i)(ii)(iii) 与小节一一对应)、理论节必有、实验章约半数有;**Intro 和 Related Work 从不用 roadmap**。措辞:双栏 "In this section, we…",单栏 "Below, we…/In what follows, we…"。
- **软化章间的三招**(可选):①方法章末偷跑一枚实验数字("over 66× slower"/"by 0.3–0.4%")替实验章开路;②下章首段回声复述上章末段(把竞品罪状原地再说一遍,冗余复现即胶水);③章内先放无题分总段("These results collectively demonstrate that ___")再切章。
- **前向指引**(9 篇 63 处,三形态):(a) 定理/章节号预支("as shown in Theorem 1"——Intro 就可预支 §2 的定理);(b) 欠账声明("later in the text");(c) 段尾 motivates/leads-to 钩。方法-实验之间最轻量的缝线是**括号插表号**:"the α parameter **(Table 9 evaluates its impact)**"。
- **回指分工**(35 处):"the above + 名词化对象"(issues/analysis/theorem)收编刚结束的推理块;"this/such + 名词"近距离粘合;**章节号回指只用于跨大章**(结论回收方法 "(Section 3.2)"、实验回收理论 "Following the analysis presented in Section 4.3");"aforementioned" 是稀缺强标记(全语料 1 次,放在全文最重要的原理→方案枢纽)。
- **理论-实验短接**(14 处,三级强度):理论区嵌表号("This is substantiated by Table 8, where ___")< 实验区回引章节号 < 制度化专节(Empirical Analysis 小节 + "To verify Theorem 2, we ___" + 图注复述定理不等式)。理论叙事越重,短接越要制度化。
- **主旋律回环**(全文级主题管理,最重要的一条):核心主张至少 **5 处变奏**——摘要 → Intro → 方法/理论 → 实验定谳 → 结论;每处**换分辨率**:编号化((1)(2))→ 符号化(T ≤ ⌊d/r⌋)→ 数字化(d=1024, r=32 → 32 tasks)→ 图表化(Figure 4 扫 rank)→ 结论再抽象。罪名逐级加重:模糊("suboptimal")→ 数值("log 2 constant and vanishing gradients")→ 图证 → 定理化。措辞用近义词轮换(neighborhoods→receptive fields→contexts);关键短语可整句逐字复用**一次**(摘要↔结论)。

---

## 9. 微观语言风格

| 维度 | 规则 |
|---|---|
| 时态 | 正文与方法一般现在时;实验操作过去时("We ran/trained");结论现在完成时("We have proposed/shown/conducted") |
| 人称 | **"we" = 贡献动作**(propose/show/argue);**"one" = 任何人都能做的数学步骤**("one can define ___ and insert it into Eq. (2)")。无被动偏好,无 "I" |
| Hedging 预算 | 主干结论不打折;hedge 只花在两处——量词副词("**often** significantly outperforming"、"typically")和附录近似声明。claim 强度与证据强度对齐:competitive > comparable > rivals 分档用 |
| 拟人动词库 | 方法/损失 enjoys / suffers / copes / ignores / encourages / alleviates / relies on——比 "has/is" 生动且省字 |
| 压缩句法 | 双斜杠对偶(similar/dissimilar、accuracy/scalability、simple/efficient)一词位装两个概念 |
| 指路牌 | "Note that"(非显然事实)、"Below, we…"(节首路标)、"so-called"(给借来/自造术语挂引导号) |
| 命名 | 方法必有可发音缩写品牌:词内大写 backronym(COLES/EASE/COSTA)、拼合词(protoLP/BiLoRA)、字母游戏(S²GC=SGC 的平方暗示升级);性质名可直接进标题("Covariance-Preserving"、"Almost-orthogonal"——标题就是定理的广告) |
| 校对(反面教训) | 语料里 camera-ready 仍有大量拼写/交叉引用错误(结论节与 checklist 是重灾区)——**学结构调度,校对必须自行做到更高标准**;避免 2025 式 LLM 修辞通胀(paradigm shift/revolutionize/profound implications 连用) |

---

## 10. 战略层:三个高频场景

### 10.1 简单方法怎么卖(核心场景)
1. **命名占位**:标题抢先把"简单"据为卖点("Simple ___");simple 必与 effective 配对出现。
2. **derive 而非 design**:方法从有名字的理论对象推导而来,公式出场前铺垫其理论传统。
3. **多重理论皈依**:同一个公式接入 2–4 个理论传统(每个一小节,各配一条借力的已证结论)——"这不是 trick,是必然结果"。理论深度感来自**视角数量与概念挂靠**,不来自证明难度。
4. **简单性变现**:免训练/闭式解/无超参 → 速度表+数量级金句+"超参跨数据集固定不调"。
5. **预答"这不就是 X 吗"**:"Relation to X" 段给精确等价条件。
6. **广度补深度**:单点提升不大就铺任务族(4+1 个任务)。
7. **减法当加法卖**:"少一个假设/少一道程序"是 novelty("unsupervised / no uniform prior / eliminating the need for ___");"Without meta-learning, we provide state-of-the-art results, outperforming a large number of sophisticated methods."
8. **缺陷重命名**:把算法的"不完美"命名成机制("incomplete power iteration ... enjoys two valuable byproducts")——bug 到 feature 的产权登记。

### 10.2 续作怎么写(升级自己的前作)
1. 摘要开场白与前作逐字复用(系列片头曲),前作以第三方口吻介绍。
2. **"in fact" 重译术**:先把前作翻译进本作的新数学语言("[前作] in fact minimizes ___"),再在新语言里超越它。
3. **收编**:"[前作] solves the ___ relaxation of [新作]"——前作降维成特例;批评前作只说"它需要额外补丁",从不说它错。
4. **参数族光谱**:一个连续参数把新旧两作安放成同一光谱的两端(p=1 是前作,p=0 是本作),消融表证明本作端最优。
5. 实验头条位打前作("[前作] vs. [新作]" 放所有对比块之首,"by up to 4.6%")。
6. 前作的 baseline 数字逐格复用(可验证的可信度资产);与前作重复的材料全下放附录——**续作正文的差异化密度必须高于首作**。

### 10.3 会议适配速查

| 维度 | ICLR/NeurIPS | CVPR | KDD |
|---|---|---|---|
| Intro | 5 段 ~830 词,竞品逐个交锋,可无 bullet 贡献 | 3–5 段 410–530 词,交锋外包给 RW,必有 bullet | 漏斗+修辞问句钩子,intro 可放数学与图证据 |
| 摘要理论句 | 2–3 句,置于实验前 | 0–1 句 | 0 句,诊断句代之 |
| Related Work 位 | 可后置(§5)或取消 | §2 | §2 |
| 实验组织 | "X vs. OURS" 粗体块 | 主表+消融小节 | RQ1–RQ4 显式结构 |
| 理论装置 | 编号环境+内联证明 | 0 环境或无证明命名定理,彩色框替身 | Definition+Lemma+Remark 三拍 |

---

## 11. 模板句库速查(按写作位置索引)

**摘要**:见 §1 表格右列。
**Intro 开局**:"X is pursued for two practical advantages: ___ and ___. The former enables ___, whereas the latter supports ___." | "Celebrated ___ methods, including [A] and [B], ___ by assuming that ___." | 警句:"It appears that ___ gain(s) nothing but ___ from ___."
**缺口**:"The ___ step is a vital but scarcely studied step of ___." | "The two existing classes of methods, ___ and ___, have the disadvantages of ___ and ___, respectively." | "However, no ___ methods use ___ by considering ___."
**方法宣告**:"Inspired by ___, we propose NAME, a novel ___ framework for ___, which ___ by ___." | "In this paper, we argue that ___, and thus ___ follows the ___ prior."
**方法推进**:"However, ___ is in fact suboptimal due to ___. Thus, we include ___ to balance ___." | "Given an insufficient number of ___, we instead transform the ___ problem into a ___ problem and then use ___ as surrogates for ___."
**理论翻译**:"Consider a practical example with ___=___: ___ is at least ___%. This is analogous to ___ versus ___." | "In other words, the ___ leads to a suboptimal ___, which results in a suboptimal ___."
**理论定超参**:"The best ___ effect is achieved for k=___. Thus, in all experiments, we set k=___."
**结果**:"Table N shows that NAME consistently achieves the best results on all datasets." | "This can be attributed to ___." | "…, which shows that NAME has an advantage over ___."
**败绩**:"On ___, our method cannot outperform ___. Thus, we argue that ___ plays a more important role here than ___. To prove this point, we also conduct an experiment (___) …"
**惊讶**:"It is somewhat surprising that although ___, it still ___. Such a good performance comes from the following facts: (i) ___; and (ii) ___."
**劣势补偿**:"Although ___ is somewhat slower than ___ in ___, it converges faster, thus enjoying a similar low runtime."
**结论**:"We have proposed ___. We have shown that ___. We have conducted extensive experiments which show that ___ is competitive frequently outperforming ___ on ___, ___ and ___ tasks."

---

*完整逐篇证据(含全部原文引句、逐句标注表、统计数据):`references/01-ssgc-gfb.md`、`02-coles-glen.md`、`03-cvpr-trio.md`、`04-costa-sfa.md`、`05-sentence-level-abs-intro.md`、`06-method-exp-figref.md`、`07-paragraph-junction-conclusion.md`*
