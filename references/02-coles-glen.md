# 证据报告 02:COLES (NeurIPS 2021) + GLEN (NeurIPS 2022)

> Hao Zhu 一作的两篇 NeurIPS 论文,同一研究线(Laplacian Eigenmaps 的对比学习推广),GLEN 是 COLES 的直接续作。所有引文逐字摘自原文。

---

## 第一篇:COLES — "Contrastive Laplacian Eigenmaps" (NeurIPS 2021)

### 1. 元信息

- 18 页 arXiv 版:正文 pp.1–10 → Acknowledgments + References pp.11–14 → Supplementary pp.15–18。**正文 10 页里实验只占约 3.5 页,理论占约 2.5 页——理论与实验平分秋色,是典型 NeurIPS 配比。**
- 定位:方法论文,但以理论性质为主卖点(方法本身只是"把负采样加进 Laplacian Eigenmaps"这一个公式)。三条贡献里两条半是理论声明。
- 首页脚注:`* The corresponding author.    Code: https://github.com/allenhaozhu/COLES.`

### 2. 标题命名模式

**"Contrastive Laplacian Eigenmaps" = [现代形容词] + [经典方法原名]**。三词名词短语。缩写通过词内强行大写凑出:"**CO**ntrastive **L**aplacian **E**igenmap**S** (COLES)"。**标题即研究纲领**——"经典方法名保留在标题里,修饰词宣告注入的现代成分"。

### 3. 摘要逐句解剖(7 句)

> "Graph contrastive learning attracts/disperses node representations for similar/dissimilar node pairs under some notion of similarity. It may be combined with a low-dimensional embedding of nodes to preserve intrinsic and structural properties of a graph. In this paper, we extend the celebrated Laplacian Eigenmaps with contrastive learning, and call them COntrastive Laplacian EigenmapS (COLES). Starting from a GAN-inspired contrastive formulation, we show that the Jensen-Shannon divergence underlying many contrastive graph embedding models fails under disjoint positive and negative distributions, which may naturally emerge during sampling in the contrastive setting. In contrast, we demonstrate analytically that COLES essentially minimizes a surrogate of Wasserstein distance, which is known to cope well under disjoint distributions. Moreover, we show that the loss of COLES belongs to the family of so-called block-contrastive losses, previously shown to be superior compared to pair-wise losses typically used by contrastive methods. We show on popular benchmarks/backbones that COLES offers favourable accuracy/scalability compared to DeepWalk, GCN, Graph2Gauss, DGI and GRACE baselines."

| 句 | 功能 | 技巧点 |
|---|---|---|
| S1 | 背景(一句话定义领域) | 用 "attracts/disperses"、"similar/dissimilar" 双斜杠压缩对偶概念 |
| S2 | 背景→机会 | "It may be combined with..." 为二者联姻埋伏笔 |
| S3 | 方法声明+命名 | "celebrated"(向经典致敬)+ 显式命名仪式 "and call them" |
| S4 | 理论声明 1 = 对现有方法的缺陷诊断 | 缺口不单独成句,打包成定理式指控 |
| S5 | 理论声明 2 = 己方机制优势 | "demonstrate analytically"、"essentially" 强断言措辞 |
| S6 | 理论声明 3 | 借他人已证结论抬轿("previously shown to be superior") |
| S7 | 实验结果 | 不报数字,只报比较维度与对手名单 |

**结构特征**:没有独立的"缺口句"和"贡献列举句";7 句里 3 句是理论声明(S4–S6 恰好对应正文 4.1/4.1/4.2 三个小节)——**摘要就是理论分析节的目录**。

### 4. Introduction 段落级解剖(4 段 + "Novelty." 段 + 贡献列表)

**P1(背景+经典的缺口)**,首句:
> "Celebrated graph embedding methods, including Laplacian Eigenmaps [5] and IsoMap [42], reduce the dimensionality of the data by assuming that it lies on a low-dimensional manifold."

**跳过 "graphs are ubiquitous" 类应用套话,第一个词就是 "Celebrated"**,直接从经典讲起。hook 逻辑是"致敬—复述假设—揭短",四句完成,段尾落缺口:
> "In other words, such penalties do not guarantee that unrelated graph nodes are separated from each other in the embedding space."

**P2(现代路线+攻击点)**,首句以对比过渡:
> "In contrast, modern graph embedding models, often unified under the Sampled Noise Contrastive Estimation (SampledNCE) framework [33, 28] and extended to graph learning [41, 15, 50], enjoy contrastive objectives."

段尾把攻击目标钉死到一个具体组件:
> "It relies on the inner product passed through the sigmoid non-linearity, which we argue below as suboptimal."

**P3(提案段——绿色高亮框)**:提案首句连同总目标公式 Eq.(1) 放进**绿色圆角底纹框**,出现在第 1 页下方:
> "Thus, we propose a new COntrastive Laplacian EigenmapS (COLES) framework for unsupervised network embedding. COLES, derived from SampledNCE framework [33, 28], realizes the negative sampling strategy for Laplacian Eigenmaps. Our general objective is given as: [Eq. (1)]"

**读者翻开第 1 页就能看到唯一核心公式**。框后紧跟逐符号解释。

**P4(理论预告段)**:"By building upon previous studies [28, 2, 48], we show that COLES can be derived by reformulating SampledNCE into Wasserstein GAN using a GAN-inspired contrastive formulation." 段内自评影响力("This result has a profound impact on the performance of COLES"),引 Figure 1 作经验证据。

**段间过渡是纯逻辑算子**:P1→P2 "In contrast" → P3 "Thus" → P4 "By building upon" → "In summary"。

**Contributions**("In summary, our contributions are threefold:" + i./ii./iii.):
> "i. We derive COLES, a reformulation of the Laplacian Eigenmaps into a contrastive setting, based on the SampledNCE framework [33, 28]."
> "ii. By using a formulation inspired by GAN, we show that COLES essentially minimizes a surrogate of Wasserstein distance, as opposed to the Jensen-Shannon (JS) divergence emerging in traditional contrastive learning. Specifically, by showing the Lipschitz continuous nature of our formulation, we prove that our formulation enjoys the Kantorovich-Rubinstein duality for the Wasserstein distance."
> "iii. We show COLES enjoys a block-contrastive loss known to outperform pair-wise losses [3]."

措辞规律:动词阶梯 **derive → show/prove → show**;每条都带机制状语;贡献数固定为三,明说 "threefold"。

**"Novelty." 段**(贡献列表后的独立粗体段)——预防性抗辩装置:
> "Novelty. We propose a simple way to obtain contrastive parametric graph embeddings which works with numerous backbones. For instance, we obtain spectral graph embeddings by combining COLES with SGC [49] and S2GC [61], which is solved by the SVD decomposition."

不否认简单,反而把 "simple" 说成卖点,并立即给出与自家前作组合的实例。

### 5. Related Work

- **位置:第 5 节**——在 Methodology(3)和 Theoretical Analysis(4)之后、Experiments(6)之前。让读者带着已建立的方法框架去读综述,且正文前 6 页不被综述打断。
- 组织:三个粗体行首段落("Graph Embeddings." / "Representation Learning for Graph Neural Networks." / "(Negative) Sampling.")。每段是"一句一方法"的目录体。
- **批评句式**:
  1. 揭缺陷+顺势引出下一家:"...Laplacian Eigenmaps ignore relations between dissimilar node pairs, that is, embeddings of dissimilar nodes are not penalized. To alleviate the above shortcomings, DeepWalk [35] uses truncated random walks..."(**"X ignores Y, that is, [大白话复述]. To alleviate the above shortcomings, Z uses..."** 标准链条)
  2. 指出领域空白:"Supervised and (semi-)supervised GNNs [22] require labeled datasets that may not be readily available. Yet, unsupervised GNNs have received little attention."
  3. **划界免战**(防审稿人要求补实验):"Multi-view augmentation-based methods, not studied by us, are complementary to COLES." / "We do not study graph classification as it requires advanced node pooling [24] with mixed- or high-order statistics [26, 25, 27]."

### 6. 方法呈现

- **Notation**:粗体 "Notations." 段,**"Let...Let...Let..." 连珠体**,收尾字体约定:"Finally, scalars and vectors are denoted by lowercase regular and bold fonts, respectively. Matrices are denoted by uppercase bold fonts."
- **形式化装置:正文 0 个编号 Theorem/Proposition/Lemma/Definition**。理论以三种形态存在:(a) **小节标题当命题用**("4.1 COLES is Wasserstein-based Contrastive Learning"、"4.2 COLES enjoys the Block-contrastive Loss");(b) 四个绿色高亮框当"无名定理环境";(c) 粗体行首段承担引理("Lipschitz continuity of COLES.")。修辞作用:降低形式化门槛、每页都有视觉锚点、把证明义务移出正文。
- **证明位置**:推导全推附录——"we cast Eq. (4) into the objective of COLES (refer to our Suppl. Material for derivations)"。
- **数学与直觉交替**:公式块 → 一句翻译,信号词 We note that / that is / In other words / Clearly:
  - "We note that COLES minimizes over the standard Laplacian Eigenmap while maximizing over the randomized Laplacian Eigenmap, which alleviates the lack of negative sampling in the original Laplacian Eigenmaps."
  - "In our setting, the case pg ∼ pr means that negative sampling yields hard negatives, that is, negative and positive samples are very similar."
  - 退化检查句:"Clearly, if η′ = 0 and Y are free variables, Eq. (5) reduces to standard Laplacian Eigenmaps [5]."
- **理论节写法 = "同一个损失换三副眼镜重述"**(4.1 GAN/OT 视角、4.2 block-contrastive 视角、4.3 超球面对齐-均匀视角),每副眼镜一个小节、一条性质、一处借来的已证优越性。开篇摆分析路线图:"the key idea of this analysis is to (i) cast the traditional contrastive loss ... as a GAN framework, and show this corresponds to the use of JS divergence and (ii) cast the objective of COLES ..., and show it corresponds to the use of a surrogate of Wasserstein distance."
- 数学操作本身初等(sigmoid 换 RBF、迹展开、Lipschitz 一行验证),**每个性质都挂靠一个重量级命名概念**——Wasserstein GAN、Kantorovich-Rubinstein duality、block-contrastive loss (Arora et al.)、Alignment/Uniformity (Wang & Isola)。深度感来自视角数量与概念挂靠,不来自证明难度。

### 7. 实验

- 组织:总纲段(定义 unsupervised/contrastive/(semi-)supervised 三组游戏规则)→ 粗体段 "Datasets." "Metrics." "Baseline models." "General model setup." "Hyperparameter of our models." → 6.1 Transductive → 6.2 Uniformity Loss as the Generalized Mean → 6.3 Inductive → 6.4 Node Clustering → "Scalability." 段收官。
- **结果讨论用 "X vs. COLES" 粗体小标题分块**:"Contrastive Embedding Baselines vs. COLES."、"Semi-supervised GNNs vs. COLES."、"Unsupervised GNNs vs. COLES."——每块打一类对手。
- **表格设计**(Table 2 主表):
  - Caption 自带图例说明书:"Mean classification accuracy (%) and the standard dev. over 50 random splits. Numbers of labeled samples per class are in parentheses. The best accuracy per column is in bold. Models are organized into semi-supervised, contrastive and unsupervised groups. OOM means out of memory."
  - mean±std、每列最优加粗、无箭头;左侧竖排组标签,组间实线、组内虚线;**自家方法行用蓝色字体**;
  - 借他人数字必声明:"Results of other models are from original papers."
  - **OOM 作为修辞武器**:竞品在大图上四格连排 OOM,表格本身替 scalability 论点说话;加 #Params 列凸显 110,120 参数打赢百万级参数模型。
- **结果句式**:
  - 归因句:"In particular, COLES-GCN outperforms GCN+SampledNCE on all four datasets, which shows that COLES has an advantage over the SampledNCE framework."(**win → which shows that [机制归因]**)
  - 幅度句:"When the number of labels per class is 5, COLES-S2GC outperforms GCN by a margin of 8.1% on Cora and 9.4% on Citeseer."
  - 认输句:"We also note that COLES-GCN (Stiefel) outperforms COLES-GCN ... by up to 2.7% but its performance below the performance of COLES-S2GC."
- **Ablation = 理论回验,不是调参扫描**:κ 消融验证"负 Laplacian 不可少";广义均值消融直接回扣理论 4.3 节,且表内行名直接写理论身份("Geometric (M0) (COLES-S2GC)"、"Arithmetic (M1) (SoftMax-Contrastive)")——**把消融表变成"我们的理论视角预测了赢家"的证词**。
- **Scalability 段模板**(具体秒数收尾):"Specifically, COLES-S2GC took 0.3s, 1.4s, 7.3s and 16.4s on Cora, Citeseer, Pubmed and Cora Full, respectively. GraphCL took 110.19s, 101.0s, ≥ 8h and ≥ 8h respectively."

### 8. 图

- **Figure 1 = 动机的经验证据**(p.2 顶部,紧贴引言):两个 minibatch 上正/负对内积得分的密度曲线——用真实数据图坐实"JS 散度会遇到近乎不相交分布"这一核心指控。**先看图信、后读定理**。
- Caption = 描述 + 解读 + 前向指路三段式:
> "Figure 1: Densities of dot-product scores ⟨v, u⟩ and ⟨v, u′⟩ (red and blue curves) between the anchor/positive embedding and the anchor/negative embedding (GCN contrastive setting). Left/right figures use two distinct minibatches sampled on Cora. With the small overlap of distributions, many contrastive methods relying on the JS divergence may underperform (see Section 4.1 for details)."
- 全文正文仅 1 图。**图不做架构示意,只做证据**。

### 9. 微观语言风格

- **高频口头禅**:**"so-called" ×13**(给每个借来的术语挂标签);**"enjoy(s)" ×9**(拟人化第一动词,进小节标题);"outperform" ×19;"e.g." ×11;"In contrast" ×8;"Moreover" ×8;"Thus" ×6;"In what follows" ×3;"To this end" ×3;"Clearly" ×2。
- **拟人动词库**:模型/损失会 "enjoys / suffers / struggles / copes / ignores / encourages / alleviates"。
- **双斜杠压缩对偶**是签名句法:attracts/disperses、similar/dissimilar、minimizes/maximizes、benchmarks/backbones、accuracy/scalability。
- **Hedging 极少,断言极强**:"we prove"、"demonstrate analytically"、"essentially"、"Clearly"、"profound impact";"may" 仅 5 处。诚实对冲集中在补充材料("The above simple illustration/intuition is by no means an exhaustive proof...")——**正文强攻、附录坦白**的分工。
- "we" 全程主语,方法句一般现在时,结论现在完成时,实验设置用被动。
- **非母语痕迹未清零**:"play important role"、缺 than、结论自家方法名拼错 "COnstrative Laplacian EigenmapS"、"Laplacian Eignemaps"——结论节是校对盲区。

### 10. 可复用模板句库(COLES)

1. [摘要-方法句] "In this paper, we extend the celebrated **[经典方法]** with **[现代成分]**, and call them **[缩写名]**."
2. [摘要-诊断句] "Starting from a **[X]**-inspired formulation, we show that the **[数学对象]** underlying many **[方法族]** models fails under **[退化条件]**, which may naturally emerge during **[实际操作]**."
3. [摘要-优势句] "In contrast, we demonstrate analytically that **[OURS]** essentially minimizes a surrogate of **[更好的数学对象]**, which is known to cope well under **[该退化条件]**."
4. [摘要-实验句] "We show on popular benchmarks/backbones that **[OURS]** offers favourable accuracy/scalability compared to **[点名 3–5 个 baseline]**."
5. [Intro-P1 开局] "Celebrated **[领域]** methods, including **[A]** and **[B]**, **[做什么]** by assuming that **[假设]**. ... In other words, such **[机制]** do not guarantee that **[想要的性质]**."
6. [Intro-P2 过渡+攻击] "In contrast, modern **[领域]** models, often unified under the **[框架名]**, enjoy **[性质]**. ... It relies on **[具体组件]**, which we argue below as suboptimal."
7. [Intro-提案框] "Thus, we propose a new **[名字]** framework for **[任务]**. **[名字]**, derived from **[母框架]**, realizes **[一句话核心思想]**. Our general objective is given as: **[总公式]**"
8. [Novelty 抗辩段] "Novelty. We propose a simple way to obtain **[产物]** which works with numerous backbones. For instance, we obtain **[实例]** by combining **[OURS]** with **[前作 1]** and **[前作 2]**."
9. [理论路线图句] "the key idea of this analysis is to (i) cast **[对手的损失]** as a **[框架]**, and show this corresponds to **[坏性质]** and (ii) cast the objective of **[OURS]** ..., and show it corresponds to **[好性质]**."
10. [结果-归因句] "**[OURS-变体]** outperforms **[对照]** on all **[N]** datasets, which shows that **[OURS]** has an advantage over the **[对照所属框架]**."

---

## 第二篇:GLEN — "Generalized Laplacian Eigenmaps" (NeurIPS 2022)

### 1. 元信息

- 15 页:正文 pp.1–10 → References → **NeurIPS Checklist p.15**。附录另册(正文多处 "Appendix A/D/E/G/I" 引用)——**用附录引用替换 COLES 里写在正文的细节,给正文腾地**。
- 定位:方法+理论,理论权重更高:正文有完整的 Condition/Theorem/Claim/Proposition 体系且证明内联。

### 2. 标题

**"Generalized Laplacian Eigenmaps"** — 与 COLES 完全同构:[升级形容词] + [经典方法原名]。"Generalized" 本身就是续作宣言。缩写:"**G**eneralized **L**aplacian **E**ige**N**maps (GLEN)"。系列命名策略:每篇的名字都是可发音的词,便于口头传播和互引。

### 3. 摘要逐句解剖(9 句)

关键句:
- S1–S2 **与 COLES 摘要前两句逐字相同**——系列品牌化开场白。
- S3 前作定位:"COLES, a recent graph contrastive method combines traditional graph embedding and negative sampling into one framework."(以第三方口吻称呼自己的前作)
- S4 前作再解读:"COLES **in fact** minimizes the trace difference between the within-class scatter matrix encapsulating the graph connectivity and the total scatter matrix encapsulating negative sampling."——**用 "in fact" 把前作翻译进新的数学语言(散布矩阵),前作被重述成即将被推广的特例**。
- S5 升级宣言:"In this paper, we propose a more essential framework for graph embedding, called Generalized Laplacian EigeNmaps (GLEN), which learns a graph representation by maximizing the rank difference between the total scatter matrix and the within-class scatter matrix, resulting in the minimum class separation guarantee."
- S6 障碍(短句制造张力):"However, the rank difference minimization is an NP-hard problem."
- S7 解法:"Thus, we replace the trace difference that corresponds to the difference of nuclear norms by the difference of LogDet expressions, which we argue is a more accurate surrogate for the NP-hard rank difference than the trace difference."
- S8 界声明:"While enjoying a lesser computational cost, the difference of LogDet terms is lower-bounded by the Affine-invariant Riemannian metric (AIRM) and upper-bounded by AIRM scaled by the factor of √m."
- S9 COLES 收尾句复用,baseline 名单换成 "state-of-the-art baselines"(最强对手是自己前作,不便点名)。

### 4. Introduction(3 段 + 贡献,比 COLES 少一段,无 "Novelty." 段)

- P2 段尾把自己的前作放在演化链顶端:"In contrast, COntrastive Laplacian EigenmapS (COLES) [55] is a framework which combines a (graph) neural network with Laplacian eigenmaps utilizing the graph Laplacian matrix within a contrastive loss."——前作成为"最新进展",本文顺势接棒。
- P3 提案段首句直接上"分析+证明"双动词:"In this paper, we analyze the relation among within-class, between-class and total scatter matrices under the rank inequality, and prove that, under a simple assumption, the distance between any dissimilar (negative) samples would be greater/equal than the inter-class distance between their corresponding class centers."
- 泛化声明句:"Based on such a condition, we derive GLEN, a reformulation of graph embedding into a rank difference problem, which is a more general framework than other graph embedding frameworks, i.e., under specific relaxations of the rank difference problem, we can recover different frameworks."
- 贡献 ii 里的括号顺手把前作降格为自己的上界:"(an upper bound of the difference of LogDet terms)"——**贡献列表内嵌续作论证**。

### 5. Related Work

- **位置提前到第 2 节**(COLES 在第 5 节):续作必须先在综述里完成对前作的改写,后文 Claim 1 才有落点。
- **三段炮批评**:"However, such contrastive approaches often require thousands of epochs to converge and perform well. In addition, many contrastive losses have an exponential increase in memory overhead w.r.t. the number of nodes. In contrast, our method does not explicitly use the local-local setting but the total scatter matrix, and thus saves computational and storage cost."(However → In addition → In contrast, our method)
- "缺保证"批评(为自己的 guarantee 卖点铺路):"However, such a family of objective functions is not motivated by the guarantee on the minimum class separation between feature vectors from different categories."
- **收编前作的定音句**:"COLES [55] unifies traditional graph embedding and negative sampling by introducing a positive contrastive term that captures the graph structure, and a negative contrastive random sampling. COLES solves the trace difference problem akin to traditional graph embedding models [43]. In this paper, we propose a more general loss for graph embedding, i.e., COLES solves the trace difference (Nuclear norms difference) relaxation of GLEN."——**先客观转述前作贡献 → 把前作归入某个传统 → 宣布前作是本文框架的一个松弛特例**。

### 6. 方法呈现

- **形式化装置大幅升级**:Condition 1、Theorem 1(带内联证明)、Claim 1、Proposition 1–5(全部内联证明)。分工:
  - **Condition 1** 把理想目标物化成一行可引用的名词,全文反复回指;
  - **Theorem 1** 承载唯一的 guarantee,叙述后一句话点破意义并挂脚注踩对手:"Theorem 1 guarantees the worst inter-class distance§."(脚注:"§Other graph embedding models that maximize/minimize inter-/intra-class distances have no such guarantees.")——**把与前人的对比塞进定理的脚注**;
  - **Claim 1** 专职收编前作:"Claim 1. COLES [55] is a convex relaxation (using the nuclear norm) of the rank difference in Eq. 3";
  - **Proposition 用来"翻译他人/前作",Theorem 留给自己的保证**。
- 能压到 3–6 行的证明内联,长推导外包附录——**从 2021 到 2022 最大的呈现升级:从散文式理论到定理-证明式理论**。
- 直觉句样本:
  - "The nuclear norm ∥·∥∗ can be regarded as the ℓ1 norm over singular values. As the ℓ1 norm induces sparsity, the nuclear norm encourages sparse singular values leading to low-rank solutions."
  - "In the extreme case, if Rank(Sw) = 0, the feature representation collapses."
  - "Thus, we use log det(I + αS) as a smooth surrogate for Rank(S)."
- **统一光谱句**(第三副眼镜把自家新旧两作放进同一个 p-参数族):"The case p = 1 yields the nuclear norm (trace) which makes the 'smoothed' rank difference of GLEN become equivalent of COLES. The opposing limit case, denoted as p = 0 recovers the LogDet formula."——**用一个连续参数族把前作和本作安排成同一光谱的两端,续作合法性论证的数学化**。

### 7. 实验

- **结果讨论新增头号小标题 "COLES vs. GLEN.",置于所有对比块之首——续作的第一场仗是打自己前作**:
> "COLES vs. GLEN. Table 1 shows the performance of GLEN vs. COLES on two different backbones, i.e., GCN and S2GC. On both backbones, GLEN shows non-trivial improvements on all four datasets. GLEN-S2GC outperforms the COLES by up to 4.6%."
- 其余 vs. 块与 COLES 对应段落**近乎逐字复用,仅换方法名和数字**。
- 表格升级:自家方法从"蓝色字"升级为**整行浅绿底纹**(与绿框统一,颜色即品牌);**COLES 作为 baseline 完整保留在表中**——前作降格为表中一行。
- 主表由 COLES 主表直接扩展:同一批 baseline、同一批数字(逐格一致),只追加 GLEN 两行——**实验矩阵的增量式维护**。
- **Ablation**:Table 5 比较 5 种 rank surrogate,行名直接是数学对象,第一行 "GLEN (Nuclear Norm)" 的数字就是 COLES 的数字——**消融表同时是"COLES 是 GLEN 特例"的实验版证词**。
- **6.4 跨域移植**:把 GLEN 装进自家 EASE(CVPR'22)打 few-shot——**用自家产品线互相搭载证明通用性**。
- 劣势补偿句:"Although the LogDet difference is somewhat slower than the trace difference in forward/backward propagation, it converges faster, thus enjoying a similar low runtime."(**"Although [劣势], it [补偿机制], thus [净结论]"**)

### 8. 图

- **Figure 1 = 概念示意图**(与 COLES 的经验证据图角色互换):三个 3D 坐标系手绘示意 Rank 条件的三种情形。Caption 逐视觉元素解码 + 末句限定范围("We show a non-exhaustive set of cases."——caption 内的 hedge,防审稿人挑"还有别的情形")。
- 系列惯例:**一篇一图,图要么当证据(COLES)要么当几何直觉(GLEN),从不画 pipeline 架构图**。

### 9. 微观语言风格(风格漂移)

- 延续:"enjoy(s)" ×5、"outperform" ×14、"In contrast" ×4、斜杠对偶照旧。
- **漂移**:"so-called" 13→2;"In what follows" 被 "Below" ×6 取代;"i.e." 3→13("e.g." 11→5)——**从举例式解释转向重述式解释**,配合更形式化文风;However/Thus 增多(障碍-解决叙事)。
- 断言副词:"in fact"、"Importantly"、"Indeed"。
- 终稿笔误仍在:"contrastvie"、"matrices matrices"、贡献里 "EigenNaps"、checklist 模板说明文字忘删("In your paper, please delete this instructions block...")——**checklist 是最后五分钟填的,不影响录用**。

### 10. 可复用模板句库(GLEN,偏续作场景)

1. [摘要-前作重述] "**[前作名]**, a recent **[类别]** method combines **[成分A]** and **[成分B]** into one framework. **[前作名]** in fact minimizes **[用新语言重写的前作目标]**."
2. [摘要-升级宣言] "In this paper, we propose a more essential framework for **[任务]**, called **[新名]**, which learns **[表示]** by **[新目标]**, resulting in the **[理论保证名]**."
3. [摘要-障碍/解法对] "However, **[理想目标]** is an NP-hard problem. Thus, we replace **[粗糙 surrogate]** ... by **[更好的 surrogate]**, which we argue is a more accurate surrogate for the NP-hard **[目标]** than **[粗糙 surrogate]**."
4. [摘要-界声明] "While enjoying a lesser computational cost, **[我们的量]** is lower-bounded by **[度量]** and upper-bounded by **[度量]** scaled by the factor of **[因子]**."
5. [RW-收编前作句] "In this paper, we propose a more general loss for **[任务]**, i.e., **[前作]** solves the **[某某]** relaxation of **[新作]**."
6. [RW-三段炮批评] "However, such **[方法族]** often require **[代价1]**. In addition, many **[组件]** have **[代价2]** w.r.t. **[规模量]**. In contrast, our method does not **[做那件贵的事]** but **[便宜的替代]**, and thus saves computational and storage cost."
7. [理论-条件命名] "Below we highlight the condition underpinning the subsequent motivation: Condition 1. **[一行数学条件]**."
8. [理论-保证+踩人脚注] "Theorem 1 guarantees **[最坏情形性质]**." + 脚注 "Other **[方法族]** that **[做类似事]** have no such guarantees."
9. [理论-统一光谱句] "The case p = **[值1]** yields **[前作的目标]** which makes the 'smoothed' **[本作目标]** become equivalent of **[前作]**. The opposing limit case, denoted as p = **[值2]** recovers the **[本作]** formula."
10. [实验-打前作句] "**[前作]** vs. **[新作]**. Table 1 shows the performance of **[新作]** vs. **[前作]** on two different backbones... On both backbones, **[新作]** shows non-trivial improvements on all **[N]** datasets."

### 11. 续作八连招(GLEN 如何写"自己前作的推广")

1. **摘要开场白逐字复用**——系列论文的"片头曲"。
2. **"in fact" 重述术**:前作原话里没有 scatter matrix,**续作先把前作翻译进自己的新语言,再在这门新语言里超越它**。
3. **正式收编(数学化的自我批评)**:不贬低前作,而是降维;对前作的"批评"只有一处且完全技术化——**批评自己前作时只指出"它需要额外补丁",从不说它错**。
4. **增量够大的三重证据**:(a) 理论给出前作没有的 guarantee;(b) 统一光谱(前作只是参数族的一个点,实验证明本作端最优);(c) 实验头条位直接打前作("by up to 4.6%")。
5. **前作作为可信度资产**:主表复用前作全部 baseline 数字(可对表验证);版式全套复用。
6. **生态互售**:新作装进自家其他产品线,每篇新作给全家族老产品带一轮新引用。
7. **Checklist**:逐条直答无解释,基础方法研究 societal impact 直接 [N/A]。
8. **压缩换空间**:与前作重复的材料全部外移附录,正文腾出的空间全给新增的定理体系——**续作正文的差异化密度必须高于首作**。

---

## 跨两篇总结

### 共同写作指纹

1. **命名公式**:[修饰词]+[经典方法名] 标题;词内大写凑可发音缩写;"and call them X" 命名仪式。
2. **"致敬经典→揭短→现代化"三步 hook**:引言第一句从不讲应用背景,直接点名经典和它的假设,第 3–4 句亮缺口,第二段 "In contrast, modern..." 引入现代流派并钉死一个具体组件开火。
3. **绿色框体系**:总目标公式放绿色圆角框,结果表自家行同色绿底——**颜色即品牌**。
4. **理论 = 多副眼镜重述同一个损失**:每副眼镜一个小节,输出一条不等式/对偶/界,挂靠一个重量级命名概念借力。数学操作保持初等,深度感来自视角数量与概念挂靠。
5. **公式-直觉交替节奏**:公式块后必跟翻译句;退化情形检查句建立与经典/极端的连续性。
6. **实验四件套**:总纲段定义游戏规则 → Datasets/Metrics/Baselines 粗体段 → "X vs. OURS" 粗体块逐类对手歼灭(win 句配 "which shows that" 归因和 "by up to Z%" 幅度)→ "Scalability." 段具体秒数收官。Ablation 一律设计成理论回验,行名写数学身份。
7. **表格语法**:caption 即说明书、mean±std、无箭头、竖排组标签+组间横线、自家行着色、OOM 与 #Params 当修辞武器、外来数字注明出处。
8. **一篇一图**:证据图或几何直觉图,不画 pipeline;caption = 元素解码+解读+前向引用/范围限定。
9. **微观词库**:enjoys/suffers/encourages 拟人动词;"so-called" 引介借来术语;In contrast/Thus/Moreover/whereas 逻辑骨架;"In what follows / Below" 开场白;双斜杠压缩;hedging 稀少、断言词浓。
10. **瑕疵容忍度**:两篇终稿都带可观的拼写/语法伤仍中 NeurIPS——精力分配:公式与实验矩阵 > 视觉识别系统 > 语言抛光。

### 从 COLES 到 GLEN 的写作演化

| 维度 | COLES (2021) | GLEN (2022) | 演化逻辑 |
|---|---|---|---|
| Related Works 位置 | 第 5 节(理论后) | 第 2 节(引言后) | 续作必须先重写前作史观 |
| 形式化装置 | 0 个编号环境 | Condition/Theorem/Claim/Prop×5 | 卖 guarantee 就必须有 Theorem |
| 图 1 角色 | 经验证据(真实密度曲线) | 概念示意(手绘几何) | 论证重心从现象诊断移向结构条件 |
| 自家标识 | 表中蓝字 | 整行绿底 | 视觉品牌强化 |
| Novelty 防御 | 独立 "Novelty." 段 | 取消,由"泛化=收编一切"承担 | novelty 论证内化为数学结构 |
| 细节安置 | 写正文 | 全部外移附录 | 正文空间让位给定理体系 |
| 复用率 | — | 摘要首尾、实验框架、表格数字、致谢逐字复用 | 固定资产复用,增量全花在差异点 |

**一句话总结**:每篇论文 = 一个经典方法名 + 一个新数学镜头 + 三条 "threefold" 贡献 + 一个绿框总公式 + 多镜头理论重述 + 理论回验式消融 + 自家生态互售;续作再加"in fact 重译前作 → Claim 收编 → 参数族光谱安放新旧 → 实验头条打前作"的标准八连招。
