# session_log.md — agent-skills 课堂日志

> agent-skills（Agent Skills）课程专属日志。
> 同行学习者：帕姆（Pom-Pom）

---

（等待第一课记录）


---

## Ch.1 — 三月 | 模式: 精细模式

**课堂摘要**：学生从"定义+边界+示例"的三要素框架出发描述 Skill——与教材的 SKILL.md 结构（name+description → Instruction → examples/）几乎完全对齐。关键穿透：三月引入"逻辑边界 vs 数据边界"的区分，学生理解了 Skill 边界包含应用范围和数据访问范围两个维度。Progressive Disclosure 以"metadata in context, details on demand"锚定。两条构建路径和三层边界区分在 Kaggle Ch.5 的基础上自然衔接。

**帕姆表现**：用"今天不是新课，是给已经会的东西换了一个名字"总结整节课，三月评价"比我总结得好"。

**课前复习**：无到期项（新课首次课）。

**课后总结**：学生确认了定义→对应元数据，边界→对应 Instruction+配置范围，示例→对应 examples/ 目录。

**角色暗线释放**：无。


---

## Ch.2 — 丹恒 | 模式: 精细模式

**课堂摘要**：以"你为什么相信这个 Skill 是好的"切入。学生理解了 Evaluation Toolkit 四道门（Trigger → Output Quality → Tool Trajectory → Token Budget），区分了精确匹配 vs 意图匹配两种 Trigger 粒度并选择了精确匹配。核心穿透：System vs Skill Evaluation Illusion（问题出在系统还是 Skill）和 Token Budget Isolation 陷阱（隔离测试的 Token 数据不可靠）。课后总结覆盖了"结果/方法/成本"三维度和"先检查 Trigger"原则。

**帕姆表现**：用"按错车厢按钮→不需要分析广播质量"类比 Trigger 第一道门。

**课前复习**：无到期项。

**课后总结**：完整——结果对不对、方法正不正确、成本高不高。出问题先查 Trigger。


---

## Ch.3 — 三月 | 模式: 精细模式

**课堂摘要**：从"最长的那一行"Token 消耗表切入，学生通过"Harness 包含什么"的反问自然定位到 Runtime 的可观测与编排两个组件。核心穿透路径：Agent Runtime 内部流程 → Context Overflow 机制（"爆炸的信息量"）→ Skill 作为改进单元的上下文管理 → 接力 vs 嵌套两种协作模式 → Token 预算上下限（1亿→窗口上限→一次运行所需的最小 Token）→ Production Degradation 循环。两个预设问题学生都给出了自己的答案（"先调另一个 Skill，再运行这个"→接力；"最少到运行一次需要的 Token"→下限），自然对接了生产化的核心观点。

**帕姆表现**：本课未出场。

**课前复习**：无到期项。

**课后总结（学生自述）**：技能设计要注意经济性、Token 上下限设定等经验性知识——理论不能完全解释，需要经验积累。三月评价："经济性不是结论——是你在代价和收益之间选了一个自己站得住的位置。"

**角色暗线释放**：三月以自己的"类比翻车×1"便签为伏笔，在本课中保持了教学深度——在"1亿"处笑了一下但立即收住回到正经内容。下课后的"那行最贵的"揭示作为课后彩蛋，保持了三月在 kaggle-agent Ch.3 时建立的"翻车但诚实"的角色锚点。


---

## Ch.4 — 丹恒 🗡️ | 模式: 精细模式

**课堂摘要**：课前复习检测了 Ch.1-3 的掌握——学生准确回答了 Trigger 优先级和接力/嵌套的区别，逻辑边界/数据边界已遗忘，丹恒直接复述了定义。核心穿透路径：课前复习（遗忘确认+直接补充）→ DAG Orchestration（有向无环图 + 并行依赖 + 无共享上下文 → 无 Overflow）→ Capability Profile（Name/Schema/Dependencies 四字段 → 系统目录）→ Meta-Skills 机制（Skill 生成 SKILL.md）→ Self-Improving 回路 → Convergence Problem（无法证明收敛）→ 需要人工确认上线 → Context Debt（10+ Skill 后维护成本折线）。学生的 DAG 问题（全称/用法/范围/例子 + Skill Composition 定义）全部得到完整回答。

**帕姆表现**：本课未出场。

**课前复习**：3/3 到期项。正确：Trigger 是 eval 第一道门（"错了后面无意义"）、接力 vs 嵌套（"接力，避免 Context Overflow"）。遗忘：逻辑边界/数据边界（已直接补充）。

**课后总结（学生自述）**：总结完整覆盖了 DAG Orchestration、Capability Profile、Meta-Skills 机制、Convergence Problem、人工上线确认五层。丹恒评价"全对。没有需要纠正的。"

**角色暗线释放**：无。


---

## Ch.5 — 三月 🎀 | 模式: 精细模式

**课堂摘要**：三月带笔记本电脑——"不看教材，看 real world"。从"做/买/组合"决策框架的真实应用出发，学生用两个项目想法（高中数学家教系统 + 每周 AI 项目搜集）完整走了一遍 Discovery → Evaluation → Decision 流程。学生选择了组合路线，通过搜索发现 MathClaw（多模态数学助手，MIT）、Khayyam Math、MathPilot 等现成项目，并定位了 KaTeX 作为公式渲染方案。核心穿透：Skill 组合拓扑设计 → Dependencies 作为最重要的评估维度 → 7 项检查清单 → 天文台自身结构对照（发现它与 Skill 制式的加载策略同构）→ Token 节省估算（约 50%）→ 决定暂不重构 → 用 Skill Creator 的 6 步流程澄清了 Meta-Skill 的人机分工边界。

**帕姆表现**：未出场。

**课前复习**：到期项覆盖 Ch.3 和 Ch.4。正确：Token 预算上下限（上限=窗口略低、下限=一次运行）、DAG vs Chain（并行 + 避免 Context Overflow）。

**课后总结（学生自述）**："介绍了设计/评估 Skill 时需要考虑什么。"

**角色暗线释放**：无。


---

## Ch.6 — 丹恒 🗡️（最终课）| 模式: 精细模式

**课堂摘要**：丹恒关掉投影，打开了一份零售企业案例文档（RetailCo，600+ 门店客服系统重构）。逐层拆解了案例中踩过的四个坑及修复方案：坑 1 — 一个 Skill 做太多事（修复：分层路由 Routing → 粗分类 → 细分类 → 执行）；坑 2 — 嵌套替代接力（修复：DAG 编排）；坑 3 — 没有 Token 预算上限（修复：设上下限）；坑 4 — 没有 Capability Profile（修复：强制写 Profile）。学生将六课内容用一句话串起：Routing 识别 → 搜索已有 Skill → 匹配则执行 → 不匹配则 Meta-Skill 生成。学生纠正了丹恒说"六个坑"的错误（实际是四个）。最终 Cheatsheet 六条 + 教材核心结论：Skills are an organizational decision。

**帕姆表现**：帕姆坐在旁边，带了刷子。在丹恒讲"一个篮子装太多鸡蛋"时轻轻接了一句。在听到学生总结"Routing + Meta-Skill = 自生长"时尾巴动了一下说："那它就从一个客服系统变成一个能自己长大的客服系统了。"

**课前复习**：本轮未做（最后一课，整课为案例研究）。

**课后总结（学生自述）**："这门课介绍了 skill 的概念、坑、和实际应用中可能遇到的问题。skill 是一个组织技巧。"

**角色暗线释放**：帕姆在本课中出场带刷子——这是 agent-skills 课程中帕姆第一次以物理在场的角色出现（之前只在群聊中被提及）。丹恒在课程结束时没有回头，但把案例文档留在了桌上。
