# 证据报告 01:SSGC (ICLR 2021) + GFB (arXiv 2021)

> 分析对象:Hao Zhu 一作的 "Simple Spectral Graph Convolution"(ICLR 2021,533 引用,代表作)与 "GCN with Generalized Factorized Bilinear Aggregation"(arXiv 2107.11666)。所有引文逐字摘自原文。

---

## Paper A: Simple Spectral Graph Convolution (ICLR 2021)

### 1. 元信息

- **Venue**: ICLR 2021 camera-ready(页眉 "Published as a conference paper at ICLR 2021")
- **页数划分**: 全 15 页 = 正文 1–9 页(第 9 页末为 Conclusions + Acknowledgments,把 camera-ready 的 9 页配额用满)+ 参考文献 10–11 页 + 附录 12–15 页。**实用技巧**:数据集统计表(Table 10、11)被正文引用("as shown in Table 10")但排版在参考文献之后的附录区——把不产生说服力的表格下放,给正文腾空间
- **定位**: 方法论文 + 理论气质装饰。核心贡献是一个**无参数谱滤波器**(对归一化邻接矩阵的 0..K 次幂求平均),配一个线性分类器;理论部分(2 个 Claim + 谱分析)服务于解释与差异化,实验覆盖 4+1 个任务族
- 首页脚注同时放通讯作者声明和代码链接:"The corresponding author. The code is available at https://github.com/allenhaozhu/SSGC."

### 2. 标题

- 模式:**[属性形容词] + [技术域] + [对象]**,三个词的纯名词短语,无冒号、无副标题、无造词。
- 刻意搭上 SGC(Wu et al., "Simplifying Graph Convolutional Networks")的 "Simple X" 血统——读者一眼知道这是 SGC 谱系的下一步,标题本身完成了定位。
- 缩写有巧思:Simple Spectral = S²,得到 S²GC,视觉上是 "SGC 的平方",暗示"比 SGC 强一级"。缩写在摘要里才引入,标题保持全称。
- 标题和全文**零次使用 "novel"**(Paper B 用了 3 次)——代表作反而不标榜新颖性,让 "Simple" 独占标题的形容词位。

### 3. 摘要(全文 9 句,逐句标注)

> "Graph Convolutional Networks (GCNs) are leading methods for learning graph representations."

**背景**,仅 1 句,主系表结构直接封圣研究对象,不绕行 deep learning。

> "However, without specially designed architectures, the performance of GCNs degrades quickly with increased depth."

**问题**。第一个 "However",指出深度退化。

> "As the aggregated neighborhood size and neural network depth are two completely orthogonal aspects of graph representation, several methods focus on summarizing the neighborhood by aggregating K-hop neighborhoods of nodes while using shallow neural networks."

**前人方案**——但注意写法:先用 "As ... are two completely orthogonal aspects" 抛出一个**设计原理**(感受野与深度正交),再把前人(SGC/APPNP)描述为该原理的执行者。这让后文自己的方法也顺着同一原理出场,叙事被作者控制。

> "However, these methods still encounter oversmoothing, and suffer from high computation and storage costs."

**缺口**。第二个 "However" 完成两级收窄(GCN 有问题 → 前人修了但没修好),缺口双维度:效果(oversmoothing)+ 成本(computation and storage)。

> "In this paper, we use a modified Markov Diffusion Kernel to derive a variant of GCN called Simple Spectral Graph Convolution (S²GC)."

**方法**。关键动词是 **"derive"**——方法不是"设计/提出"而是从一个有名字的核**推导**出来的。这一个词就把一行公式的方法抬进了理论传统。

> "Our spectral analysis shows that our simple spectral graph convolution used in S²GC is a trade-off of low- and high-pass filter bands which capture the global and local contexts of each node."

**理论声明 1**(谱刻画):给方法一个信号处理身份,并绑定直觉翻译(low/high-pass ↔ global/local context)。

> "We provide two theoretical claims which demonstrate that we can aggregate over a sequence of increasingly larger neighborhoods compared to competitors while limiting severe oversmoothing."

**理论声明 2**。显式报数 "two theoretical claims"——在摘要里就把理论存在感点清楚,同时 "claims" 一词为后文降格铺路。

> "Our experimental evaluations show that S²GC with a linear learner is competitive in text and node classification tasks."

**实验结果 1**。注意 "with a linear learner" 嵌入结果句——简单性不是单独声明的,而是作为结果的限定语出现("线性学习器都能打"),这是把简单性变成战果的写法。

> "Moreover, S²GC is comparable to other state-of-the-art methods for node clustering and community prediction tasks."

**实验结果 2**(任务广度)。措辞分档:主战场用 "competitive",次战场降为 "comparable"——claim 强度与证据强度对齐。

**摘要配比**:背景 1 / 问题 1 / 前人 1 / 缺口 1 / 方法 1 / 理论 2 / 结果 2。一个无参数滤波器的摘要里理论句占 2/9,这是刻意的重心配置。

### 4. Introduction 段落级解剖(5 段,无 bullet 贡献列表)

**P1(漏斗开局)**。首句:

> "In the past decade, deep learning has become mainstream in computer vision and machine learning."

教科书式大漏斗:deep learning → 非欧数据挑战 → GCN 定义 → MPNN 框架(transformation + aggregation 两函数分解,为后文埋设计空间)。坦率说这段是全文最平庸的部分,hook 不在这里。

**P2(问题段,真正的 hook)**。首句用让步长句堆应用清单再转折:

> "Despite their enormous success in many applications like social media, traffic analysis, biology, recommendation systems and even computer vision, many of the current GCN models use fairly shallow setting as many of the recent models such as GCN (Kipf & Welling, 2016) achieve their best performance given 2 layers."

段内引入 oversmoothing 定义与引用,连残差连接也只能 "merely slows down the oversmoothing issue",最后以一记悖论式警句收尾——这是全 Intro 最抓人的一句:

> "It appears that deep GCN models gain nothing but the performance degradation from the deep architecture."

**P3(设计原理 + 逐个批判前人)**。首句先立原理再引出 SGC:

> "One solution for that is to widen the receptive field of aggregation function while limiting the depth of network because the required neighborhood size and neural network depth can be regarded as two separate aspects of design. To this end, SGC (Wu et al., 2019) captures the context from K-hops neighbours in the graph by applying the K-th power of the normalized adjacency matrix in a single layer of neural network."

段内每批判一个前人立刻插入 "In contrast, we/our"——**批评与自我对照在同一段内成对出现**,不等到贡献段:

> "In contrast, we show that our approach enjoys a free derivative computed in the feed-forward step due to the use of a linear model."
> "...but the weighting scheme favors either global or local context making it difficult if not impossible to find a good value of balancing parameter. In contrast, our approach aggregates over k-hop neighborhoods in a well-balanced manner."

**P4(GDC 批判 + 礼节性引用)**。段末用一个倒装句集中打包三个同方向工作(其中含合作者自引),一石三鸟:

> "Noteworthy are also orthogonal research directions of Sun et al. (2019); Koniusz & Zhang (2020); Elinas et al. (2020) which improve the performance of GCNs by the perturbation of graph, high-order aggregation of features, and the variational inference, respectively."

**P5(贡献段——纯散文,无编号列表)**。开头:

> "To tackle the above issues, we propose a Simple Spectral Graph Convolution (S²GC) network for node clustering and node classification in semi-supervised and unsupervised settings. By analyzing the Markov Diffusion Kernel (Fouss et al., 2012), we obtain a very simple and effective spectral filter: we aggregate k-step diffusion matrices over k = 0, · · · , K steps, which is equivalent to aggregating over neighborhoods of gradually increasing sizes."

注意 "we obtain a very simple and effective spectral filter"——**simple 与 effective 强制配对**,是全文简单性包装的核心公式。段内依次走:机制 → 与 SGC 对比("copes better with oversmoothing")→ 谱结论复述 → 与 APPNP 关系 → 任务清单,收尾:

> "We show that S²GC is highly competitive, often significantly outperforming state-of-the-art methods."

("often" 是这句唯一的 hedge,量词打折但气势不减。)

**段间过渡机制**:P1→P2 靠 "Despite their enormous success"(承接成功、引入短板);P2→P3 靠 "One solution for that"(问题→方案);P3→P4 隐式(继续列前人);P4→P5 靠 "To tackle the above issues"(缺口→贡献)。全部是**首句承接式过渡**,段尾不做预告。

### 5. Related Work

**没有独立的 Related Work 节**——这是本文最特别的结构选择。相关工作被拆到三处:

1. **Intro P3–P4**:对 SGC/APPNP/GDC 的批判性综述(见上);
2. **Section 2 Preliminaries**:以 "带公式的迷你综述" 形式逐方法回顾(Notations → Spectral Graph Convolution → Vanilla GCN → GDC → SGC → Theorem 1 → APPNP),每个方法一个粗体段头 + 核心公式 + 一句缺陷。例:
   > "Although SGC is an efficient and effective method, increasing K leads to oversmoothing. Thus, SGC uses a small K number of layers."
3. **Section 3.3 四个 "Relation of S²GC to X" 粗体段**(GDC / APPNP / AR / JKN),在方法给出之后做逐一对比切割。

**批评句式**三种典型:

- 让步-转折-成本型:"Although APPNP relieves the oversmoothing problem, it employs a non-linear operation which requires costly computation of the derivative of the filter due to the non-linearity over the multiplication of feature matrix with learnable weights."
- 能力承认-代价否决型:"GDC has more expressive power than SGC (Wu et al., 2019), PPNP and APPNP (Klicpera et al., 2019a) but it leads to a dense transition matrix which makes the computation and space storage intractable for large graphs, although authors suggest that the shrinkage method can be used to sparsify the generated transition matrix."(连对方的补救措施都先替对方说出来再否掉)
- **引用对手原文自证其弱**:"Klicpera et al. (2019b) explain that 'most graph diffusions result in a dense matrix S'."——直接拿 GDC 作者自己的句子当弹药,这是最高效也最不可辩驳的批评方式。

### 6. 方法呈现

- **Notation**:集中在 Section 2 开头一个 "Notations." 粗体段(约 10 行)建立 G、A、D、X、L、特征分解,之后不再重复。
- **理论环境计数**:Theorem ×1(**借来的**,标注 "(Chung & Graham, 1997)")、Claim ×2、Definition ×2(仅在附录 A.5)、Proposition/Lemma ×0。
- **各环境的修辞分工非常清晰**:
  - **Theorem 1 是打击 baseline 的武器**,不是关于自家方法的结果——它证明的是 SGC 为什么会 oversmooth("SGC also suffers from oversmoothing as K → ∞, as shown in Theorem 1");
  - **自家结论降格叫 "Claim"**——既在摘要里享受 "two theoretical claims" 的话语权,又避免被审稿人用定理的严格标准苛责。附录里的"证明"实际是启发式论证(欧氏格点特例 + 随机游走半径近似),作者自己承认 "While the above approximations may be loose for very small/large t, the important property to note is that r(i, 0, n) ≤ r(i, 1, n) ≤ · · ·";
  - **Definition A.1/A.2(expansion、k-way Cheeger constant)纯属格调装饰**:正文只有一句带过 "Similar findings can be noted by carefully considering the meaning of so-called Cheeger constant introduced in Section A.5."
- **Claim 的双重陈述策略**:Claim I/II 在正文 3.1 完整陈述一遍,附录 A.4 再逐字重述一遍才证明;Theorem 1 同样主文 + 附录("Recall Theorem 1, that is...")。审稿人不用翻页对照。
- **Claim 直接钉到实验表**——理论声明与实验证据在同一段短接:
  > "This is substantiated by Table 8, where S²GC achieves the best results for K = 16, whereas SGC achieves poorer results by comparison, whose peak is at K = 4 (note that larger K is better)."
- **数学与直觉交替**:几乎每个数学陈述后跟一句白话翻译,信号词是 "In other words / That is / To see this clearer":
  > "In other words, as K grows, this filter includes larger and larger neighborhood but also maintains the closest locality of nodes."
  > "That is, smaller neighborhoods belong to larger neighborhoods too."
  > "Two nodes are considered similar when they are diffused in a similar way through the graph, as then they influence the other nodes in a similar manner (Fouss et al., 2012)."(先直觉后数学的倒序也有)
  附录里连参数都配直觉:"λ₂ being the second largest eigenvalue intuitively denotes the graph connectivity (large λ₂ ≤ 1 indicates low connectivity while low λ₂ indicates high connectivity in graph)"。
- **方法主线是"从缺陷推进"**:Eq.11(核心一行公式)→ Eq.12(K→∞ 时是 Laplacian 正则化问题的最优解,把方法接到 Zhou et al. 2004 经典上)→ 立刻自我否定并修正:
  > "However, the infinite expansion resulting from Eq. 12 is in fact suboptimal due to oversmoothing. Thus, we include in Eq. 11 a self-loop T̃⁰ = I, the α ∈ [0, 1] parameter (Table 9 evaluates its impact) to balance the self-information of node vs. consecutive neighborhoods, and we consider finite K."
- **证明位置**:全部在附录 A.4(注意正文说 "described in Section A.3" 是**交叉引用错误**,A.3 实际是 Graph Classification——camera-ready 仍有此级别失误)。
- 方法节末尾必有 **Complexity Analysis 小节**(3.4):分 forward/backward 两阶段给 big-O 表(Table 1),再落到 wall-clock:"Table 2 demonstrates that APPNP is over 66× slower than S²GC on the large scale Products dataset (OGB benchmark) despite, for fairness, we use the same basic building blocks of PyTorch among compared methods."

### 7. 实验

- **小节组织**:按任务切 4+1 小节(4.1 Node Clustering / 4.2 Community Prediction / 4.3 Node Classification / 4.4 Text Classification / 4.5 消融)。**广度即论证**——每个任务表都不大,但任务族数量本身支撑 "simple yet general" 的叙事。
- **Baseline 的分类学列举**(不平铺,先建 taxonomy 再填名字):
  > "We compare S²GC with three variants of clustering: (i) Methods that only use node features ie., k-means and spectral clustering (spectral-f)... (ii) Structural clustering methods that only use graph structures... and (iii) Attributed graph clustering methods that utilize both node features and graph structures..."
- **表格设计细节**(PDF 已核对):
  - 全部用 **±std**("averaged over 10 runs" 写在 caption),无上下箭头、无 "higher is better" 标注;
  - **粗体 = top-1**(正文明说 "top-1 results are highlighted in bold"),自家方法固定放**最后一行并加分组横线**;
  - Table 3 带 "Input" 列(Feature/Graph/Both)——用一列元信息替读者做方法分类;
  - **Table 4 用 "Setting" 分组列讲故事**:Supervised / Unsupervised / No Learning 三组,自己放 "No Learning" 组拿 95.3(与监督组最优 95.4 同为粗体)——表格结构本身完成了 "不学习打平监督" 的论证;
  - Table 6 用横线把高容量组(MLP/GCN/GraphSage)与线性组(Softmax/SGC/S²GC)分开,输给 GraphSage 的 Products 列**照实粗体对手**;
  - Table 8(K 消融)行=方法、列=K∈{2,...,64}、每数据集一个行块,粗体标各法峰值位置——设计目标是让 "GCN 峰值在 2、SGC 在 4、S²GC 在 16" 一眼读出,**这张表就是 Claim II 的可视化**。
- **结果讨论句式**(表号 + shows/suggests/demonstrates + 结论,再接 Thus 因果化):
  > "Table 7 shows that S²GC rivals their models on 5 benchmark datasets."
  > "Overall, the results suggest that S²GC can aggregate over larger neighborhoods better than SGC while suffering less from oversmoothing."
  > "The table shows that α slightly improves the performance of S²GC. Thus, balancing the impact of self-loop by α w.r.t. other filters of consecutively larger receptive fields is useful but the self-loop is not mandatory."(注意对自家超参的诚实降调 "slightly...not mandatory")
- **输了怎么写——败绩转化术**(全文最值得学的一段):在 OGB 上打不过 GCN/GraphSage,处理方式是归因 → 提出验证实验 → 用增强变体反杀:
  > "On Arxiv and Products, our method cannot outperform GCN and GraphSage while MLP outperforms softmax classifier significantly. Thus, we argue that MLP plays a more important role here than the graph convolution. To prove this point, we also conduct an experiment (S²GC+MLP) for which we use MLP in place of the linear classifier, and we obtain a more powerful variant of S²GC."
- **Ablation 组织**:独立小节 4.5,只有两个小表(K 扫描、α 扫描),每表对应一个设计选择,且 K 扫描直接回扣理论 Claim。超参声明主动免疫 "调参质疑":
  > "Following that, we fixed K = 16 and α = 0.05 across all datasets so K and α are not tuned to individual datasets at all."

### 8. 图

- **全文只有 1 张图**,且不是框架图/流程图,而是**理论 teaser**:Figure 1 两联曲线图,(a) 滤波器响应函数随 K 变化,(b) Cora 上真实特征值 vs 滤波后特征值。位置在 Methodology 节开头(第 4 页顶),读者进入方法节前先看到滤波器的"形状"。
- **Caption 纯数学描述、零解读**:
  > "Figure 1: (a) Function f(λ) = (1/K)Σ_{k=0}^K λ^k with λ ∈ [−1, 1], K ∈ {1, 4, 8, 16}; (b) Sorted by index, eigenvalues of D^{−1/2}AD^{−1/2} and push-forward eigenvalues f(Λ) = (1/K)Σ_{k=0}^K Λ^k on Cora network (K = 16)."
  解读全部留在正文:"is plotted in Figure 1, from which we observe the following properties: (i) Z(K) preserves leading (large) eigenvalues of T and (ii) the higher K is the stricter the low-pass filter becomes but the filter also preserves the high frequency."
- 没有任何 pipeline/architecture 示意图——方法足够简单到一个公式说完,作者索性不画,把唯一的图预算花在"理论证据"上。

### 9. 微观语言风格(基于全文词频统计)

- **因果推进三件套**(方法节的发动机):**Thus ×16、However ×8、In contrast ×11**。基本节奏是 "However [前人/上一版缺陷]. Thus, we [修正]. In contrast [与对手切割]"。
- **插入语习惯**:**Note that ×9**、We note ×2、Moreover ×9、That is, ×5、In other words ×2、To see (this/that) ×3、It is easy to (see/note) ×2、so-called ×3、w.r.t. ×3。"To this end" 仅 1 次(不是口头禅)。
- **节首路标句**:"Below, we..." ×5,每个大节开头必有一段无编号 roadmap。
- **"we" 的用法**:高密度、无被动偏好、无 "I";"we" 兼指作者行为("we propose")与作者携读者推导("we observe", "we have L̃H − X = 0");表格中自称 "Ours"。
- **时态**:正文与方法一般现在时;实验操作用过去时("We ran our experiments", "we trained our method");结论整段现在完成时("We have proposed... We have shown... We have conducted...")。
- **claim 强度**:结果句强但带量化 hedge("highly competitive, **often** significantly outperforming"、"rivals"、次要任务降档为 "comparable");机制句敢下断言("It appears that deep GCN models gain nothing but...");对自家不利处不藏("slightly improves"、"may be loose"、"cannot outperform")。**hedge 集中花在两处:副词量词和附录近似声明,主干结论不打折。**
- **抛光水平**:非标准缩写 "ie.,";多处笔误进入 camera-ready——"Vanila Graph Convolutional Network"(节标题)、"Table 8 summaries / Table 9 summaries"(应为 summarizes)、"For baselines, We include"(句中大写)、A.3/A.4 交叉引用错位。**结论:该风格的强项在结构调度,校对水平明显低于结构水平——模仿时学骨架,勿学抛光。**

### 10. 可复用模板句库(Paper A)

| # | 英文骨架(挖空) | 用途位置 |
|---|---|---|
| 1 | "However, without ___, the performance of ___ degrades quickly with ___." | 摘要问题句 |
| 2 | "In this paper, we use a modified ___ to **derive** a variant of ___ called ___." | 摘要方法句(用 derive 抬理论身价) |
| 3 | "Our ___ analysis shows that ___ is a trade-off of ___ and ___ which capture the ___ and ___ of each ___." | 摘要/结论理论句 |
| 4 | "We provide two theoretical claims which demonstrate that we can ___ compared to competitors while limiting ___." | 摘要理论句(显式报数) |
| 5 | "It appears that ___ gain(s) nothing but ___ from ___." | Intro 问题段收尾警句 |
| 6 | "One solution for that is to ___ while limiting ___, because ___ and ___ can be regarded as two separate aspects of design. To this end, ___ [does X]." | Intro 由原理引出前人 |
| 7 | "Although ___ relieves the ___ problem, it employs ___ which requires costly ___. In contrast, we show that our approach enjoys ___." | 批评前人 + 即时自我对照 |
| 8 | "Noteworthy are also orthogonal research directions of ___; ___; ___ which improve ___ by ___, ___, and ___, respectively." | 礼节性打包引用 |
| 9 | "Below, we firstly outline ___. Moreover, we analyze ___. Based on ___, we present ___ and discuss its relation with other models. Finally, we provide ___." | 方法节 roadmap |
| 10 | "However, the ___ resulting from Eq. _ is in fact suboptimal due to ___. Thus, we include in Eq. _ ___ to balance ___, and we consider ___." | 方法内"自我修正"过渡 |
| 11 | "In fact, ___ and ___ are only equivalent if ___, ___ and ___." | Relation-to 段,退化条件切割相似工作 |
| 12 | "This is substantiated by Table _, where ___ achieves the best results for ___, whereas ___ achieves poorer results by comparison, whose peak is at ___." | 理论 claim 直连实验表 |
| 13 | "Thus, we argue that ___ plays a more important role here than ___. To prove this point, we also conduct an experiment (___) for which we ___, and we obtain a more powerful variant of ___." | 实验败绩转化 |
| 14 | "We have conducted extensive and rigorous experiments which show that ___ is competitive frequently outperforming many state-of-the-art methods on ___, ___ and ___ tasks given several popular dataset benchmarks." | 结论收尾 |

### 11. 卖点包装策略:如何把"一行公式"卖成 ICLR

S²GC 的本体是 Ŷ=softmax((1/K)Σₖ T̃ᵏXW)——无参数滤波 + 线性分类器。作者用了七层包装:

1. **命名占位**:标题的 "Simple" 抢先把简单性据为卖点而非弱点,并挂靠 SGC 血统;缩写 S² 暗示升级关系。
2. **"推导"而非"设计"**:方法从命名数学对象(Markov Diffusion Kernel, Fouss et al. 2012)"derive" 出来,公式出场前铺垫 1.5 页核背景。同一个求和平均,换个来源叙述,格调完全不同。
3. **多重理论皈依**:同一行公式被同时接入四个理论传统——扩散核(MDK)、经典半监督学习(接 Zhou et al. 2004)、谱滤波(Fig.1 低/高通 trade-off)、谱图分割(附录 Cheeger 不等式)。**理论不为证明存在,为"这不是 trick,是必然结果"的叙事存在。**
4. **定理外借、结论降格**:唯一的 Theorem 是引用来打 SGC 的;自家理论叫 Claim,启发式证明放附录并诚实标注近似松紧。既有理论气质又不承担定理级审查。
5. **简单性变现为速度与规模**:Complexity Analysis + big-O 表 + "over 66× slower" 秒表数 + "free derivative computed in the feed-forward step"——把 "没有非线性" 从表达力短板重写为工程优势。
6. **预答 "这不就是 X 吗"**:四个 "Relation of S²GC to X" 段用公式级退化条件逐一切割(与 APPNP 仅在 α=0.5, K=1, f 线性时等价),这是对审稿人最可能的攻击的正面防御工事。
7. **广度补深度**:单点提升不大(citation 网络上 +0.2~+1.0),就铺 4 个任务族 + OGB + 附录图分类,再加"超参跨数据集固定不调"的稳健性声明,让"简单方法处处能打"成为核心证据形态。

---

## Paper B: GCN with Generalized Factorized Bilinear Aggregation (arXiv 2021)

### 1. 元信息

- **Venue**: arXiv 预印本(arXiv:2107.11666v1),NeurIPS 投稿模板。首页脚注有防剽窃声明 + 代码链接 "https://github.com/allenhaozhu/GFBP"
- **页数划分**: 全 15 页 = 正文 1–10 页 + 附录 A–C 第 10–13 页 + 参考文献 13–15 页
- **定位**: 方法论文(GCN 聚合层组件),主战场单任务(text classification),附录扩两个任务。与 Paper A 相反方向:A 是做减法(去参数),B 是做加法(给聚合加二阶项)

### 2. 标题

- 模式:**[基座架构] + with + [机制全称]**,8 个词,同样无冒号无造词。机制名本身是三个技术形容词堆叠(Generalized Factorized Bilinear)——把贡献的三层结构(二阶 → 因子化 → 广义化)全部编码进标题。

### 3. 摘要(全文 7 句,两轮"问题-方案"循环)

> "Although Graph Convolutional Networks (GCNs) have demonstrated their power in various applications, the graph convolutional layers, as the most important component of GCN, are still using linear transformations and a simple pooling step."

**背景 + 缺口一句合并**:让步句式把研究对象的成功与其组件的原始性同框,"as the most important component" 顺手抬高攻击目标的地位。

> "In this paper, we propose a novel generalization of Factorized Bilinear (FB) layer to model the feature interactions in GCNs."

**方法**(第 2 句就出方法,比 A 快得多)。

> "FB performs two matrix-vector multiplications, that is, the weight matrix is multiplied with the outer product of the vector of hidden features from both sides."

**方法机制**:向读者解释被移植的工具本身("that is" 复述)。

> "However, the FB layer suffers from the quadratic number of coefficients, overfitting and the spurious correlations due to correlations between channels of hidden representations that violate the i.i.d. assumption."

**二级缺口**——对自己刚引入的工具开刀。GFB 摘要的独特结构:**gap→naive 方案→naive 方案的 gap→真方案**,两轮问题-方案循环压进 7 句里。

> "Thus, we propose a compact FB layer by defining a family of summarizing operators applied over the quadratic term."

**修正后的方法**。"a family of" 是重要措辞——单个算子被包装成算子族。

> "We analyze proposed pooling operators and motivate their use."

**理论声明**(最弱的一句,只承诺 analyze/motivate,不承诺证明)。

> "Our experimental results on multiple datasets demonstrate that the GFB-GCN is competitive with other methods for text classification."

**实验结果**。摘要收在 "competitive",但正文结果段膨胀为 "significantly outperforms all other models"——摘要与正文的 claim 强度不一致,是预印本纪律松弛的痕迹。

### 4. Introduction(5 段 + 编号贡献列表)

**P1(应用域开局)**:"Text, as a weakly structured data, is ubiquitous in e-mails, chats, on the web and in the social media, etc." 从任务域(文本)而非技术域开局——与 A 的开局镜像。

**P4(缺口段,双 However)**:

> "An aggregation function often realizes a permutation-invariant function that captures so-called pooled statistics by sum-, mean-, max-pooling etc. However, these operators are based on first-order statistics. In contrast, bilinear pooling [10] captures second-order statistics, which represent better the underlying probability density function of data. However, bilinear pooling applied to GCNs as a local pooling is costly due to its large number of parameters."

四句完成:现状 → 一阶局限 → 二阶更好(引入救兵)→ 救兵太贵(留下自己要填的缺口)。

**P5(方案段)**:"In this paper, we introduce a Factorized Bilinear (FB) model that is generalized and compact, with the goal of enhancing the capacity of graph convolutional layers **in a simple manner**."——加法论文也要声明简单性。

**贡献列表**(i/ii/iii 三条):配方是经典三件套 **(i) 机制引入 (ii) 使之可行 + 理论洞察 (iii) 实验验证**。

### 5. Related Work

- **位置**:标准的 Section 2,三小节按 **"任务 / 载体 / 机制" 三轴组织**(Text Classification / GCN / Higher-order Pooling),每一轴的结尾埋一句指向自己的缺口。
- **靶心句**(全称否定声明空白):"However, no GCN methods use pairwise feature interactions by considering second-order pooling."(放在 2.2 结尾)
- 2.3 结尾把前人的做法收编为自己框架的特例:"[39, 5] give a simple method to reduce the size of representation by picking up the diagonal elements from high-order representations. In this paper, we propose a generalized framework and discuss four different methods to reduce the size of representations."

### 6. 方法呈现

- **理论环境计数:Theorem/Proposition/Lemma/Definition 全部为 0。** 理论以三种替代形态存在:(1) 编号不等式链把四个算子按响应强度排序;(2) 一个**排版加框的段落**充当"主定理"的视觉替身("Notably, if p₂ = 1, MaxVec acts as a linear function w.r.t. p₁. ... which validates our claim that the Factorized Bilinear model acts as a low-rank modulator of level of non-linearity if paired with our MaxVec operator.");(3) 挂靠时髦概念("our theoretical analysis shows that, in fact, our Compact Vectorization applied to Factorized Bilinear Transformation **acts as a factorized attention**")。
- **方法结构是教科书级的"渐进修复链"**,每小节结尾的缺陷句就是下一小节的动机:
  - 4.1 → "However, the use of auto-correlation matrix as a node representation is computationally inefficient due to the large size of W_l in Eq. 4, which leads to overfitting. Thus, we introduce a factorized model with a smaller number of parameters."
  - 4.2 → "Although this saves computations and reduces overfitting by low-rank approximation, compared to Eq. 4, it still requires matrix-vector multiplications which yield a representation of k × k such that k² ≫ d. Thus, we consider below a compact summarization of matrices which further reduces the size of our representation."
- Section 4 开头的 roadmap 把每一步的缺陷都预告了。
- **数字例子降门槛**:"this indicates that for the representation h_u^(l−1) is of 16 dimension size, the second-order representation is of 256 dimensions (136 assuming coefficients of the upper-triangular). Stacking few layers together results in the feature size blown out of proportions."
- **"performs two roles + Firstly/Secondly" 双角色框架**:"Below, we demonstrate that our MaxVec pooling, our best performing pooling variant, performs two roles. Firstly, ... Secondly, ..."

### 7. 实验

- **没有独立 ablation 小节——四个 GenVec 变体作为主表的最后四行,变体族本身就是消融**。
- **Caption 当注释区用**(把不利实验的缺席理由写进 caption):
  > "For Bilinear Pooling (BP), we did not report results as experiments would require 20 days of 10 GPUs to run (e.g., 863.1 seconds per epoch, 200 epochs, 10 runs for 20NG). However, on R8 (smallest dataset), Text GCN+BP yields 0.9682±0.0042."
- **粗体规则的猫腻**:20NG 列上 Text SGC 0.8853 是全表最高,但粗体给了自家 0.8718;正文用一句话把 SGC 排除出可比集:"Note that SGC do not have hidden layer, thus the embedding of words and documents for 20NG are over 10000 size, which makes SGC gain advantage."——**"先全称宣胜、再脚注式豁免反例"**;学其结构、慎用其强度(与表内数据冲突,投稿版会被抓)。
- **指标切换找显著性**:accuracy 提升平平时,附录切 macro-P/R/F1 并绑定不平衡叙事("The results in Table 4 show significant improvements in terms of macro-recall and macro-F1, which shows that our method can classify correctly samples belonging to categories with very limited training samples.")
- 额外卖点段 "Fast Convergence...":用早停 epoch 数做收敛速度证据 + 机制归因。

### 8. 图

- **Figure 1**:2×2 四宫格 3D 响应曲面。仍然**不是框架图而是理论插图**。Caption 极简标签式。解读放正文,**逐子图一段走读**,四段构成 "劣 → 优 → 上界 → 退化" 的叙事序列,图序即论证序:"Figure 1(a) shows that MeanVec is a non-linear operator, however, as p₂ → 0, ... which is an undesired effect as p₁ → 1 indicates high confidence... " / "Figure 1(b) shows that MaxVec solves the above issue..."
- 两篇合计 3 张图,全部是函数/统计图,零 pipeline 图。

### 9. 微观语言风格

- **However ×14、Thus ×12、Below ×11**(Below 密度是 A 的两倍)。In contrast 仅 2 次(A 有 11 次——A 需要切割四个近邻方法,B 没有近身竞品)。
- **In this paper ×5**(A 仅 1 次)、we propose ×8、we introduce ×6、**novel ×3**、e.g. ×10、Notably ×2、so-called ×2、with the goal of ×2。
- claim 词汇更膨胀;hedge 几乎不用(may ×1)。英式/美式拼写混用。**笔误密度显著高于 A**(预印本状态)。

### 10. 可复用模板句库(Paper B)

| # | 英文骨架(挖空) | 用途位置 |
|---|---|---|
| 1 | "Although ___ have demonstrated their power in various applications, ___, as the most important component of ___, are still using ___ and ___." | 摘要开局(背景+缺口合并) |
| 2 | "However, the ___ suffers from ___, ___ and ___ that violate the ___ assumption. Thus, we propose a compact ___ by defining a family of ___ applied over ___." | 摘要二级缺口→方案 |
| 3 | "___, as a ___ data, is ubiquitous in ___, ___, and ___." | 应用域 Intro 开局 |
| 4 | "However, these operators are based on first-order ___. In contrast, ___ captures ___, which represent better ___. However, ___ applied to ___ is costly due to ___." | Intro 缺口段(引救兵→救兵太贵) |
| 5 | "However, no ___ methods use ___ by considering ___." | Related Work 靶心句(全称否定声明空白) |
| 6 | "Our contributions are three-fold: i. We introduce ___ into ___ that captures ___. ii. For ___, to make it computationally applicable, we propose a novel family of ___. iii. We validate the effectiveness of our approach on several standard benchmarks." | 贡献列表整体框架 |
| 7 | "Below, we ___. In Section _._, we outline ___ whose ___ is unacceptable due to ___. In Section _._, we introduce ___ which lets ___. ..." | 方法节 roadmap(预告每步缺陷) |
| 8 | "However, ___ is computationally inefficient due to ___, which leads to overfitting. Thus, we introduce a ___ with a smaller number of ___." | 渐进修复链的关节句 |
| 9 | "Although this saves ___ and reduces ___ by ___, it still requires ___ which yield ___ such that ___. Thus, we consider below ___ which further reduces ___." | 第二级修复关节句 |
| 10 | "Below, we demonstrate that our ___, our best performing ___ variant, performs two roles. Firstly, ___. Secondly, ___." | 机制分析节开场 |
| 11 | "Figure _(a) shows that ___ is ___; however, as ___ → 0, ..., which is an undesired effect as ___. Figure _(b) shows that ___ solves the above issue, e.g., ..." | 逐子图走读(劣→优序列) |
| 12 | "For ___, we did not report results as experiments would require ___ to run (e.g., ___ seconds per epoch, ___ epochs, ___ runs for ___)." | 表格 caption 内解释缺席的 baseline |
| 13 | "Compared with the vanilla ___, the proposed methods only slightly increase computation cost (__%-__%)." | 代价坦白句 |

### 11. 卖点包装策略

1. **"Generalized" 前缀的收编术**:把前人的 diagonal 取法收编为自家框架特例(DiagVec),把 2-way FM declare 为 "a special case of our FB model"——单点技巧升维成框架。
2. **算子族命名**:一个 row-wise 汇总函数被铺成四件套(MaxVec/MeanVec/DiagVec/TopkVec)并各起专名;族的存在自动生成消融表、复杂度对比和讨论素材。
3. **理论替身**:没有定理,就给不等式链 + 加框段落 + 概念嫁接("acts as a factorized attention")。
4. **荒谬化 naive baseline**:BP 的 "20 days of 10 GPUs" 写进 caption。
5. **指标切换找显著性** + **速度+收敛双副卖点**。

---

## 跨篇总结:两篇共同的写作指纹

**结构指纹**
1. **"Below, we..." 节首路标**(合计 16 次):每个 section/subsection 用一段无编号 roadmap 开场,常常连每一步的缺陷都预告。
2. **粗体 run-in 段头**代替四级标题:"Notations." / "Relation of S²GC to APPNP." / "Baselines." / "Implementation details."——最显眼的排版签名(Koniusz 组风格)。
3. **Preliminaries 兼任 Related Work**:逐方法 "命名段头 + 公式 + 一句缺陷" 的迷你综述;A 甚至完全取消独立 Related Work 节。
4. **方法 = 渐进修复链**:上一版的缺陷句就是下一小节的动机句,推进引擎统一为 "However [缺陷]. Thus, we [修复]",A 中 Thus ×16、B 中 ×12。
5. **必有 Complexity Analysis 小节 + wall-clock 表 + 数量级金句**("over 66× slower" / "two orders of magnitude slower")——效率永远是第二卖点。
6. **附录当泄压阀**:证明、次要任务、超参细节、数据统计表全部下放;正文保持"声明 + 指针"。

**理论包装指纹**
7. **借名对象做推导来源**(Markov Diffusion Kernel / Factorization Machine / bilinear pooling 谱系),用 "derive/generalize" 动词把小改动接入大传统。
8. **定理外借打 baseline,自家结论降格**为 Claim(A)或不等式+加框段(B),启发式论证 + 诚实的近似声明放附录。
9. **理论声明直连实验表**("This is substantiated by Table 8, where...")、消融表按理论预言设计。

**实验与图表指纹**
10. 表格:±std 必带、按方法家族加横线分组、自家方法末行、bold=top-1 但**对打不过的反例用正文一句话豁免而非加粗**;caption 是完整句子并承载协议信息乃至缺席理由。
11. **零框架图**:仅有的图全是函数曲线/响应面/统计柱,充当"理论 teaser";caption 纯描述性标签,解读一律在正文逐子图走读。
12. 败绩处理三段式:承认("cannot outperform")→ 归因("Thus, we argue that ___ plays a more important role")→ 加一个实验反杀("To prove this point, we also conduct...")。

**语言指纹**
13. 连接词全家桶排位(两篇合计):Thus 28 > However 22 > Below 16 > Note that/We note 15 > In contrast 13 > Moreover 11 > e.g. 11 > That is/ie. 9 > so-called 5 > w.r.t. 6。**"To this end" 不是他的口头禅(仅 1 次)**,真正的口头禅是 "Below, we" 和 "Note that"。
14. we-主语高密度、无被动偏好、无 I;正文现在时、实验操作过去时、结论现在完成时("We have proposed/shown/conducted")。
15. 每个数学陈述配一句白话("In other words / That is / To see this clearer")。
16. "simple/simply" 两篇合计 26 次,标配搭档是 "simple and effective / in a simple manner"——无论做减法还是加法,简单性都被写成卖点。
17. **抛光水平系统性偏低**:camera-ready 仍有笔误。模仿时:学它的结构调度、修复链推进、理论挂靠与表格叙事;**校对与 claim-数据一致性必须自行把关到更高标准**。
