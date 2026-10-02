# 证据报告 06:Method/Experiments 逐句解剖 + 图表引用规范普查(9 篇全量)

> 任务 A 深挖 SSGC(ICLR,单栏)与 EASE(CVPR,双栏)的 Method/Experiments;任务 B 横扫 9 篇的 163 条正文图表引用句与 106 条 caption。引文逐字。

---

# 任务 A:Method 与 Experiments 逐句解剖

## A1. 公式密度
- SSGC §3:6 个编号公式 / 2.2 页 ≈ **2.7 个/页**;§2 Preliminaries 3.9 个/页。
- EASE §3:11 个编号公式 + Algorithm 1 / 2.6 页 ≈ **4.2 个/页**(CVPR 双栏密度约为 ICLR 的 1.6 倍)。

## A2. 公式周边句链的功能类型(样本节选)

**SSGC §3.2 MDK 块**(11 句):设计动机句(直觉先行+引文背书,31 词)→ 直觉补充(Moreover,14)→ 公式前导句("The Markov Diffusion distance between nodes i and j at time K is defined as:",15)→ **where 句兼下一公式前导句(链式)**(24)→ "By defining Z(K)=…, we reformulate Eq. 8 as the following metric:"(前导句,行内定义新算子,15)→ 公式后解析句(17)→ 图引用+性质声明前导(38)→ 编号两条性质(28)→ "In other words, as K grows, this filter includes larger and larger neighborhood but also maintains the closest locality of nodes."(公式后直觉句,21)→ Note that 桥接定义(21)→ Thus 推论收束(14)。

**SSGC §3.3 核心推导块**(10 句)要点:
- 前导句 "Based on the aforementioned Markov Diffusion Kernel, we include self-loops and propose the Simple Spectral Graph Convolution (S²GC) network with the softmax classifier after the linear layer:"(一句交代继承来源+两个改动)
- 与前人对照句+设计动机一句合并:"Compared with the more common form in (Zhou et al., 2004), we impose ‖hᵢ‖₂²=‖xᵢ‖₂²=1, to minimize the difference between hᵢ and xᵢ via the cosine distance rather than the Euclidean distance."
- **自我修正对**:"However, the infinite expansion resulting from Eq. 12 is in fact suboptimal due to oversmoothing." → "Thus, we include in Eq. 11 a self-loop T̃⁰ = I, the α ∈ [0,1] parameter (Table 9 evaluates its impact) to balance ..., and we consider finite K."(**括号内前向指到消融表**)
- 最短前导句形态:"We generalize the Eq. 11 as:"(6 词)

**SSGC "Relation to X" 对照段群**:四段共用**三步模板** [对方做法 1–2 句,可引对方原文] → [In contrast, 我方 1–2 句] → [Thus/This shows 结论 1 句]。GDC 段亮点:**直接引用对方原文为自己的批评背书**("Klicpera et al. (2019b) explain that 'most graph diffusions result in a dense matrix S'.");APPNP 段以**精确等价条件**收束("In fact, S²GC and APPNP are only equivalent if α = 0.5, K = 1 and f is the linear transformation.")。

**EASE 五句标准型**(Dissimilarity Matrix 块):Although 让步动机句(28)→ "Intuitively, given a K-way N-shot task with B queries for each class, we are targeting an (N+B)×K-way 1-shot problem where off-diagonal entries can be assumed to represent differing entities (on-diagonals represent the same entity)."(**Intuitively 显式标记**,38)→ Thus 前导句(15)→ where 句(2 符号,14)→ 前向指引句("We will discuss the relation between the dissimilarity matrix and PCA later in the text.",15)。

**EASE SIAMESE 块**结尾五句(对照段以数字压轴):对方做法 → 对方局限 → "**Our minor contribution**, SIAMESE, extends Sinkhorn K-means [12] to a semi-supervised setting with label propagation."(显式自我定级)→ 机制句 → **数字收尾**("Across all datasets, EASE+SIAMESE was consistently better than EASE+Sinkhorn K-means by 0.3–0.4%.")——**Method 章的对照段用一个增量数字压轴,不留到实验章**。

## A3. Method 章铁律汇总

**每个公式的伴随句配比**:

| 论文 | 编号公式 | 前导句 | where/解析句 | 直觉/动机句 | 求解/用法句 | 平均伴随 |
|---|---|---|---|---|---|---|
| SSGC §3 | 6 | 6(每式恰 1 句,6–28 词) | 4 | 5 | 0 | ≈2.5 句 |
| EASE §3 | 11 | 11(7/11 以冒号结尾) | 6 | 8 | 5 | ≈2.7 句 |

1. **没有裸公式**——每个编号公式必有一句前导句(常以冒号结尾)。前导句五模板:"X is defined as:" / "Given …, … can be quantified as:" / "By defining …, we reformulate … as:" / "Thus, we …, and we obtain:" / "We generalize … as:"。
2. **旧符号从不重复解释**;where 只在公式引入新符号时出现。
3. **where 句规律**(13 处):一个 where 解析 1–3 个符号(众数 2);**符号超过 3 个时改用公式前的 Given/Let 句一次性定义**(EASE Eq11 的 Given 句连定义 5 个符号);顺序 = 符号在公式里从左到右;内容 = 符号 + 系动词 + 类型/形状 + 至多一个角色短语;**直觉一律塞括号**("(think the conditional probability p(yᵢ=k|hᵢ))")。
4. 高级用法:**链式 where**(where 句同时充当下一公式的前导句);**角色型 where**(不给类型给作用:"where A_sim and A_dis are two different measurements with the opposite effect.")。
5. **证明外包一句话**:"Our design follows Claims I and II described in Section A.3, which includes their detailed proofs."(声明+位置合一)
6. **Method 章预指实验表**:Claim 陈述后紧跟 "This is substantiated by Table 8, where ..."(SSGC);EASE 的 0.3–0.4% 同理。

## A4. Experiments 段落句链范式

**SSGC 4.1 Node Clustering(5 句,零结论句范式)**:对比对象枚举(i)(ii)(iii) 两句(35+74)→ 指标句(21)→ 协议+表引用+**黑体规则声明**("We run each method 10 times on four datasets: …, and we report the average clustering results in Table 3, where top-1 results are highlighted in bold.",31)→ 超参选择句(26)。**没有任何一句文字结论——胜负完全交给表格加粗,"结论进表、口径进文"的极端版。**

**SSGC OGB 段(8 句,"结论—归因—验证"完整链,全段无一个具体数字)**:总起+表引用+对比对象(33)→ "On these three datasets, our method consistently outperforms SGC."(9)→ **负结果句**("On Arxiv and Products, our method cannot outperform GCN and GraphSage while MLP outperforms softmax classifier significantly.",17)→ "Thus, we argue that MLP plays a more important role here than the graph convolution."(机制归因,15)→ "To prove this point, we also conduct an experiment (S²GC+MLP) ..."(验证实验,32)→ 分数据集展开(because 归因,幅度词 tiny margin 代替数字,23)→ 概括(11)→ 小结(12)。

**SSGC 层数消融段(4 句标准链)**:表引用总起+括号读法说明(30)→ "We observe that on Cora, Citeseer and Pubmed, our method consistently obtains the best performance with K = 16, equivalent of 16 layers."(观察句:给最优超参位置而非精度数字,23)→ "Overall, the results suggest that S²GC can aggregate over larger neighborhoods better than SGC while suffering less from oversmoothing."(机制小结,19)→ "In contrast to S²GC, the performance of GCN and SGC drops rapidly as the number of layers exceeds 32 due to oversmoothing."(baseline 对照+归因,22)。

**EASE 协议段(8 句,数字口径一次性集中声明)**:数据集句(顺带引文证明基准通用性)→ 协议句 → **批量表 roadmap 句**("The results ... are summarized in Tables 1, 2, 3, 4, 5 and 6 respectively, and discussed in the following sections.")→ **数字口径句**("The performance numbers are given as accuracy %, and the 0.95 confidence intervals are reported."——全章只声明这一次)→ 协议细节(括号处理例外)→ backbone 来源 → backbone 列表 → 附录指引。

**EASE 半监督段(9 句全要素链)**:设置(33)→ 表引用(13)→ 结论+范围+幅度("As shown in Table 5, our method is superior to other competitors in all settings by a significant margin (ResNet-12 backbone) e.g., the gain varies between 3% and 6% on mini-ImageNet 1-shot protocol."——**delta 用范围不用点值**,34)→ 机制归因("This can be attributed to improved capturing of the data-manifold structure given extra unlabeled samples.",15)→ 第二骨干复证+幅度(24)→ 复现说明(交代对手数字从哪来,21)→ **负结果归因**(先因后果,30)→ 负结果陈述(Thus,12)→ 补充对比(**对手不在表里 → 文中带 ± 直报**:"84.89±0.74 vs 82.66±0.97",18)。

**EASE MCT 对话段(5 句,负结论先行)**:"Some recent models such as MCT [19] use data/model perturbation/augmentations and achieve results even better than ours."(**承认他人更好**)→ "However, we use the TAFSSL protocol (and thus their features) for the common testbed with other methods."(口径辩护)→ 逐点数值对比 ×3(对方不在表里 → 数字直接进正文)。

**EASE DenseNet 段(4 句,结论先行范式)**:"Our method is insensitive to the feature extractor."(**8 词结论先行总起**)→ 表引用+设置(35)→ 数值证据(delta 整数化:"gains 13% ... more than 4%",21)→ 对比范围扩展(点名 2–3 个,不念全表,20)。

## A5. Experiments 统计汇总

| 维度 | SSGC | EASE |
|---|---|---|
| 结果段句数 | 5–9 句,中位 ≈7 | 3–9 句,中位 ≈5 |
| 开头类型 | 7 段全部描述/设置先行,两段通篇无文字结论 | 9 段中 3 段**结论先行**(含"负结论先行") |
| 典型链 | 设置→表引用→正结论→负结论→归因→验证实验→小结 | 设置→表引用→结论+幅度→归因→复证→负结果+归因→补充对比 |
| 表内精度 | 均值 1 位小数+std;聚类 2 位无 ±;计时 2 位 | 全部 2 位小数+±(CI 只在协议段声明一次);计时科学计数 |
| 正文数字习惯 | **几乎不进正文**:只用方向词+幅度词(consistently/tiny margin/slightly/rivals),唯一数字 "over 66×" | delta 进正文且**粗化**(整数/1 位/区间);绝对值+± 只在对手不在表里时直报 |
| 负结果处理 | 明写并当作归因起点 | 明写并给机制原因,再补一个能赢的对比对冲 |

---

# 任务 B:图表引用规范普查(9 篇,163 条正文引用句 + 106 条 caption)

## B1. 引用句式分布

| 句式 | 次数 | 占比 | 首提 | 回指 | 典型场景 |
|---|---|---|---|---|---|
| **主语式**(Table N + 动词) | 96 | 59% | 69 | 27 | **首提结果表的默认形态**;回指时换一个结论切片再用 |
| 从句中置式(…shown in Table N 在句中后部) | 38 | 23% | 24 | 14 | 引用动作是句子的次要成分:协议句挂表 |
| 括号式((see Table N) / (Figure 1b)) | 11 | 7% | 8 | 3 | 辅助证据、附录表、子面板 |
| 从句前置式(As shown in Table N, …) | 9 | 6% | 2 | 7 | **78% 用于回指** |

**动词库**(主语式 96 句):**show 66(绝对主力)**,illustrate 5,demonstrate 4,provide 4,summarize 3,present 2,其余零星。"shows/demonstrates that + 结论从句" 43 次(26%)。**首提结果表用 "shows that+结论";首提信息表(数据统计/超参)用 "provides/presents + 内容名词"**("Table 1 provides details of all datasets.")。

特殊变体:冒号引出发现("Table 5 reveals an interesting finding: ...");多表合并判决("Tables 1, 2 and 3 (mini-ImageNet and tiered-ImageNet) show that EASE (best variant) outperforms all the previous (transductive/inductive) SOTA.");roadmap 批量挂号。

回指范例(同一表反复引用、每次给**不同**结论切片):GLEN 对 Table 1 连用三次主语式,每次切不同的比较维度。

## B2. 引用句里写什么(六型)

1. **结论+方向**:"Table 4 shows that COLES-GCN relies on negative Laplacian Eigenmaps."
2. **结论+范围限定**(all datasets / 某 backbone / 某 protocol):"protoLP consistently outperforms all the previous (transductive and inductive) methods."
3. **结论+增量数字**(delta 或倍数,非绝对值):"Table 3 shows that without the negative Laplacian Eigenmaps, the performance of COLES-S²GC drops significantly i.e., between 6% and 9% for 5 labeled samples per class." / "Table 2 demonstrates that APPNP is over 66× slower than S²GC…"
4. **趋势方向**(figure 主体):"Figure 3 shows that results gradually improve until they peak at 20 (dimension) and then continue to decrease, whereas our method helps improve the performance until the number of dimensions equals the number of samples."
5. **机制归因绑定在引用句内**:"Figure 4 shows that nodes with a small degree exhibit more bias, which confirms our insight that ..."
6. **对比对象+条件**:"Tables 6 and 7 show that OT improves results especially in 1-shot classification when the features are not discriminative enough (ResNet-12)."

## B3. 引用句里从不写什么(负空间——最重要)

1. **不写"我们可以看到"类空话**。163 句中 "we can see (that)" 仅 1 例且出自唯一未发表的 arXiv 稿;"it can be observed that" 0 例。通行做法:动词直接落在表上("Table N shows…")或结论直接开句。
2. **不复述表的完整设置**。协议、单位、CI 含义、episode 数只声明一次(集中在实验章开头协议段),之后所有引用无一重复口径。
3. **不逐行念表、不点全名单**。baseline 全名单只在首提枚举一次,后续一律 "all the previous SOTA" / "other methods" 概括,最多点名 1–3 个关键对手。全语料没有一句按行列坐标读表。
4. **绝对成绩通常不进正文**。正文只报增量/范围/倍数;绝对值+± 只在对手数字**不在任何表里**时出现。SSGC 更极端:整章结果讨论仅一个数字("over 66×")。
5. **caption 与正文分工严格**。只进 caption 不进正文:指标单位、平均次数/分割协议、黑体规则、符号图例、缺格解释("OOM means out of memory.")、数字来源("Results of other models are taken from their papers.")、分组方式。反向同样成立:**caption 从不写结论**——106 条 caption 无一含 outperform/best/superior 类判决词。

## B4. Caption 写法

**信息构成公式**:`[指标+单位] + [协议/次数] + [数据集/骨干](必备名词短语) (+ 黑体/符号规则) (+ 分组说明) (+ 异常/缺格/来源声明) (+ 读法指引)`。

**长度**:表 caption 首句中位 ≈12–15 词;全 caption:ICLR/CVPR 组 5–30 词(1–2 句),NeurIPS/KDD 组 30–45 词(3–5 句)。图 caption 两极分化:结果曲线图 ≈10 词一句;方法/动机图 33–69 词、3–5 句、常带 (left)/(right)/(a)(b) 逐面板指引。

代表样本:
- 极简名词短语:"Computational and storage complexities O(·)."(SSGC Table 1,5 词)
- 标准表 caption:"Test accuracy (%) averaged over 10 runs on citation networks."(10 词)
- 带读法指引:"Summary of classification accuracy (%) w.r.t. various depths. In the linear model, the filter parameter K is equivalent to the number of layers."
- 带来源声明:"Test Micro F1 Score (%) averaged over 10 runs on Reddit. Results of other models are taken from their papers."
- 规则型极大值(COLES Table 2,42 词 5 句):"Mean classification accuracy (%) and the standard dev. over 50 random splits. Numbers of labeled samples per class are in parentheses. The best accuracy per column is in bold. Models are organized into semi-supervised, contrastive and unsupervised groups. OOM means out of memory."
- 带缺格解释:"... CUB 5-shot omitted: no class has the required 70 examples."
- 符号图例压缩+反指正文:"(∗: inference aug., §4.2.3)"
- 动机图逐面板:"Drawbacks of prototype-based and graph-based FSL. (left) Some label assignments are incorrect due to the imperfect decision boundary. (right) Some 'strong' links in the fixed graph are incorrect as they associate samples of different classes."

会议差异:NeurIPS/KDD 组把黑体规则写进 caption;ICLR 的 SSGC 放正文;CVPR 两篇全文不解释加粗。

---

# 浓缩操作规则(五条)

1. **公式三件套**:冒号结尾的前导句(五模板之一)→ 公式 → where 句只解析新符号(≤3 个、按公式内从左到右、"类型/形状+至多一个角色");符号超 3 个改用公式前 Given/Let 句;直觉进括号或单独 "Intuitively," 句。
2. **对照段模板**:对方做法(可引原文)→ "In contrast, …" → "Thus, …" 结论;高配版给出与对方的**精确等价条件**,或以一个增量数字收尾。
3. **结果段链**:设置(1)→ 表引用(1)→ 结论+范围+粗化 delta(1)→ 机制归因 "can be attributed to / due to"(1)→ 复证或负结果+归因(1–2)→ 收尾对比(1);段长 4–9 句;结论先行仅用于强断言段(约 1/3)。
4. **数字纪律**:表内 2 位小数+±;正文只报方向词与粗化增量(整数/1 位/区间);绝对值+± 只为不在表中的对手保留;口径全文声明一次(协议段或 caption,二选一),永不在引用句重复。
5. **引用句纪律**:首提用 "Table N shows that + 结论"(结果表)或 "provides/presents + 内容"(信息表);回指用 "As shown in Table N" / 换结论切片再用主语式;辅助材料用括号式;**禁 "we can see"**。
