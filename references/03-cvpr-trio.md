# 证据报告 03:EASE (CVPR 2022) + protoLP (CVPR 2023) + BiLoRA (CVPR 2025)

> Hao Zhu 一作的三篇 CVPR 论文。所有引文逐字摘自 PDF。

---

## 论文一:EASE (CVPR 2022)

### 1. 元信息
- 11 页 = 正文 8 页 + 参考文献 3 页(附录另册)。作者 2 人(Zhu + Koniusz 师徒组)。
- 定位:不训练 backbone、只改 transductive 推理阶段的即插即用模块。方法本体极轻(一个 SVD 闭式解 + 一个 Sinkhorn 循环)。
- 代码链接在首页脚注:"*The corresponding author. Code: https://github.com/allenhaozhu/EASE"

### 2. 标题
"EASE: Unsupervised Discriminant Subspace Learning for Transductive Few-Shot Learning"
- 模式:**缩写词 + 冒号 + 完整描述性方法名 + for + 任务名**(CVPR 最保险的命名公式)。
- 缩写构造是**内嵌字母倒造词(backronym)**:"**unsupErvised discriminAnt Subspace lEarning**" 取词内大写 E-A-S-E——先定好词 EASE(暗示"简单/轻松",呼应方法轻量卖点),再反推大写位置。
- 第二个组件同法炮制:"**conStraIned wAsserstein MEan Shift clustEring (SIAMESE)**"。这种大小写**在正文每次正式定义时都原样保留**(出现 3 次以上)——把方法名当广告位。
- 可学之处:两个组件各给一个可发音的名字,让"投影 + 聚类"的两步流水线读起来像两项发明。

### 3. 摘要(8 句,零引用、零数字)
结构:背景(2)→ 相关工作定位(1)→ 方法主体(3)→ 次要组件(2)→ 实验(1)。
- S4 方法总述一个长句同时交代名字、任务、机制、数据来源、时机:"We present an unsupErvised discriminAnt Subspace lEarning (EASE) that improves transductive few-shot learning performance by learning a linear projection onto a subspace built from features of the support set and the unlabeled query set in the test time."
- S5 "which is efficiently solved with SVD" 是摘要里唯一的"理论格调"词,把闭式解当卖点。
- S6 "We also introduce conStraIned wAsserstein MEan Shift clustEring (SIAMESE) which extends Sinkhorn K-means by incorporating labeled support samples."("extends X by incorporating Y" 句式)
- S8 罗列 5 个数据集 + "both steps significantly boost" 暗示消融完备,**不报具体数字**。

### 4. Introduction(4 段 + 贡献列表)
- P1 大成功→大限制教科书开局:"Supervised end-to-end learning has been extremely successful in computer vision, speech, and machine translation tasks..." → "However, with the current learning paradigm, limited data is an obstacle..."
- P2 "人类少样本学习"桥接 + FSL 三分类(metric/meta/transfer)各一句定义——给非 FSL 审稿人 30 秒补课。
- P3 全文最重的一段:立 transductive 赛道 → 通病("However, such methods ignore the potential structure among the data points in the support set and the query set.")→ 核心主张:"In this paper, we argue that features in the inference step can be approximately drawn from a union of multiple subspaces, and thus the sample affinity matrix follows the block-diagonal prior."(**"we argue that" 把一个假设包装成论点**)
- P4 战果预告:性能 + 速度双卖点。
- 贡献列表("Our contributions are as follows:" + 罗马数字 i./ii./iii.):
  - i. **把"假设/先验"本身列为第一贡献**——方法轻量时的经典升格手法。
  - iii. "**As a minor contribution**, we propose ..."——罕见的自降权声明,主动给次要组件定级,防"增量拼盘"质疑(结论里再次出现)。
- CVPR 式特征:无形式化问题定义、无 roadmap 段;贡献列表必备、SOTA 声明前置、引用成簇轰炸。

### 5. Related Work
- §2,四个粗体段首标签分组,由远及近:大领域 → 方法家族 → 本文设定。
- 每段 = 数句中性罗列 + **段尾一次性转折划清界限**。批评从不针对单篇,打包整族:
  - "However, different from GNN-based methods, we do not use a graph or any affinity matrix to propagate labels or features."
  - "Despite PCA and ICA are able to improve the classification performance, they are not designed to act in a discriminant manner via a discriminant criterion step."(针对最近竞品 TAFSSL 的精准一刀:承认有效 → 指出设计缺陷)
  - "Our motivation is different from such methods in that we employ metric learning on the feature space in the test stage (novel classes) to find a discriminant subspace for classification. Moreover, our approach is unsupervised. This makes it work well even in the 1-shot setting."(三连短句收尾,差异点拆成 3 个独立卖点)

### 6. 方法呈现
- §3.1 先**完整复述 ProtoNet 的 Eq.(1)(2)**,然后把自己的方法呈现为对经典公式的一处外科手术:"one can define a linear projection W ∈ RO×O′ (O′ ≪ O) and insert it into Eq. (2)"——**先锚定领域最经典的公式,再最小改动**。三篇共用的呈现骨架。
- **Definition/Proposition/Theorem 数量:0**。理论内容用两个**蓝色圆角底纹框**替代:
  - "**Theoretical Interpretation.** Eq. (6) can be regarded as working with two different loss functions, one preserving the similarity and the other preserving the maximal variance. This is akin to positive and negative sampling strategies in graph node embedding [28,47,56,57]…"——不证明任何东西,只做"视角重述 + 类比挂靠",但排版成框让它看起来像定理。
  - 第二个框 "**SIAMESE vs. Sinkhorn K-means [12].**" 里直接塞实验结果:"Across all datasets, EASE+SIAMESE was consistently better than EASE+Sinkhorn K-means by 0.3–0.4%."——**用彩色框把"与最近亲方法的差异"钉在方法节**,防"这不就是 Sinkhorn K-means 吗"。
- 直觉句样本:
  - "Intuitively, given a K-way N-shot task with B queries for each class, we are targeting an (N + B) × K-way 1-shot problem where off-diagonal entries can be assumed to represent differing entities (on-diagonals represent the same entity)."
  - "For the 5-way 1-shot setting, it is hard to minimize the intra-class distance because only one sample per class is available."
  - "Given an insufficient number of labeled samples per episode, we instead transform the metric learning problem into a graph embedding problem and then use similarity and dissimilarity measures as surrogates for the label information."(**因为 X 不够,我们把 A 问题转化为 B 问题**)
- 闭式解呈现:"The optimal W∗ can be found by selecting top-k (not bottom-k) eigenvectors of ... (the so-called generalised eigenvalue problem)."——一句话给解 + 挂学名抬格调 + 防错细节。
- **"Relation to PCA" 段**:借 PCA 正统性,又为实验里打 TAFSSL 埋钩子。
- 伪代码有(Algorithm 1);交替优化用"发现缺约束 → 升级成 OT 问题"的叙事式推导:"However, Eq. (10) ignores another constraint 1⊤P = 1 which balances the class distribution among K classes [20]. Thus, we reformulate Eq. (10) with the constraint as minimizing the optimal transport distance…"

### 7. 实验
- §4 开头总起段(数据集、协议、"The performance numbers are given as accuracy %, and the 0.95 confidence intervals are reported. The tests are performed on 10,000 random 5-way episodes…")→ §4.1 主表 → §4.2 Ablations(粗体段标题:"Number of queries…"/"EASE vs. other dimensionality reduction methods."/"Subspace dimension of EASE."/"Inference time.")。
- 表格:主表按 backbone 分块,块内先 Inductive 后 Transductive,**自家三个变体压块底标 "(ours)"**;**每列最优用红色标出(含别人赢的格——不藏拙)**;主表同时放三个自家变体行——**SOTA 表兼任组件消融表,一表两用**。
- 推理时间表用科学计数法秒数 + "Our method is about 10× faster (AMD 2700 CPU) than other two SOTA methods."
- 结果句式:
  - "Tables 1, 2 and 3 (mini-ImageNet and tiered-ImageNet) show that EASE (best variant) outperforms all the previous (transductive/inductive) SOTA."
  - "As shown in Table 5, our method is superior to other competitors in all settings by a significant margin (ResNet-12 backbone) e.g., the gain varies between 3% and 6% on mini-ImageNet 1-shot protocol. This can be attributed to improved capturing of the data-manifold structure given extra unlabeled samples."(**声明 → 具体数字区间 → 一句机制归因,三段式**)
  - 失利也解释:"the relatively large number of categories resulted in randomly selected very diverse unlabeled samples which have no positive effect on the support and query sets."
  - 防御性坦白段:"Some recent models such as MCT [19] use data/model perturbation/augmentations and achieve results even better than ours. However, we use the TAFSSL protocol (and thus their features) for the common testbed with other methods." 随后当场给出可比口径下的数字反杀——**把潜在 rebuttal 提前写进正文**。
- 鲁棒性段口头禅 "Our method is insensitive to the feature extractor."

### 8. 图
- 无首页 teaser。**Figure 1 = 框架图**(第 3 页通栏):五阶段横向流水线,底部有阶段名标注条。Caption 完整多句、自足(不看正文能懂)。
- 消融图 caption 短(一句话标题式)、框架图 caption 长——**两档 caption 制**。

### 9. 微观语言风格
- However ×10、Thus ×6、"so-called" ×4、"akin to" ×3、one can/One can ×4、novel ×8。
- **"we"=贡献,"one"=任何人都能做的数学步骤**,划分很稳定。
- 通篇一般现在时(包括实验)。Hedging 低:敢用 "significantly boost"、"by significant margins"、"consistently"。
- 英式/美式混拼(generalised/optimization);非母语痕迹散见("Despite PCA and ICA are able…"、"a few of milliseconds")。

### 10. 模板句库(EASE)
1. "___ (领域缩写) has received a lot of attention due to its remarkable ability to ___" — 摘要第一句。
2. "Although many techniques have been proposed for ___, they mostly focus on ___" — 摘要缺口句。
3. "In this paper, we argue that ___ can be approximately ___, and thus ___ follows the ___ prior" — 把假设升格为论点。
4. "However, such methods ignore the potential ___ among ___" — intro 缺口一击。
5. "In experiments, our model outperforms state-of-the-art methods by significant margins, consistently providing improvements across different settings, datasets, and training models" — intro 战果段(protoLP 近逐字复用,私有模板)。
6. "As a minor contribution, we propose ___ which extends ___ by incorporating ___" — 次要贡献自降权句。
7. "However, different from ___-based methods, we do not use ___ … Our approach is to ___" — related work 划界句对。
8. "Given an insufficient number of ___, we instead transform the ___ problem into a ___ problem and then use ___ as surrogates for ___" — 资源不足 → 问题转化。
9. "The optimal ___ can be found by ___ (the so-called ___ problem)" — 闭式解 + 挂学名。
10. "This can be attributed to ___" / "Our method is insensitive to ___" — 实验讨论件套。

### 11. 卖点包装策略
1. **先验升格为贡献**(block-diagonal prior 当第一贡献)。
2. **双命名策略** + "As a minor contribution" 主动定级。
3. **理论挂靠而非理论证明**:蓝框 "Theoretical Interpretation" 全是"联系"没有定理,但排版制造理论感。
4. **闭式解/无监督/免训练当格调**:"Without meta-learning, we provide state-of-the-art results, outperforming significantly a large number of sophisticated few-shot learning methods."(**"没有 X 也能赢"句式,把'缺机制'反转成'胜过 sophisticated 方法'**)+ "plug-and-play modules"。
5. **速度专表 + 数量级话术**。
6. **预答辩式坦白**(MCT 段)。

---

## 论文二:protoLP (CVPR 2023)

### 1. 元信息
- 14 页 = 正文 8 + 参考文献 3 + 附录 3(附录小节编号接续正文,§6–§11,含 "§9 Note on Fair Comparisons")。
- EASE 的直系续作(EASE 作为 [60] 被引并进消融表)。

### 2. 标题
"Transductive Few-shot Learning with Prototype-based Label Propagation by Iterative Graph Refinement"
- **无缩写、纯描述式长标题,"任务 with 机制 by 手段"三段式**。方法名 protoLP 只在正文定义(camelCase 拼合词)。
- 同一作者两种命名策略并存:**命名随"方法是否有故事性"切换**——protoLP 卖点是"两家族合体",名字由两个家族名拼接即自明。

### 3. 摘要(8 句)
- S3 **缺口句是本篇最强设计**:"The two existing classes of methods, prototype-based and graph-based, have the disadvantages of inaccurate prototype estimation and sub-optimal graph construction with kernel functions, respectively."——**先把全领域二分,再用 "respectively" 一句话给两族各判一罪**。整篇论文(含 Figure 1 teaser)都建立在这个二分法上。
- S4 "In this paper, we propose a novel prototype-based label propagation to solve these issues."(直接回扣两宗罪)
- S6 全摘要最短句,7 词:"As prototypes are being updated, the graph changes."——**故意用短句强调动态图这一差异点**。
- S5/S7 用 "rather than / instead of" 双对比句式。

### 4. Introduction
- P3 **二分 + 判罪 + 图证**:"We categorise transductive FSL into: (i) ..., and (ii) ..." → "However, the above two paradigms have their own drawbacks." → 两个 drawback 分别用 **Fig. 1 (left)/(right) 佐证**。**文字二分法 + teaser 左右分格一一对应**。
- P4 "In order to avoid the above pitfalls of transductive FSL, we propose prototype-based Label-Propagation (protoLP)." + 第二卖点:"Importantly, protoLP does not assume the uniform class distribution prior while significantly outperforming other methods that assume the uniform prior, as shown in ablations on the imbalanced benchmark [46] where methods relying on the balanced class prior fail."(**"Importantly," 开头 + 点名竞品会 fail 的场景**)
- P5 与 EASE P4 近逐字相同(自模板复用铁证)。
- 贡献 i 卖统一框架:"We identify issues resulting from separation of prototype-based and label propagation methods. We propose prototype-based Label Propagation (protoLP) for transductive FSL, which unifies both models into one framework."(**"We identify issues" 把'指出问题'列为贡献的第一动词**);ii 卖去先验:"By introducing parameterized label propagation step, we remove the assumption of uniform class prior while other methods highly depend on this prior."

### 5. Related Work
- 大量句子从 EASE 直接搬运。新批评句:
  - "Additionally, some methods [14, 22, 60] leverage the uniform prior on the class distribution with the optimal transport while in realistic evaluation of transductive FSL the prior is unknown [46]."(**用"realistic evaluation"文献当武器批整个 OT 流派——[60] 就是自己的 EASE,连自己前作一起批,为新作让路**)
  - 划界句:"In contrast to FSL with a fixed graph, we do not construct a graph from samples directly but construct a bipartite graph by prototypes and samples. As prototypes change, so does the constructed graph, which we regard as a learnable graph."(**把迭代更新重命名为"可学习图"——修辞性升格**)

### 6. 方法呈现
- §3.1 Preliminaries **把两大家族的经典公式各复述一遍**(ProtoNet + 经典 LP),为"统一"做铺垫。
- Definition/Theorem:0。理论感靠:闭式解("globally-optimal closed-form formula")、马尔可夫链解读、附录复杂度论证("reduce computational complexity from n3 to c3 where n ≫ c")。
- 直觉句:
  - "Intuitively, we can regard ak as a learnable label for the k-th prototype which is non-sparse in contrast to a one-hot class vector."
  - "One may think of the above process as a 2-hop diffusion on a bipartite graph with samples xi and prototypes ck located in two partitions of that graph. Notice the graph changes with prototypes."(**先给概率链式推导,再补一句"你可以把它想成..."——数学→图像化转译**)
  - 组件必要性一句话:"Using A is not mandatory but this linear projection improves results by limiting overfitting during propagation."
- **交替优化的可读化呈现(最值得抄)**:总纲句 "Below we explain how to optimize w.r.t. Z, A and C by alternating. The order of optimisation in each round assumes minimization w.r.t. Z, then A and finally C." + "**Updating Z.**" / "**Updating A.**" / "**Updating C.**" / "**Inference.**" 四个粗体段,每段 = 子问题目标式 + 闭式解 + 一句稳定性说明。
- **Algorithm 1 与图显式互锁**:算法内四个斜体步骤名与 Fig. 2 四个环节同名,正文点破:"Four steps indicated in italics are also indicated in Fig. 2."——**算法行名 = 框架图板块名 = 小节段名,三位一体**。

### 7. 实验
- 消融升级为**编号小节** §4.2.1–4.2.5 + §4.3——消融是主要卖点载体。
- 新排版元素:自家行**整行淡红底纹**;caption 内嵌协议脚注并交叉引用消融小节:"(∗ : inference aug., §4.2.3)"。
- **卖点表设计**:用 "Sinkhorn ✓/空" 两行对照同一方法,证明 "OT improves performances of EASE by 13% and iLPC by 4.5% … Notice that OT only boost protoLP by 0.7%"——**"别人离了先验掉多少 vs 我只掉 0.7%"的对照表**;unbalanced 表给出 "PT-MAP [14] looses 18% accuracy maximum in the unbalanced setting"。
- 收敛性一笔带过:"Finally, Fig. 3 shows the value of loss in Eq. (11) w.r.t. the iteration number. The loss converges fast."(**不证收敛,只画曲线 + 四词断言**)
- 附录 §9 "Note on Fair Comparisons" **把方法论批评写成社区服务姿态**:"We hope that bringing attention to these evaluation issues will help researchers avoid following the unrealistic settings and move toward fairer evaluation protocols and models."

### 8. 图
- **Figure 1 = 真正的 CVPR 式 teaser**(首页右栏):左右两格漫画分别演示两族方法的失败模式。**teaser 画的是"敌人的问题"而非自己的方法**,与摘要 S3、intro P3、结论四重呼应。
- **Figure 2 = 环形循环框架图**:四个蓝色大箭头的循环,视觉上直接表达"迭代精化"标题词。

### 9. 微观语言风格
- "Notice" 取代 "Note that" 成为口头禅(×4);"w.r.t." ×5;"so-called" 归零——**口头禅随内容类型漂移**。
- 语法瑕疵密度三篇最高:"exceeds in"、"annotations are may be scarce"、"gradient decent"、"looses"、"with under the same testbed"。
- 复用指纹:intro 战果段、"insensitive to the feature extractor"、"plug-and-play module"、协议句、表 caption 与 EASE 逐字同。

### 10. 模板句库(protoLP 新增)
1. "The two existing classes of methods, ___ and ___, have the disadvantages of ___ and ___, respectively" — **摘要级"二分判罪"句,轻方法找定位的最强模板**。
2. "We categorise ___ into: (i) ___, and (ii) ___. However, the above two paradigms have their own drawbacks" — intro 版二分 + 转折。
3. "In order to avoid the above pitfalls of ___, we propose ___" — 缺口→方法过渡。
4. "Importantly, ___ does not assume the ___ prior while significantly outperforming other methods that assume ___, as shown in ablations on ___ where methods relying on ___ fail" — "少一个假设"卖点句。
5. "We identify issues resulting from separation of ___ and ___ methods. We propose ___, which unifies both models into one framework" — 统一框架贡献句。
6. "As ___ change(s), so does ___, which we regard as a learnable ___" — 把迭代过程重命名为"可学习对象"。
7. "One may think of the above process as a ___ on a ___" — 推导后的图像化转译。
8. "Using ___ is not mandatory but this ___ improves results by limiting ___" — 可选组件辩护。
9. "Below we explain how to optimize w.r.t. ___, ___ and ___ by alternating..." + "Updating ___." — 交替优化骨架。
10. "We hope that bringing attention to these evaluation issues will help researchers … We encourage the community to compare different methods under the same testbed" — 附录社区喊话。

### 11. 卖点包装策略
1. **"统一者"叙事**:"Our protoLP inherits advantages of individual prototype refinement and label propagation steps while avoiding the disadvantages of the bias in estimation of prototypes and the fixed graph bias."(inherits...while avoiding 对仗)
2. **假设消除当第二贡献** + 选择性引入对自己有利的评测坐标系(unbalanced),展示竞品崩盘(−18%)而自己稳。**方法增量有限时,换评测坐标系是高杠杆包装**。
3. **理论性质轻量化**:收敛只给曲线、最优性只到子问题闭式解、复杂度放附录——**每样理论都点到为止,但每样都有**。
4. **连环消融矩阵化**:把 EASE、iLPC、LP、PT-MAP 全拉进 ✓/✗ 对照,顺手完成"protoLP > EASE"的代际宣告。

---

## 论文三:BiLoRA (CVPR 2025)

### 1. 元信息
- 10 页 = 正文 8 + 致谢参考文献 2。**无附录,两条定理均未给证明**(全文无 "Proof" 字样)。
- 作者 4 人跨机构(Zhu、Yifei Zhang、Junhao Dong、Koniusz),Equal contribution 脚注——从师徒二人组变为四人组。
- 领域切换到 continual learning;方法 = 固定 DFT 基 + 频域稀疏掩码的 LoRA 变体。

### 2. 标题
"BiLoRA: Almost-orthogonal Parameter Spaces for Continual Learning"
- 缩写构造:**portmanteau 拼合**(Bi(linear) + LoRA)——2024–25 年 LoRA 生态标准命名法,搭便车心智。
- **标题第二段放的不是机制而是理论性质**("Almost-orthogonal")——把论文的概念货币直接写进标题。

### 3. 摘要(9 句)
- S4 **摘要里直接点名唯一靶子 InfLoRA**(前两篇摘要从不点名竞品)。
- S6 "Our key insight is that by expanding the parameter space quadratically through two fixed bases, we can achieve "almost orthogonal" task subspaces probabilistically, eliminating the need for explicit interference elimination procedures."(**"Our key insight is that…" 模板 + 尾部现在分词从句**)
- S7 **摘要里直接写大 O 速率对比**:"We provide theoretical guarantees that this approach reduces the probability of task interference from O((k/d)²) to O((k/d²)²), ensuring reliable task separation without complex optimization."
- S8 动词是 "validate our theoretical bounds"——**实验的第一职能被写成验证理论,SOTA 排第二**。
- S9 代码句进摘要正文(2025 惯例)。

### 4. Introduction(6 段 + 贡献 i–iv)
- **P4 靶子段是结构核心**:"Recently, InfLoRA [22] attempted to address such an interference by enforcing orthogonality between task-specific matrices. While this approach provides task separation guarantees, it faces two critical limitations: (1) The number of tasks is strictly bounded by the dimensionality of the parameter space - with model dimension d and rank r, only ⌊d/r⌋ tasks can be supported. (2) Early tasks may claim key parameter subspaces, leaving later tasks with potentially suboptimal allocations…"——**给竞品缺陷编号 (1)(2),此后被逐字级重述至少三次**。重复锤打是刻意策略。
- 贡献扩为四条,**配额固定为方法→理论→实现→实验四件套**,条目 ii 内嵌套 (1)(2) 并写入速率——贡献条目本身携带定量对比。

### 5. Related Work
- 批评句式升级为**"承认→判罪→自比"三连,每族一击**:
  - "While effective, these approaches increase model complexity and cannot maintain task separation."
  - "Input-based methods such as Prompt-tuning [21] and VPT [17] modify input representations via learnable tokens but their expressive power is limited to manipulating the input space."
  - 段尾自比:"Our frequency-domain approach differs fundamentally by providing inherent task separation through orthogonal basis functions, avoiding the computational overhead of gradient projection while maintaining mathematical elegance."

### 6. 方法呈现
- **"把竞品公式当预备知识复述"**:§3 Preliminaries 复述 LoRA Eq.(1) → CL-with-LoRA Eq.(2) → "Existing Solution." 段复述 InfLoRA 的 Eq.(3)。
- **Theorem ×2,均带命名**——"Theorem 1 (Frequency Separation)"、"Theorem 2 (Task Interference Bound)",无证明、无附录指针。作用是**可引用的锚点**:实验节反复回扣("To verify Theorem 2, we measure the actual interference…")。
- **推导可读化**:内积展开链每步在行尾括号给理由("(UTU = I)"、"(by Cauchy-Schwarz)")——**证明步骤注释内联化**。随后总结分工:"This shows how all three conditions work together to maintain task independence: orthonormal U preserves output separation, orthonormal V preserves input transformation, and orthogonal B matrices ensure task parameter separation."(冒号 + 三平行短句)
- **定理后必接"翻译段"**(本篇最鲜明的技术):
  - Theorem 1 后:"Consider a practical example with model dimension d = 1024 and k = 32 components per task: the probability of perfect separation is at least 99.9%. This is analogous to randomly placing k items in a d × d grid versus a 1D array of size d…"——**具体数字实例 + 生活化类比**。
  - Theorem 2 后:"The bound in Eq. (16) tells us exactly how many frequency components we can allocate per task while keeping interference under control. This enables us to realize a budget – as one adds more tasks (T increases), one needs to be more conservative with the per-task allocations (k decreases). The log(1/δ) term provides a safety margin…"——**把界读成"预算"隐喻,逐项解释每个符号的工程含义**。
- 两策略平行呈现(Without/With replacement 两个 bullet)——**确定性保证与概率保证并列成菜单**,后文消融一一对应。

### 7. 实验
- **§5.2 Empirical Analysis(理论验证专节)**是新结构:模拟实验对齐定理曲线("The experimental results closely match our theoretical predictions, with the interference growing quadratically with the sampling rate.")。
- Table 1 表头 "Last (↑)/Avg. (↑)" 箭头;**Joint Training(上界)与 Sequential(下界)两行夹住所有方法**——"三明治"设计让 "approaches the joint training performance" 有视觉支撑。
- 结果句式:"On ImageNet-R, we achieve 77.95% final accuracy and 81.52% average accuracy, outperforming previous best results by 2.3%."(声明→数字→差值);贴上界话术:"where our method approaches the joint training performance (91.92%) with 87.46% final accuracy"。
- **反向消融竞品**:"Figure 4 provides a compelling evidence for why previous orthogonal subspace approaches struggle with scaling. … This empirically validates our theoretical argument about the fundamental limitations of the orthogonal subspace allocation…"——**专门做实验证明"敌人的缺陷"(把 InfLoRA 的 r 扫一遍看它崩),动机实验化的高级打法**。
- 消融疑问句标题首次出现:"How Many Frequency Components Are Needed?";千分号记忆点:"our method achieves the optimal performance using only 3.2‰ of the available frequency components."

### 8. 图
- Figure 1 概念对比图(Naive LoRA / InfLoRA / Bilinear LoRA 三联),caption 三句对仗、递进到自己。但**浮到了第 4 页**(intro 第 5 段就引用)——概念上是 teaser,版面上失位,引以为戒。
- Figure 3 **理论-实验对齐图**,caption 直接写定理编号:"validating Theorem 2's prediction that maintaining k ≤ c(d²/T) log(1/δ) ensures bounded interference between tasks."
- Figure 5 热图阵列,caption 教读者怎么读图。

### 9. 微观语言风格(三篇词频对比)

| 特征 | EASE'22 | protoLP'23 | BiLoRA'25 |
|---|---|---|---|
| so-called | 4 | 0 | 1 |
| Notice / Note that | 2 | 4 | **0** |
| akin to | 3 | 0 | **0** |
| w.r.t. | 1 | 5 | **0** |
| However | 10 | 4 | 6 |
| fundamental | 0 | 0 | **10** |
| significant* | 4 | 4 | **11** |
| key insight | 0 | 0 | 2 |

- **LLM 时代语域特征密集**(2025):"delicate balance"、"fundamentally reimagines"、"mathematical elegance"、"best of both worlds"、"profound implications"、"challenging the conventional wisdom"、"paradigm shift"、"could revolutionize";尾部现在分词从句(", eliminating…/", ensuring…" 合计 10+ 次)与"冒号 + 三平行短语"高频。
- 旧 ESL 语法瑕疵基本消失,但仍有笔误(Euqal/Overlaping)——**"AI 润色 + 人工表格"的工序分离**。
- 结论段修辞通胀达到峰值(连用三个拔高句)——**慎学**。

### 10. 模板句库(BiLoRA)
1. "___ requires models to ___ while maintaining a delicate balance between ___ (___) and ___ (___)" — 双括号定义式开场。
2. "However, existing ___ methods such as ___ face fundamental limitations, i.e., they rely on ___ which is increasingly difficult as ___" — 摘要点名缺口句。
3. "Our key insight is that while ___ becomes increasingly difficult with ___, we can achieve ___ with high probability by ___" — 洞见句。
4. "We provide theoretical guarantees that this approach reduces ___ from O(___) to O(___), ensuring ___ without ___" — 摘要理论声明。
5. "While this approach provides ___, it faces two critical limitations: (1) ___. (2) ___" — 竞品缺陷编号句(可反复重述)。
6. "This shows how all three conditions work together to ___: ___ preserves ___, ___ preserves ___, and ___ ensure(s) ___" — 推导后分工总结。
7. "Consider a practical example with ___ = ___ and ___ = ___: ___ is at least ___%. This is analogous to ___ versus ___" — 定理翻译段(实例+类比)。
8. "This enables us to realize a budget – as one adds more ___ (___ increases), one needs to be more conservative with ___ (___ decreases)" — 界的工程化解读。
9. "___ offers the best of both worlds, i.e., ___ and ___ – making it the preferred choice for practical applications" — 消融结论。
10. "Figure ___ provides a compelling evidence for why previous ___ approaches struggle with ___ … This empirically validates our theoretical argument about ___" — "实验证明敌人缺陷"句对。

### 11. 卖点包装策略
1. **把"放弃保证"卖成洞见**:不追求严格正交,改卖概率意义的 "almost orthogonal";结论宣布颠覆常识:"expanding the parameter space can be more effective than enforcing strict constraints, challenging the conventional wisdom in task separation."
2. **理论装配线**:命名定理(无证明)→ 摘要写速率 → 定理后接实例/类比/预算隐喻 → 理论验证专节模拟曲线 → caption 回引定理。**理论是叙事骨架而非数学负担**——两页纸完成"有理论保证的方法"的全部观感。
3. **单靶策略**:全文动机压在 InfLoRA 一家,两条编号缺陷重复三遍,Figure 4 钉死靶子。
4. 效率新说法:"constant memory footprint"、"3.2‰"(千分号)、"unlimited tasks"。
5. **上下界夹逼表**。

---

## 跨三篇总结

### 共同写作指纹
1. **Intro 恒定模板**:宏观成功叙事 → 数据/标注限制 → 立赛道 → However 判罪 → we propose → 性能+速度战果段 → "Our contributions are as follows:" + 罗马数字,**末条永远是实验贡献**。战果段逐字复用。
2. **"复述经典公式 → 外科手术式修改"的方法开场**:新方法永远被呈现为对领域最著名公式的最小编辑。
3. **段落级粗体标签驱动**;算法框必有且与图/正文步骤名互锁。
4. **每个公式配一句直觉转译**(Intuitively / One may think of ___ as / can be regarded as);理论一律"点到为止":闭式解 + 复杂度一句 + (2025 起)无证明定理,从不写完整证明。
5. **表格文化**:主表按 backbone 分块、(ours) 多变体压底、± 不确定度、最优标色(诚实标出别人赢的格)、SOTA 表兼任消融表、必有推理时间表。
6. **固定卖点三件套**:(a) 免训练/即插即用;(b) 对 backbone 鲁棒;(c) **少一个假设/少一道程序**(EASE: unsupervised;protoLP: no uniform prior;BiLoRA: no explicit orthogonalization)——**三篇的 novelty 论证核心都是"减法当加法卖"**。
7. **预答辩写作**:主动坦白不利比较并给可比口径、附录"公平比较"宣言、给次要贡献自降权。
8. 微观:低 hedging、强副词、"we"=贡献 vs "one"=数学、图 caption 两档制。

### 2022 → 2025 演化
1. Teaser:无 → 首页"敌人失败模式"漫画 + 次页框架环图(最标准 CVPR 配置)→ 概念三联对比图(但浮到第 4 页)。
2. **理论呈现三级跳**:彩色底纹伪定理框 → 附录复杂度论证 + "loss converges fast" → 命名定理×2 + 摘要写大 O + 理论验证专节 + caption 引定理。**理论含量没实质增长(始终无证明),但理论的"叙事地位"从装饰升为主线**。
3. 树敌方式:批整族 → 二分判罪 + 换评测坐标系 → 单点锁定命名竞品、缺陷编号、重复三遍、专设实验。
4. **语言的 LLM 断层**:2022/23 满是 ESL 指纹与个人口头禅;2025 几乎清零,换成高浓度 LLM 语域,代价是同义重复与修辞通胀。
5. 规范演化:代码链接从脚注进摘要;协议从 10,000 episodes + CI 换成 5 seeds + Last/Avg(↑);表头出现箭头、上下界夹逼行。
6. **不变的内核**:三篇方法都是"一页纸能写完"的轻方法,论文都成立于同一公式——**轻机制 + 强先验故事 + 减法卖点 + 全覆盖实验矩阵 + 效率专表**。
