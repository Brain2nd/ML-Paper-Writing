# 证据报告 07:段间关系普查 + 跨章缝合 + Conclusion 逐句(SSGC / COLES / EASE / BiLoRA)

> 4 篇全文(Introduction→Conclusion)每个自然段交界逐一标注;段落边界经 PDF 原版面逐页核对(单栏靠段间垂直空距、双栏靠首行缩进;公式后小写接续行判为同段)。引文逐字。

## 交界装置分类(9 型)

| 代号 | 定义 |
|---|---|
| A | 显式承接算子:However/Thus/Moreover/In contrast/Despite/Instead of/Compared with/To this end 等句首连接词或目的式 |
| B | 回指词承接:the above ___/such ___/this ___/aforementioned/公式号定理号回指 |
| C | 粗体 run-in 段头制:段间关系由粗体小标题承担,段首句本身不承接 |
| D | 路标句制:"Below, we…"/"In what follows…"/"In this section…" 预告后文 |
| E | 冷启动:无显式装置直接开新话题(含数学冷启动 Let/Given 与断言式主题句) |
| F | 编号/列表制:(i)(ii)、罗马数字、Claim I/II、Theorem 编号 |
| G | 词汇链承接:上段的专名/术语/符号原样搬入下段首句作锚(上段谈 APPNP,下段首句 "GDC … further extends APPNP") |
| H | 范围状语开段:"For X, …/On dataset Y, …/In the case of Z, …"——状语本身声明并列/枚举关系 |
| T | 图表锚点开段:段首句主语就是 "Table N/Figure N/Algorithm N",编号承担排序与衔接 |

逻辑关系(与装置分列):递进深化 / 并列展开 / 转折反驳 / 让步后转折 / 因果承接 / 实例化具体化 / 总分 / 分总 / 新对象引入 / 回环呼应。

---

## 任务 1:段落交界普查(节选代表性交界 + 全量统计)

### SSGC(ICLR 2021,40 交界)代表性样本

**Intro(4 交界,全部 A/B/G)**:
- P1→P2 [A 让步后转折]:"Despite their enormous success in many applications like social media, traffic analysis, biology, recommendation systems and even computer vision, many of the current GCN models use fairly shallow setting…"——让步从句复述上段成就再拐弯。
- P2→P3 [B 因果]:"One solution for **that** is to widen the receptive field of aggregation function while limiting the depth of network…"——回指代词 "that" 收编整段问题。
- P3→P4 [G 并列]:"GDC (Klicpera et al., 2019b) further extends **APPNP** by generalizing…"——上段专名 APPNP 作宾语接续。
- P4→P5 [B 因果收束]:"**To tackle the above issues**, we propose a Simple Spectral Graph Convolution (S2GC) network…"——一次收编 P2–P4 全部罪状。

**Method 关键交界**:
- 3.2→3.3 [B,全文枢纽]:"**Based on the aforementioned Markov Diffusion Kernel**, we include self-loops and propose the Simple Spectral Graph Convolution (S2GC) network…"——aforementioned 全语料仅此 1 例,用在原理→方案的最重要拐点。
- 推导链内 [B 公式回指]:"By defining Z(K) = 1/K ΣK k=1 Tᵏ, we reformulate **Eq. 8** as the following metric:"
- 对照块内 [A×4]:"In contrast, our approach is simply computed as…"/"In contrast, we use the linear function XW."
- 成本段 [H]:"For S2GC, the storage costs is O(|E| + nd)…" → "For the backward stage including computations of the gradient…"(前向账→后向账,范围状语并列)
- 收束 [T 分总]:"Table 1 summarizes the computational and storage costs of several methods."

**Experiments 关键交界**:
- 4.1→4.2 [G]:"We **supplement our social network analysis** by using S2GC to inductively predict the community structure on Reddit…"——动词短语自带"补充"定位。
- 4.2→4.3 [H 并列]:"For the semi-supervised node classification task, we apply the standard fixed training, validation and testing splits…"
- 4.3→4.4 [E 冷启动并列]:"Text classification predicts the labels of documents."(零装置,小节标题独扛)
- 4.4→4.5 [T 递进]:"Table 8 summaries the results for models with various numbers of layers…" → 4.5 内 [T 排比]:"Table 9 summaries the results for the proposed method for various α…"

### COLES(NeurIPS 2021,44 交界)代表性样本

- Intro P2→P3 [A 因果]:"Thus, we propose a new COntrastive Laplacian EigenmapS (COLES) framework…"——且上段段尾已埋前向 "which we argue below as suboptimal"(双保险)。
- §2.1 末=**整段桥**(全语料唯一):"In what follows, we argue that the choice of sigmoid for σ(·) leads to negative consequences. Thus, we derive COLES under a different choice of sΘ(v,u) and s̄Θ(v,u′)."
- 理论节推导 [B]:"**The above analysis** shows that traditional contrastive losses are bounded by the JS divergence."(分总定罪)
- 理论节 [G+框]:"By the Kantorovich-Rubinstein duality [45], **the optimal transport problem for COLES** can be equivalently expressed as:"(词汇链+绿框加冕)
- 4.3 内镜像排比 [G]:"Wang and Isola [47] have decomposed the SoftMax contrastive loss into Lalign and L′uniform:" → "COLES can be decomposed into Lalign and Luniform [47] as follows:"(句式镜像=对比论证)
- 实验 [C+T ×多]:"**Contrastive Embedding Baselines vs. COLES.** Table 2 shows that…"/"**Semi-supervised GNNs vs. COLES.** Table 2 shows that…"(段头+表锚)
- 6.1→6.2 [B+T,**回环**]:"**Following the analysis presented in Section 4.3**, Table 5 demonstrates the impact of the choices of the uniformity loss…"(理论→实验兑现)

### EASE(CVPR 2022,33 交界)代表性样本

- Intro P1→P2 [A]:"In contrast to the requirement of big data in deep learning, humans learn new objects from a few examples."
- 3.1 末双簧桥:[D 预告]"In the following section, we present a novel unsupervised discriminant subspace learning…" → 3.2 首 [D 落地]"Below, we present our unsupErvised discriminAnt Subspace lEarning (EASE)."
- 组件块 [C+A]:"**Dissimilarity Matrix.** Although one might design a linear projection based on the similarity relationship alone, we use both…"(标题+块首让步)
- RBF→LRR [E 因果]:"Low-Rank Representation (LRR) [24] expresses each data point xi as a linear combination of other points…"(上段段尾 However 已铺垫,新段零装置)
- [C 回环]:"**Relation to PCA.** By PCA, one seeks projection directions with maximal variances akin to our problem below:"——兑现 #16 段尾预告 "later in the text"。
- 实验消融 [C 并列 ×4]:"**Number of queries in transductive FSL.**"/"**EASE vs. other dimensionality reduction methods.**"/"**Subspace dimension of EASE.**"/"**Inference time.**"

### BiLoRA(CVPR 2025,41 交界)代表性样本

- **段间 A 算子为零**(4 篇唯一):However/Moreover 全部内收到段中句,段间只靠 C 标题+B 回指("this challenge"/"such an interference"/"This approach"/"The above theorem"×2/"These results")。
- Intro P3→P4 [B 递进聚焦]:"Recently, InfLoRA [22] attempted to address **such an interference** by enforcing orthogonality…"
- §4 内 [B 实例化]:"**Building upon the bilinear reformulation**, we show that parameter-efficient finetuning with Discrete Fourier Transform (DFT) [9] naturally fits into our bilinear framework…"
- 定理引渡 [段尾冒号钩,全语料唯一]:"This leads to our main result on the task interference:" → "**Theorem 2 (Task Interference Bound).**"
- 定理→解读 [B ×2]:"The above theorem reveals a fundamental advantage…"/"The above theorem translates our collision probability into the practical guidance…"
- 实验 [C+T 全覆盖]:"**Overall Performance.** Our method achieves state-of-the-art results across all three benchmark datasets (Table 1)." … "**Understanding Capacity Limitations of InfLoRA.** Figure 4 provides a compelling evidence for why previous orthogonal subspace approaches struggle with scaling."(回环打竞品)
- 章内无题分总段 [B]:"These results collectively demonstrate that our frequency-domain approach not only provides theoretical advantages but also translates to practical improvements…"

### 全量统计(158 交界)

| 论文 | A算子 | B回指 | C段头 | D路标 | E冷启动 | F编号 | G词汇链 | H范围状语 | T图表锚 | 合计 |
|---|---|---|---|---|---|---|---|---|---|---|
| SSGC'21 | 8(20%) | 5 | 11(27.5%) | 0 | 5 | (2) | 4 | 4 | 3 | 40 |
| COLES'21 | 5(11%) | 6 | 16(36%) | 4 | 9 | (2) | 4 | 1 | (3) | 44 |
| EASE'22 | 4(12%) | (伴随5) | 15(45%) | 3 | 7 | (1) | 1 | 4 | (0) | 33 |
| BiLoRA'25 | **0** | **10(24%)** | **20(49%)** | 5 | 1 | 3 | 1 | 0 | (6伴随) | 41 |

**五条规律**:

1. **段头制(C)份额随 venue 与年代单调上升**:27.5%→36%→45%→49%。ICLR 单栏长段落靠算子勾连;CVPR 双栏短段落"每段一顶帽子"。BiLoRA 段间算子归零——衔接从"算子外置"演化为"**标题分舱 + 回指粘合**"。
2. **装置分区**:**Intro 从不用 C**(17 交界中 C=1),是算子/回指密度最高区;**Related Work 是纯 C 领地**(11/14);Method 混合区(推导链靠 B 公式回指+E 数学冷启动、组件切换靠 C、竞品对比靠 A);Experiments 靠 C+T+H(CVPR 段头覆盖 >85%,SSGC 无段头就用 H+T 排比)。
3. **段尾预告 vs 段首承接**:约 85% 的衔接负担在下段首句;段尾钩只用于两种场景——**欠账声明**(先用后证:"We will discuss the influence of α and K later."/"later in the text")与**定理引渡**(段尾冒号)。4 篇无一笔坏账(所有欠账后文兑付)。
4. **装置-关系搭配律**:因果拐点(问题→方案)必配显式装置(A/B),4 篇提案句无一例外;**并列是唯一常态化免算子的关系**(E/C/H/T 任选);递进在数学区靠 B、叙述区靠 G;让步后转折永远显式;回环必带坐标(章节号/定理号/专名/复现短语),从不裸回。
5. **三大章段间策略画像**:Intro=论证链(算子驱动,固定完成"背景→转折→因果→分总");Method=推导链+组件舱;Experiments=货架(**协议总分→主战场并列→消融并列/递进→效率或分总收尾**,四篇完全同构)。

各章逻辑骨架(实测序列):
- SSGC Intro:背景封圣→让步后转折→因果(半吊子方案)→并列(竞品链)→因果收束(提案)
- COLES Theory:纲领总分→推导→分总定罪→因果(换 Wasserstein)→递进对偶→并列性质
- EASE Method:路标总分→递进→转折(困境)→双路标交接→组件总分并列→因果→回环(PCA 兑现)→拔高框→组件二
- BiLoRA Method:因果总分(三阶段)→转折(固定基)→因果(双线性)→实例化(DFT)→递进(约束编号)→实例化(算法)→分总→定理链

---

## 任务 2:跨章缝合装置清单

### 2.1 节首 roadmap 句

- **分布律:Method 4/4 必有,理论节 2/2,Experiments 2/4;Intro 与 Related Work 四篇均无 roadmap。**
- SSGC §3(最完整,四句对应四小节):"Below, we firstly outline two claims which underlie the design of our network, with the goal of mitigating oversmoothing. Moreover, we analyze the Markov Diffusion Kernel (Fouss et al., 2012) and note that it acts as a low-pass spectral filter of various degree. Based on the feature mapping function underlying this kernel, we present our Simple Spectral Graph Convolution network and discuss its relation with other models. Finally, we provide the comparison of computational and storage complexity requirements."
- EASE §3(Firstly/Secondly/Thirdly/Finally 四拍,尾句挂图):"…Firstly, we define our model with the classifier in prototypical networks [40]. Secondly, we present how to learn a discriminant subspace given similarity and dissimilarity matrices… Thirdly, we demonstrate how to use the so-called self-representation… Finally, we reformulate the estimation of class centers and the query prediction as a conStraIned wAsserstein MEan Shift clustEring (SIAMESE)… Figure 1 illustrates our method."
- BiLoRA §4(三阶段编号,精确对应小节):"Our solution develops three key stages: (i) We introduce fixed orthogonal bases as a replacement for learned orthogonal projections… Building on this foundation, (ii) we develop a bilinear reformulation that expands the available parameter space from d to d² dimensions… (iii) We then implement this approach using Fourier transforms, which provides both theoretical guarantees for task separation and computational efficiency."
- COLES §4.1(分析纲领 (i)(ii)):"…the key idea of this analysis is to (i) cast the traditional contrastive loss in Eq. (3) … as a GAN framework, and show this corresponds to the use of JS divergence and (ii) cast the objective of COLES in Eq. (4) as a GAN framework, and show it corresponds to the use of a surrogate of Wasserstein distance."
- 词汇差:CVPR 用 "In this section, we…";单栏用 "Below, we…/In what follows, we…"。EASE §4 用表号序列当路标:"…are summarized in Tables 1, 2, 3, 4, 5 and 6 respectively, and discussed in the following sections."

### 2.2 前向指引(三形态)

- (a) 定理/章节号预支:"However, SGC also suffers from oversmoothing as K → ∞, **as shown in Theorem 1**."(SSGC Intro 提前引用 §2 定理);"…which we argue below as suboptimal."(COLES Intro);图注前向:"With the small overlap of distributions, many contrastive methods relying on the JS divergence may underperform **(see Section 4.1 for details)**."(COLES Figure 1 caption)
- (b) 欠账声明(EASE 专用):"We explain how we obtain Asim and Adis latter in the text."(latter 为笔误)/"We will discuss the relation between the dissimilarity matrix and PCA later in the text."——两笔账后文均兑现。
- (c) 段尾 motivates/leads-to 钩(BiLoRA 专用):"This inherent capacity limit motivates our bilinear extension…"/"This leads to our main result on the task interference:"
- 方法-实验最轻量缝线=**方法节括号插表号**:"…the α ∈ [0,1] parameter **(Table 9 evaluates its impact)** to balance…"(SSGC)

### 2.3 回指(分工明确)

- "**the above + 名词化对象**"(objective/analysis/theorem/issues/shortcomings)收编刚结束的推理块;
- "**this/such + 名词**" 近距离粘合(BiLoRA 主力:this challenge/such an interference/This approach/These results);
- **章节号回指只用于跨大章**:结论回收方法("…a method extending the Markov Diffusion Kernel **(Section 3.2)**, whose feature maps emerge from the normalized Laplacian Regularization problem **(Section 3.3)**…",SSGC 结论)与实验回收理论("Following the analysis presented in Section 4.3…",COLES);
- "**aforementioned**" 全语料仅 1 例(SSGC 枢纽交界)——稀缺强标记。

### 2.4 理论-实验短接(三级演化)

- 一级(理论区嵌表号,SSGC):"This is substantiated by Table 8, where S2GC achieves the best results for K = 16, whereas SGC achieves poorer results by comparison, whose peak is at K = 4."
- 二级(实验区回引章节号,COLES):§6.2 整节兑现 §4.3——理论节结尾铺四个均值选项("We investigate the geometric (p = 0), arithmetic (p = 1), harmonic (p = −1) and quadratic (p = 2) means."),实验节按同一顺序验收。**跨过整个 Related Work 的远程伏笔**。
- 三级(制度化,BiLoRA):专设小节(5.2 Empirical Analysis)+ 定理号点名("To verify Theorem 2, we measure the actual interference…")+ 图注复述定理不等式("…validating Theorem 2's prediction that maintaining k ≤ c(d²/T)log(1/δ) ensures bounded interference between tasks.")+ 实验反打理论论断("This empirically validates our theoretical argument about the fundamental limitations of the orthogonal subspace allocation…")。
- 方法→实验方向的另一形态(EASE):方法节框内直接报消融数("Across all datasets, EASE+SIAMESE was consistently better than EASE+Sinkhorn K-means by 0.3–0.4%.")。

### 2.5 主旋律回环(核心主张的多处变奏)

- **SSGC "更大邻域 + 压制 oversmoothing"(6 处)**:摘要→Intro P5→§3 roadmap→Claim II→§4.5→结论。措辞轮换:neighborhoods→receptive fields→contexts;"limiting severe"→"mitigating"→"suffering less from"。骨架不变,近义词轮换。
- **COLES "JS 失效 vs Wasserstein 扛得住"(7 处)**:摘要→Intro P2 种子("which we argue below as suboptimal")→Intro P4→Figure 1 图注→§2.1 桥段→§4.1→结论。**罪名逐级加重:模糊("suboptimal")→数值("log 2 constant and vanishing gradients")→图证→定理化**。9 词核心串 "COLES essentially minimizes a surrogate of Wasserstein distance" 在摘要与结论**逐字复用**。
- **EASE 双旋律**:"block-diagonal prior"(Intro→贡献 i 近逐字→§2→§3.2 claim 句→Figure 1 版面);"minor contribution"(贡献 iii→§3.3 框→结论,**三处逐字复现**,配套动词固定 "extends Sinkhorn K-means")。
- **BiLoRA "InfLoRA 二宗罪"(7 处,最重回环)**:摘要→Intro P4(编号 (1)(2))→§3(符号化 T ≤ ⌊d/r⌋)→§4 P1(数字化 d=1024, r=32, 32 tasks)→§5.1(图表化 Figure 4)→§5.3→结论(再抽象 "the traditional pursuit of perfect orthogonality, while mathematically elegant, becomes increasingly impractical")。**同一素材五种分辨率:编号化→符号化→数字化→图表化→再抽象**。

### 2.6 章间交接(18 处)

- **纯冷切 12 处**:章与章之间不牵手,由每章自己的开门 roadmap 重启坐标(7 例 roadmap 重启)。
- **显式双面交接仅 1 例**(COLES 2→3):章末桥段 "In what follows, we argue that the choice of sigmoid for σ(·) leads to negative consequences…" + 章首 "In what follows, we depart from the above setting…"——两句都以 "In what follows" 开头形成接力棒。
- **软交接三招**:①方法章末偷跑实验证据(SSGC 方法章末引 Table 2 计时 "over 66× slower";EASE 方法框报 0.3–0.4%);②下章首段回声复述上章末段(BiLoRA 3→4:§4 首段将 §3 末段的二宗罪原地复述,"While InfLoRA successfully addresses catastrophic forgetting… our analysis reveals its two significant limitations.");③章内先放无题分总段再切章(BiLoRA 5→6)。

---

## 任务 3:Conclusion 逐句标注

### SSGC(1 段 5 句 145 词;均句长 29.0)

| # | 原句 | 词数 | 功能 | 与上句关系 |
|---|---|---|---|---|
| S1 | "We have proposed Simple Spectral Graph Convolution (S2GC), a method extending the Markov Diffusion Kernel (Section 3.2), whose feature maps emerge from the normalized Laplacian Regularization problem (Section 3.3) if K → ∞." | 33 | 成果重述(现在完成时;双章节号回指) | 开门 |
| S2 | "Our theoretical analysis shows that S2GC obtains the right level of balance during the aggregation of consecutively larger receptive fields." | 20 | 理论重述 | 并列展开 |
| S3 | "We have shown there exists a connection between S2GC and SGC, APPNP and JKN by analyzing spectral properties and implementation of each model." | 23 | 关系重述(现在完成) | 并列展开 |
| S4 | "However, as our Claims I and II show that we have designed a filter with unique properties to capture a cascade of gradually increasing contexts while limiting oversmoothing by giving proportionally larger weights to the closest neighborhoods of each node." | 40 | 机制重述+差异化(However;原句语法残缺——camera-ready 笔误) | 转折反驳(有联系→但我独有) |
| S5 | "We have conducted extensive and rigorous experiments which show that S2GC is competitive frequently outperforming many state-of-the-art methods on unsupervised, semi-supervised and supervised tasks given several popular dataset benchmarks." | 29 | 战绩重述(现在完成) | 并列展开(收束) |

与摘要对齐 3/5(60%):"two theoretical claims"→"Claims I and II";"sequence of increasingly larger neighborhoods"→"cascade of gradually increasing contexts";"trade-off"→"right level of balance"。

### COLES(1 段 6 句 143 词)

| # | 原句 | 词数 | 功能 | 与上句关系 |
|---|---|---|---|---|
| S1 | "We have proposed a new network embedding, COnstrative Laplacian EigenmapS (COLES), which recognizes the importance of negative sample pairs in Laplacian Eignemaps." | 22 | 成果重述("COnstrative"、"Eignemaps" 均原文拼错) | 开门 |
| S2 | "Our COLES works well with many backbones, e.g., COLES with GCN, SGC and S2GC backbones outperforms many unsupervised, contrastive and (semi-)supervised methods." | 22 | 战绩重述 | 递进深化 |
| S3 | "By applying the GAN-inspired analysis, we have shown that SampledNCE with the sigmoid non-linearity yields the JS divergence." | 18 | 理论重述-定罪 | 新对象引入 |
| S4 | "However, COLES uses the RBF non-linearity, which results in the Kantorovich-Rubinstein duality; COLES essentially minimizes a surrogate of Wasserstein distance, which offers a reasonable transportation plan, and helps avoid pitfalls of the JS divergence." | 34 | 理论重述-我方(However;分号双联) | 转折反驳(破立复奏) |
| S5 | "Moreover, COLES takes advantage of the so-called block-contrastive loss whose family is known to perform better than their pair-wise contrastive counterparts." | 21 | 理论重述 2 | 并列展开 |
| S6 | "Cast as the alignment and uniformity losses, COLES enjoys the more robust geometric mean rather than the arithmetic mean (used by SoftMax-Contrastive) as the uniformity loss." | 26 | 理论重述 3 | 并列展开 |

与摘要对齐 4/6(67%),含 9 词逐字串;S6 是摘要没有的新增(结论比摘要多收一条战线)。

### EASE(1 段 7 句 119 词;均句长 17.0,4 篇最短;零现在完成时)

| # | 原句 | 词数 | 功能 | 与上句关系 |
|---|---|---|---|---|
| S1 | "Without meta-learning, we provide state-of-the-art results, outperforming significantly a large number of sophisticated few-shot learning methods." | 16 | 战绩重述+减法开门 | 开门 |
| S2 | "The proposed methods are plug-and-play modules for the inference step of few-shot learning as our transductive inference fits into the code of the standard prototypical network." | 26 | 定位重述 | 递进深化 |
| S3 | "Our solution is simple, efficient and also compatible with semi-supervised approaches." | 11 | 拔高句(三形容词) | 并列展开 |
| S4 | "It consists of two components: unsupErvised discriminAnt Subspace lEarning (EASE) and a minor contribution, conStraIned wAsserstein MEan Shift clustEring (SIAMESE)." | 20 | 成果重述(冒号拆件;"minor contribution" 第三次逐字回环) | 总分 |
| S5 | "Both components can operate independently." | 5 | 机制重述(全文最短句) | 递进深化 |
| S6 | "EASE learns a discriminant subspace to minimize the surrogate problem exploiting the data structure without any label information." | 18 | 机制重述-组件甲 | 并列展开 |
| S7 | "SIAMESE uses the labeled support set with labels and unlabeled queries to estimate the class means more effectively and improve the final prediction." | 23 | 机制重述-组件乙 | 并列展开 |

**结论写成"产品说明书"而非"工作汇报"**(全现在时)。与摘要对齐 4/7。

### BiLoRA(1 段 9 句 202 词,4 篇最长;宣言体)

| # | 原句 | 词数 | 功能 | 与上句关系 |
|---|---|---|---|---|
| S1 | "This work addresses a fundamental question in parameter-efficient continual learning: how to achieve a reliable task separation without the burden of learning orthogonal spaces." | 24 | 问题重述(设问定义贡献) | 开门 |
| S2 | "Our analysis reveals that the traditional pursuit of perfect orthogonality, while mathematically elegant, becomes increasingly impractical as task numbers grow." | 20 | 诊断重述(竞品罪状第 7 次回环) | 因果承接 |
| S3 | "Instead, we demonstrate that "almost orthogonality" through bilinear extension provides a more scalable solution with provable guarantees." | 17 | 成果重述(Instead;标题词加引号回收) | 转折反驳(破→立) |
| S4 | "Our findings have profound implications for both theoretical understanding and practical applications of continual learning." | 15 | 拔高句 | 递进深化 |
| S5 | "The probabilistic analysis reveals that expanding the parameter space can be more effective than enforcing strict constraints, challenging the conventional wisdom in task separation." | 24 | 理论重述+拔高 | 总分 |
| S6 | "This insight, combined with the natural structure of fixed bases such as the Fourier transform, replaces the complex challenge of learning orthogonal spaces with an intuitive frequency allocation scheme." | 29 | 机制重述 | 递进深化 |
| S7 | "Looking forward, this work suggests a paradigm shift from the pursuit of perfect preservation to probabilistic guarantees in continual learning." | 20 | 前瞻/拔高 | 新对象引入 |
| S8 | "This new perspective not only simplifies the implementation of continual learning systems but also provides clearer paths for adaptation to specific domain requirements." | 23 | 前瞻-应用面 | 递进深化 |
| S9 | "While our current focus has been on LoRA-based architectures, the principles of "almost orthogonality" and the bilinear extension could revolutionize how we approach parameter efficiency in deep learning more broadly." | 30 | 范围限定+外推(4 篇唯一 limitation 色彩句) | 让步后转折 |

### Conclusion 汇总

| 指标 | SSGC | COLES | EASE | BiLoRA |
|---|---|---|---|---|
| 段/句/词 | 1/5/145 | 1/6/143 | 1/7/119 | 1/9/202 |
| 现在完成时句数 | 3 | 2 | **0** | 1 |
| limitation | 无 | 无 | 无 | 半句(While 从句) |
| future work | 无 | 无 | 无 | 前瞻 3 句(愿景式非 to-do 式) |
| 与摘要对齐率 | 60% | 67% | 57% | 44% |
| 数字/数据集名 | 0/0 | 0/0 | 0/0 | 0/0 |

**共同律**:(1) 全部单段无小节无编号;(2) **结论零数字零数据集名**——战绩只用比较级与范围词;(3) 开门句三选一:"We have proposed X, …" / 减法状语+"we provide state-of-the-art results" / "This work addresses a fundamental question: …";(4) 结论都执行一次微型**破立转折**(However/Instead),把主旋律的对立结构最后复奏一遍;(5) 无独立 Limitations 节;limitation 至多一个 While 从句并立即外推。**演化线:2021=完成时工作清单;2022=现在时产品说明书;2025=现在时宣言体(问题-范式-前瞻),句数词数最大而战绩句清零。**

---

## 可移植操作规程(六条)

1. **每章自立坐标,不搞章间牵手**:章间 2/3 冷切,靠新章 roadmap 重启;软化三招——方法章末偷跑一枚实验数字、下章首段回声复述上章末段、章内先放无题分总段。
2. **装置分区**:Intro 只用 A/B(算子+回指),Related Work 只用 C(段头)+段尾一次性转折,Method 用 B(公式回指)+E(数学冷启动)+C(组件舱)+A(对比),Experiments 用 C/T/H。
3. **"问题→方案"拐点必须显式化**;"并列"是唯一可裸奔的关系。
4. **欠账要立字据**:先用后证一律写 "as shown in Theorem 1"/"later in the text"/"(Table 9 evaluates its impact)",且全文兑付(4 篇无一笔坏账)。
5. **主旋律至少五处变奏**(摘要→Intro→方法/理论→实验定谳→结论),每次换分辨率:编号化→符号化→数字化→图表化→再抽象;关键短语可整句逐字复用一次。
6. **结论=单段无数字复奏**:重述成果/机制/理论,复奏一次破立转折,句子与摘要半数对齐但全部改写措辞。
