# 证据报告 04:COSTA (KDD 2022) + SFA (AAAI 2023)

> Yifei Zhang(学生)一作、Hao Zhu 二作指导的两篇高引论文——代表 Hao Zhu 指导学生论文时的团队写作模式。引文逐字摘自 arXiv 版。

---

## 第一部分:COSTA (KDD 2022)

### 1.1 元信息
- 18 页 = 正文 11 页 + 参考文献 3 页 + 附录 4 页(A 三个引理的证明 / B 稀疏随机投影加速 / C 数据集统计)。
- 定位:**"诊断—修复"型方法论文**。先制造一个可量化的病(graph augmentation 的 bias),再用一行代码的操作(随机投影)治病,理论(matrix sketching 误差界)负责给这一行代码正名。

### 1.2 标题
"COSTA: Covariance-Preserving Feature Augmentation for Graph Contrastive Learning"
- **"先选好词、再回填短语"的强造背首字母缩写(backronym)**:COSTA 是可发音真词,四字母从短语的非首字母位置强行提取("**CO**variance-pre**S**erving fea**T**ure space **A**ugmentation")。正文用混合大小写反复展示提取路径。
- 标题公式:`缩写名: 核心性质形容词-ing + 操作对象 + for + 应用领域`。"Covariance-Preserving" 把唯一的理论卖点直接抬进标题——**标题本身就是定理的广告**。

### 1.3 摘要逐句(7 句)
| 句 | 关键词 | 功能 |
|---|---|---|
| S1 | "improves ... leading to SOTA" | 领域定调 |
| S2 | "The graph augmentation step is **a vital but scarcely studied step** of GCL." | **缺口公式:"重要但少有人研究"——两个形容词一正一负制造张力** |
| S3 | "we show that ... is highly biased, somewhat limiting" | **先卖诊断再卖药**:第一贡献是负面发现;"somewhat limiting" hedging 降半格 |
| S4 | "Thus, instead of ... we alternatively propose" | 转向句 |
| S5 | "Inspired by so-called matrix sketching, we propose COSTA, a novel COvariance-preServing feaTure space Augmentation framework for GCL, which generates augmented features by maintaining a "good sketch" of original features." | **招牌提案句:`Inspired by 理论 + we propose 名字 + a novel 展开式 + which 机制`,一句完成理论背书+命名+机制** |
| S6 | "To highlight the superiority ... single-view setting ... conserves memory and computations" | 副贡献 + 效率卖点捆绑 |
| S7 | "achieves comparable/better results" | 结果句,零数字,斜杠对冲 |

特征:无任何数字、无数据集名;负面发现先于方法;效率必占一句。

### 1.4 Introduction
- P1 漏斗:GNN 需要标签 → SSL 免标签 → CL 追平监督 → GCL → 依赖手工增强 → 引最新文献埋雷 → 段末**修辞问句收口**:"Such observations naturally raise the question: are there better augmentation strategies for GCL other than GA?"(KDD 式悬念钩子)
- P2 **intro 里放数学**:第二段直接写出 WLLN 的极限式,现场引用 Figure 1a/1b——**第一页读完,读者已经看过"证据"**。
- P3 "We assert that ..."(全文最强立场动词)一句话塞三组斜杠反义对。
- P4 粗体 "Our Contributions." 段,近乎逐句复述摘要。
- 贡献列表三条,槽位:**i=诊断(point out the issue)、ii=方法(simple and effective + 命名)、iii=附加设定(效率)**。
- 列表后**窄域 first 声明**:"To our best knowledge, this is the first work which considers feature augmentation (in the single-view setting) in GCL with the matrix sketching step performing feature augmentation."——"first" 被三层限定词包住,**缩到不可证伪的窄域**。

### 1.5 Related Work
- §2,两级小节按"轴"切分,每段"领域巡礼 + 段末一句划清界限"。
- 批评句式:
  - "The above multi-view methods suffer from the large memory and computational footprint, respectively."
  - "Although COLES [46] proposes a robust single-view GCL approach, it works the best with linear GNNs such as S2GC [45]."(**自引后自我设限,顺手把师门前作织进叙事**)
  - "However, no prior work has combined FA with contrastive learning in the graph domain the way COSTA performs FA."(排他句自带限定从句)

### 1.6 方法呈现
- Notation:§3.1 独立小节约 20 行,全量铺陈(其中一半后文根本不用)——**notation 段本身就是"理论纪律"的着装**。
- 理论构件:**1 Definition(引 KDD 血统的 Liberty 定义——选品精准)+ 3 Lemma + 3 Remark**;附录 1 个引入的 Theorem。**自己的结果全部只叫 Lemma**——标签经济学:标准结论的改述用小标签,避免被攻击理论新颖性。
- **固定三拍节奏:Lemma(界)→ "Proof. See Appendix A."(一行放逐)→ Remark(白话翻译 + 顺手处决一个变体)**:
  > "Remark 4.3. The upper bound of ‖X⊤X − X̃⊤X̃‖₂ is controlled by the (k + 1)-th largest eigenvalue σk+1. Usually, σk+1/σmax is small as σk+1 ≪ σmax even when k is small. However, SVD is computationally intensive and unsuitable for decomposition of large feature matrices."
  三个 Remark 连成比较阶梯,终点 Remark 4.7 **理论提前替实验里的赢家背书**。
- 每个 display 公式后必跟一句工程语言("Note that computing Eq. (3) is both memory costly and time consuming as it requires ...")。
- **版式武器:淡青色圆角高亮框**。一框住 "Bias(T_GA(x)) ≫ Bias(T_FA(x))"——**一句定性口号被排成不等式并加框,把观察升格为"结论物"**;二框住方法定义 Eq.(6)。

### 1.7 实验
- **KDD 惯例 RQ 结构满配**:开门列 RQ1–RQ4,小节标题带 RQ 编号。**RQ1 不是方法实验,而是把 motivation 定量化**——第一组"实验结果"验证论文的前提(hypothesize 语式)。
- 表格:主表按方法族分组 + Training Data 列(X / A / X,A)标示信息公平性 + 自家两行浅青底纹。
- 结果句式:
  - "Tables 2 and 3 show that COSTA achieves competitive performance compared to the baseline methods, and even surpasses them on most datasets. These results demonstrate that COSTA is an effective framework leveraging the advantage of feature augmentations."(**`Table N shows that ... These results demonstrate that ...` 双句起手:先陈述再升华**)
  - **输局解释术**:"We note that datasets on which COSTASV does not achieve SOTA have a small number of nodes with low node degrees (i.e., only around 10% of nodes in Amazon-photo and Coauthor-Physics have the degree less than 3, meaning less bias is introduced by the topology GA."——**输的地方用自己的 bias 理论反向自洽("输恰恰因为那里没病可治"),再补效率安慰**。
  - **"惊讶—解释"两段式**:"It is somewhat surprising that although the random projection is not the optimal solution to Eq. (6), it still outperforms the SVD-based sketching. Such a good performance comes from the following facts: (i) ...; and (ii) ..."——主动暴露反直觉点,编号事后解释,把随机性重述为 regularization。
- 收尾句 "as expected" 盖章:"Notably, removing the random projection completely from training decreases the accuracy on three datasets, as expected."

### 1.8 图
- Figure 1 = **首页证据图**(散点+KDE),caption 直接下判词("(a) FA is unbiased. (b) GA is biased.")且自带实验配置。
- Figure 2 = 概念漫画(反例:有偏增强如何毁掉对比学习)。
- Figure 3 = **管线图,新模块黄色高亮、其余灰调**——架构图里给"增量"打高光,一眼看出论文只动了哪一块。
- 小图 caption 即结论:"Figure 4: The bias vs. the node degree." "Figure 5: Node degrees obey the power law distribution."

### 1.9 微观语言
- 连接词:Thus / To this end / However / Moreover / Specifically / In contrast;段落起手大量 "Below,"。
- **斜杠反义对(最强指纹)**:comparable/better、similarity/dissimilarity、grouping/separating、related/unrelated、accuracy/speed,连小节标题都用斜杠。
- "so-called" 驯化术语;"Note that"(≥6);"We note that"(结果讨论标配);"i.e.," 侵占 "e.g.," 职能。
- Hedging:"somewhat limiting"、"may result in";断言处用力:"Clearly,"、"We assert that"。
- 结论段现在完成时:"We have quantitatively and qualitatively analyzed ... we have shown ... we have proposed ..."
- 校对松散:"tasks.Thus"、"CitSeer"、"we use use"、"matirx"。

### 1.10 模板句库(COSTA)
1. 缺口句:"The ___ step is a vital but scarcely studied step of ___."
2. 提案句:"Inspired by ___, we propose NAME, a novel ___ framework for ___, which generates ___ by maintaining a "___" of ___."
3. 问句转轴:"Such observations naturally raise the question: are there better ___ other than ___?"
4. 诊断预告:"To this end, we show that ___ obtained with ___ are highly biased compared to ___, that is, ___."
5. 窄域 first:"To our best knowledge, this is the first work which considers ___ (in the ___ setting) in ___ with ___."
6. Remark 三连:"The upper bound of ___ is controlled by ___. Usually, ___ is small as ___. However, ___ is computationally intensive and unsuitable for ___."
7. 主结果起手:"Tables X and Y show that NAME achieves competitive performance compared to the baseline methods, and even surpasses them on most datasets. These results demonstrate that ___."
8. 输局解释:"We note that datasets on which NAME does not achieve SOTA have ___ (i.e., only around N% of ___), meaning ___. However, NAME requires less runtime and memory to achieve the comparable performance."
9. 惊讶—解释:"It is somewhat surprising that although ___ is not the optimal solution to ___, it still outperforms ___. Such a good performance comes from the following facts: (i) ___; and (ii) ___."
10. 结论骨架:"We have quantitatively and qualitatively analyzed the problems stemming from ___, and we have shown that such a strategy suffers from ___. To overcome this ___, we have proposed ___."

### 1.11 "一行代码 + 理论"包装五层
方法实体:X̃ = (1/√k)PX(给隐层特征乘一个随机高斯矩阵)。
1. **性质命名进标题**:JL 谱系的教科书事实被命名为 "Covariance-Preserving" 抬进标题——"副产品性质"变成"设计原则"。
2. **框架化**:一行代码升维成带约束通式的特例;前人的 Gaussian noise injection 被收编为 "One special case of COSTA"——**让竞品变成自己框架的退化点**。
3. **三选一的定理阶梯**:全是标准结果的转述,真实功能是构成"理论上随机投影应当最好"的推理链,**让实验赢家显得是被推导出来的**。
4. **病理学造势**:自定义 Bias 度量 + WLLN 话语 + 幂律度分布联动——**方法的价值由病的严重度定价**。
5. **口号排版成数学**:定性判断排成编号公式并加框,获得定理般的视觉权重。

---

## 第二部分:SFA (AAAI 2023)

### 2.1 元信息
- AAAI 双栏:主文 9 页 + 补充材料 7 页。
- **首页脚注公开分工**:"*Corresponding author. PK was primarily concerned with the theoretical analysis (e.g., Prop. 2 & 3)."——**理解团队生产模式的钥匙:学生搭系统跑实验,资深理论作者负责"抬格调"的数学**。
- COSTA 的直接续作(related work 明写 "We outperform feature augmentations such as COSTA")。

### 2.2 标题
"Spectral Feature Augmentation for Graph Contrastive Learning and Beyond"
- 平实三词法名 + 缩写 SFA;**"and Beyond" 后缀三重作用**:(1) 预告跨域实验(图+图像);(2) 适配 AAAI 综合 venue;(3) 给"通用算子"承诺。摘要第一句就埋伏笔("(e.g., perturbation of graph edges, image crops)")。

### 2.3 摘要要点(8 句)
- S1 让步开场 + **三形容词缺口公式**("another plausible, complementary yet not well researched strategy")。
- S2 **"argumentation" 是 "augmentation" 的错拼,错在摘要第二句**——校对松散的极致样本。
- S4 **算子命名句**:"This is achieved by the proposed herein incomplete power iteration, a non-standard power iteration regime which enjoys two valuable byproducts (under mere one or two iterations): (i) it partially balances spectrum of the feature map, and (ii) it injects the noise into rebalanced singular values of the feature map (spectral augmentation)."——**把"没跑够的幂迭代"重命名为一个"regime",缺陷即特性**。
- S6/S7 理论两句("We derive the analytical form for: (i)...(ii)..." + "We also show that the spectral augmentation improves the generalization bound."——后者实为引用他人定理,摘要不注明)。
- S8 **插件式三连声明**:更强 / 可叠加 / 兼容各损失("outperforms baselines, and is complementary with other augmentation strategies and compatible with various contrastive losses")。

### 2.4 Introduction
- P2 转轴:"The above issue motivates us to propose a simple/efficient data augmentation model which is complementary with existing augmentation strategies. We target Feature Augmentation (FA) as scarcely any FA works exist in the context of CL and GCL."
- 设计选择辩护句:"Hence, we opt for injecting random noise into the singular values of feature maps as such a spectral feature augmentation does not alter the orthogonal bases of feature maps by much, thus helping preserve semantics correlations."(**选择+理由+软化词+收益,一句完成**)
- P3 "In other words" 重述术:同一论点先术语版后白话版各说一遍。
- 贡献四条(方法/算子/理论/变体);**iv 公然把消融基线写成贡献**:"For completeness, we devise other spectral augmentation models, based on the so-called MaxExp and Power Norm. operators and Grassman feature maps, whose rebalancing and noise injection profiles differ with our method."——**为打败而造的对照组升格为"我们还顺手设计了一族算子",消融变分类学**(且工具来自 Koniusz 自己的 TPAMI 工作——自家工具箱二次变现)。

### 2.5 Related Work
- 批评句式:"Popular random data augmentations are just one strategy to construct views, and their noise may affect adversely downstream tasks. Thus, some works learn graph augmentations but they require supervision."(先降格为"只是其中一种",再点死"要监督")
- 段末:"In contrast, we study spectral feature augmentations to perturb/rebalance singular values of both views. We outperform feature augmentations such as COSTA [Zhang et al. 2022c]."(**直接点名超越自己的前作——续集式自我对标**)

### 2.6 方法呈现
- Notation 整体挪进补充材料,且与 COSTA §3.1 近乎逐字相同(**同一模板文件复用的铁证**)。
- 理论构件:正文 Propositions 1/2/3 + Theorem 1(引用他人)。**标签经济学与 COSTA 相反而互补:自己的新分析用 Proposition(匹配原创性),Theorem 只留给引进的结果**("To show SFA achieves the improved generalization bound we quote the following theorem"——"we quote" 用词坦白)。
- **青色圆角框成为"翻译层"**:Prop 2 给出含超几何函数的解析期望后,紧邻青框用编号白话拆解("Note on Spectrum Rebalancing. Fig. 3 explains the consequences of Prop. 2 & 3 and connects them with Alg. 1. Notice following: (i) ... (ii) The injected variance is clearly visible in that flattened range (we know the quantity of injected noise). (iii) The analytical and simulated variances match.")。
- 另一青框**用理论钦定超参数**:"Choice of Number of Iterations (k). ... The best rebalancing effect is achieved for k = 1. ... Thus, in all experiments (including image classification), we set k = 1"——**把调参决定写成解析推论,审稿人无法再问"k 怎么选"**。
- **小节标题设问**:"3.2 Why does the Incomplete Power Iteration work?"——把审稿人必问的问题做成标题自问自答。
- **"SVD 透镜"**:把 InfoNCE 的 alignment 项用 SVD 展开(Eq.5 病)再写出加 SFA 后的版本(Eq.6 药),青框总结——**公式 A(病)与公式 A′(药)的最小对照对,是全文论证的枢轴**。
- 证明编号分步("Step 1. ... Step 4."),且坦率:"...is simply obtained by the integration using the Mathematica software..."——**格调来自结果形态(闭式解),不来自推导的手工艺**。

### 2.7 实验
- 无 RQ(AAAI 不吃这套),改**4.1 Main Results + 4.2 Analysis 两段式;4.2 的每一小段对应一个理论命题的实证回执**——理论—实验闭环是本篇骨架。
- **插件式行交错**设计(SimCLR / SFA_SimCLR、BarlowTw / SFA_BT 逐对排布)——**表格版式本身就在演示"即插即用"**。
- **教学式 caption**:"Table 1: Node classification on graph datasets. Note that SFAInfoNEC and SFABT can be directly compared to GRACE and G-BT."——**caption 直接指挥读者比哪两行,预防"比较不公平"质疑**。
- **羞辱式效率表**:"Table 3: Running time on Ogb-arxiv." 内容仅一行——SFA 0.25 hour / SVD 12 hours / Random SVD 1.2 hours。
- **数字连祷文**句式:"AG yields 2.2%, 2.2% and 3.2% gain on Am-Computer, Cora, and CiteSeer. AF∗ yields 1.7%, 4.1% and 1.8% gain on ... Importantly, when both AG and AF∗ are applied, the gain is 3.7%, 6.0% and 4.8% ... Thus, SFA is complementary to existing graph augmentations."
- 判负解释仍回扣自家理论:"As Grassman binarizes spectrum, it may reject some useful signal at the boundary between leading and non-leading singular values."

### 2.8 图
- Figure 1 = **首页机制漫画**(四联椭圆,与摘要并排;caption 90 词自带完整论证链)——**长 caption 承担推理(不是"看图说明",是"看图论证")**。
- Figure 2a 管线图与 COSTA 同模板同画风(灰调管线 + 新模块黄色高亮)。
- Figure 3 = **理论—仿真对照图**,caption 收尾 "Note theoretical φ in Prop. 2 and real φ′ from Alg. 1 match."——**"解析与仿真吻合"作为可信度仪式**。

### 2.9 微观语言
- **"so-called" 爆表**(10+ 次)。
- **Koniusz 腔书面倒装/雅词**:"the proposed herein"、"enjoys"、"regime"、"push-forward function"。**理论段与实验段的语域明显分裂——可按语域切片辨认执笔人**。
- 斜杠对延续:"simple/efficient"、"perturb/rebalance"、"graph/image datasets"。
- 校对更松(摘要 "argumentation"、图 1 "Spetral"、引文 GCA/GRACE 互换、坏 bib 条目)。

### 2.10 模板句库(SFA)
1. 让步缺口开场:"Although ___ boost the efficiency of ___, ___ is another plausible, complementary yet not well researched strategy."
2. 算子命名:"This is achieved by the proposed herein ___, a non-standard ___ regime which enjoys two valuable byproducts (under mere ___): (i) ___, and (ii) ___."
3. 动机转轴:"The above issue motivates us to propose a simple/efficient ___ which is complementary with existing ___."
4. 设计选择辩护:"Hence, we opt for ___ as such a ___ does not alter ___ by much, thus helping preserve ___."
5. 白话重述:"In other words, the ___ leads to a suboptimal ___, which results in a suboptimal ___ model."
6. 理论贡献:"As ___ is stochastic in its nature, we derive its analytical form which provably demonstrates its ___ effect in expectation, and captures the variance of ___."
7. 消融变贡献:"For completeness, we devise other ___ models, based on ___, whose ___ profiles differ with our method."
8. 借定理三明治:"To show NAME achieves the improved ___ we quote the following theorem [___]. ... Theorem 1 says the key to ___ is ___. NAME improves ___ by design."
9. 理论定超参:"The best ___ effect is achieved for k = ___. ... Thus, in all experiments (including ___), we set k = ___."
10. 插件增益:"we find that the performance of ___ improves by a large margin when integrating with NAME (e.g., major baseline, ___, yields N% and M% gain on ___), which shows that NAME is complementary to ___."
11. 数字连祷文:"X yields a%, b% and c% gain on D1, D2, and D3. ... Importantly, when both are applied, the gain is g%, h% and i%."
12. 判负解释:"As ___ binarizes/ignores ___, it may reject some useful signal at ___."

### 2.11 "不完全幂迭代"包装七层
方法实体:一次矩阵-向量乘 + 一次 rank-1 减法(三行 PyTorch)。
1. **缺陷重命名为体制(regime)**:幂迭代只跑一步 = "没收敛";命名为 "incomplete power iteration" 后,不收敛的两个副作用被逐条转写为两个设计目标——**命名完成了从 bug 到 feature 的产权登记**。
2. 期望层定理(Prop.1)做正当性(唯一必要的理论)。
3. **解析闭式(Prop.2&3)做格调**:没人会在训练中计算这些闭式;功能是 (a) 宣示"完全理解该算子" (b) 支撑解析—仿真吻合仪式 (c) 反哺超参选择 (d) 分工上是资深作者的进场处。
4. **借来的泛化界(Theorem 1)做天花板**:整个引自他人,SFA 只证容易的一环;**摘要里未注明界是借的**——声誉借贷的标准操作。
5. **SVD 透镜改写损失函数**:方法没变、损失没变,**变的是观察损失的坐标系——透镜即贡献**。
6. **事后建构设计空间**:围绕赢家造出算子家族,逐一击败并用理论解释败因——消融被抬成分类学,写进贡献。
7. **防御性收缩**:complementary / compatible / negligible overhead / plug-and-play——**把主张面缩到"加了不亏",审稿风险最小化**。

---

## 第三部分:跨篇总结

### 3.1 团队集体写作指纹
**A. 续集式自我模板复用(最硬指纹)**:两篇之间成段逐字/近逐字复用——领域定调句(同句同引文)、GCL 定义句(同义词替换级复用)、Notation 节、投影头说明、评测协议段、致谢;SFA 消融表的无增强基线数字直接续用 COSTA 的数值。**成熟的论文生产线:固定骨架文件,每篇换心脏(算子 + 其理论)**。

**B. 三层配方**:①用自造透镜诊断出一个可量化的病;②给出 1–3 行线性代数操作当药;③从数值线性代数与统计工具箱拉理论给药定价。**理论的四个具体用途:预判赢家、钦定超参、解释败局、抬升命名**。

**C. 版式指纹**:淡青色圆角 takeaway 框;管线图新模块黄色高亮、其余灰调;结果表自家行青底;×/✓ 消融网格;教学式表注;图内嵌注释。

**D. 结构指纹**:摘要 = 让步/定调开场 + "vital/plausible ... but scarcely/not well researched" 缺口公式 + "Inspired by/we present a novel + 命名 + which 机制"提案句 + 零数字结果句;理论 = 小标签正文陈述 + "Proof. See supplementary" + Remark/青框翻译层,大标签只给引进结果;实验 = 主表 + 插件增益表 + 效率证据 + ×/✓ 消融 + 理论回执小节。

**E. 句法词汇指纹**:斜杠反义对 15+ 处;"so-called" 高频;"To this end,"/"Thus,"/"Below,"/"Note that"/"Notably,"/"Importantly,";"we opt for";数字连祷文;方法名+下标变体命名法(COSTA_SV、SFA_InfoNCE)。

**F. 修辞姿态指纹**:窄域 first 声明;"It is somewhat surprising"式主动暴露反直觉再编号解释;**输局必解释且解释必回扣自家理论**;complementary/compatible/negligible overhead 的防御性主张收缩;长 caption 承担论证。

**G. 生产纪律(反面)**:typo/引文错误密度显著高于顶会平均——**精力预算倾斜给数学与实验,散文润色最后被牺牲**。模仿时该刻意规避。

**H. 分工可见性**:**朴素叙事层(学生)+ 线性代数创意层(Zhu 的 sketching/谱方法血统)+ 理论装甲层(Koniusz)** 的三明治。

### 3.2 venue 适配差异(同一团队的自我调节)

| 维度 | COSTA @ KDD | SFA @ AAAI |
|---|---|---|
| RQ 结构 | RQ1–RQ4 显式列出并进小节标题 | 无,改 Main Results + Analysis 两段式 |
| Notation | 正文独立小节 | 移入补充材料 |
| 理论标签 | Definition + Lemma + Remark(小标签) | Proposition(原创)+ 引用 Theorem |
| Figure 1 | 实验证据图(散点) | 机制漫画(与摘要并排) |
| 实验广度 | 单任务 × 9 数据集 + 效率 | 四任务证 "and Beyond" |
| 命名 | 强 backronym | 平实缩写 + "and Beyond" 后缀 |

**一句话总结**:高度模板化的"续集流水线"——骨架文本跨篇复用,每篇的差异化投资集中在 (a) 一个被精心命名的极简线性代数算子、(b) 围绕它临时搭建的理论装甲、(c) 青框/黄框/青底行的视觉说服系统;散文润色被系统性放在优先级最后。**模仿其长处(缺口公式、算子命名术、理论四用途、输局解释术、插件三连主张),规避其短处(typo、引文错配)。**
