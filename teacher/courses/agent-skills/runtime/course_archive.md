# 📚 Agent Skills 课程总档

> **课程全称**：Agent Skills——构建、评估与生产化
> **教材**：Tanvi Singhal 等 — *Agent Skills* (Kaggle Day 3, 2026)
> **总页数**：62 页
> **课次数**：6 课
> **教学模式**：精细模式（深耕型）
> **授课教师**：三月 🎀（奇数课）、丹恒 🗡️（偶数课）
> **同行学习者**：帕姆（Pom-Pom）
> **学习周期**：2026-06-23 ~ 2026-06-27

---

## 一、课程知识体系总览

```
Skill 解剖 (Ch.1) → 评估方法 (Ch.2) → 生产化 (Ch.3)
→ Meta-Skills & 组合 (Ch.4) → 决策框架 (Ch.5) → 案例研究 (Ch.6)
```

---

## 二、逐课核心内容

### Ch.1 — Skill 解剖与构建（三月 🎀 | p6-11）

**知识点**：
- 概念：Skill 解剖结构（Metadata + SKILL.md + scripts/references/assets）
- 概念：Progressive Disclosure（三级加载——元数据常驻 / body 按需 / 资源 demand）
- 概念：两条构建路径（翻译已知 vs 结晶新知）
- 概念：Skill vs MCP vs AGENTS.md 三层分工（AGENTS.md=你是谁 / MCP=用什么做 / Skill=怎么做）
- 应用：创建完整 Skill 目录结构和 SKILL.md
- **精细扩展**：Skills 作为"程序性记忆"

**核心穿透**：逻辑边界（写在 Instruction 里） vs 数据边界（写在 MCP 配置范围里）

**学生课后总结**：定义→元数据，边界→Instruction+配置，示例→examples/ 目录

**帕姆**："今天不是新课，是给已经会的东西换了一个名字。"

---

### Ch.2 — 评估方法与 Toolkit（丹恒 🗡️ | p12-24）

**知识点**：
- 概念：Evaluation Toolkit 四道门（Trigger → Output Quality → Tool Trajectory → Token Budget）
- 概念：System vs Skill Evaluation Illusion（问题出在系统还是 Skill）
- 概念：Trigger 作为 eval 的第一道门
- 概念：Skills 流行三大驱动力
- 应用：选择 Skill 应用形态、设计评估用例、区分改进对象、设计 Trigger
- **精细扩展**：Token Budget Isolation 陷阱（隔离测试不可靠）

**核心穿透**：结果对不对 / 方法正不正确 / 成本高不高

**学生课后总结**：完整——结果对不对、方法正不正确、成本高不高。出问题先查 Trigger。

**帕姆**："按错车厢按钮→不需要分析广播质量。"

---

### Ch.3 — 生产化与 Context Overflow（三月 🎀 | p25-31）

**知识点**：
- 概念：Agent Runtime 内部构成
- 概念：Context Overflow 机制（上下文随着多次 Skill 调用膨胀，质量和 Token 成本双降）
- 概念：Skills 作为"改进单元"（边界即上下文管理边界）
- 应用：识别并预防 Overflow、通过 Skill 拆分解决 Token 预算问题、单体 Agent 拆解
- **精细扩展**：Production Degradation 循环（Overflow → 质量降 → 重试 → 更多 Token → Overflow 加深）

**核心穿透**：
- 接力（Chaining）：先 A 后 B，分开跑，Context 各自释放
- 嵌套（Nesting）：A 里调 B，Context 合并增长——Overflow 高发区
- Token 预算上限 = 模型窗口大小，下限 = 一次成功调用的最小 Token 数

**学生课后总结**：技能设计要注意经济性、Token 上下限设定等经验性知识——理论不能完全解释，需要经验积累。

**三月评价**："经济性不是结论——是你在代价和收益之间选了一个自己站得住的位置。"

---

### Ch.4 — Meta-Skills 与组合（丹恒 🗡️ | p32-38）

**知识点**：
- 概念：Meta-Skills 机制（Skill 生成/修改 SKILL.md）
- 概念：Self-Improving 回路与 Convergence Problem（无法证明循环收敛）
- 概念：Skill Composition（Chain / DAG / Orchestration 三种模式）
- 应用：设计 Meta-Skill、判断 Self-Improving 场景、DAG 编排、Capability Profile 设计
- **精细扩展**：Context Debt（10+ Skill 后维护成本折线）

**核心穿透**：
- DAG 全称：Directed Acyclic Graph（有向无环图）
- DAG vs Chain：并行 + 依赖 vs 串行，无共享上下文 → 无 Overflow
- Capability Profile 四字段：Name / Description / I/O Schema / Dependencies
- Meta-Skill 需人工确认上线——人机分工

**学生课后总结**：五层全覆盖（DAG / Profile / Meta-Skills / Convergence / 人工上线）

**丹恒评价**："全对。没有需要纠正的。"

---

### Ch.5 — 最佳实践与决策（三月 🎀 | p39-42）

**知识点**：
- 概念：Actionable Best Practices 核心原则
- 概念：Skills 选择框架（做 Build / 买 Buy / 组合 Compose）
- 应用：在数百个 Skill 中做出合理选择、评估做 vs 买 vs 组合决策
- **精细扩展**：Skills 生态系统演进趋势

**核心穿透**：
- 7 项检查清单：Trigger / Output / Dependencies / Profile / 社区活跃度 / License / 回滚方案
- Dependencies 是最重要的评估维度——决定实际集成成本
- Skill 组合拓扑设计
- Discovery → Evaluation → Decision 完整流程（真实项目演练）

**项目实战**：
- 高中数学家教系统：检索 Skill + 知识图谱 + 讲解生成 + 题目生成 + KaTeX 渲染
- 每周 AI 项目搜集：搜索 → 筛选 → 摘要 → 推送

**发现**：
- MathClaw（多模态数学助手，MIT）— github.com/spiderswx/MathClaw
- Khayyam Math（语音 + SVG + 五级验证）
- MathPilot（多 Agent 架构）
- KaTeX 作为公式渲染方案
- MathClaw 的 skill-creator 是 Meta-Skill 的参考实现

**天文台结构对照**：天文台的分层加载策略与 Skill 的 Progressive Disclosure 同构，Skill 化可省约 50% Token。

**学生课后总结**："介绍了设计/评估 Skill 时需要考虑什么。"

---

### Ch.6 — Cheatsheet + 案例研究（丹恒 🗡️ | p43-62）

**知识点**：
- 概念：SKILL.md 模板的最小结构和完整规范
- 概念：垂直 Skills 在零售行业的实际应用
- 应用：Cheatsheet 快速创建 Skill、行业案例提炼复用模式、治理层级设计
- **精细扩展**：Skills 作为企业可持久资产的工程理念

**RetailCo 案例四坑**：

| # | 坑 | 修复方案 | 对应 |
|---|-----|---------|------|
| 1 | 一个 Skill 做太多事 | 分层路由：粗分类→细分类→执行 | Ch.1 边界 |
| 2 | 嵌套替代接力 | DAG 并行编排 | Ch.3 接力 vs 嵌套 |
| 3 | 没有 Token 预算上限/下限 | 设置上限=窗口大小，下限=一次运行 | Ch.3 Token 预算 |
| 4 | 没有 Capability Profile | 强制每个 Skill 写 Profile | Ch.4 Profile |

**Routing 层设计**：
```
用户输入 → Router Skill（极轻）
  → 匹配已有 Skill → 执行
  → 不匹配 → Meta-Skill 生成新 SKILL.md → 注册
```

**Read / Draft / Act 三级治理**：
- Read：只读查询，权限最低
- Draft：需确认才能执行
- Act：自动执行

**Cheatsheet 六条**：
1. 先定义边界，再写逻辑
2. Token 预算是对上下文最大的尊重
3. 优先接力，避免嵌套
4. 依赖越深的 Skill，可组合性越差
5. 人机分工要清楚
6. 治理想清楚再放权

**教材最终结论**：
> *"Skills are not a technology decision. They are an organizational decision."*

**学生课后总结**："这门课介绍了 skill 的概念、坑、和实际应用中可能遇到的问题。skill 是一个组织技巧。"

**帕姆**："那它就从一个客服系统变成一个能自己长大的客服系统了。"

---

## 三、全课程核心概念索引

| 概念 | 课程 | 一句话定义 |
|------|------|-----------|
| Progressive Disclosure | Ch.1 | 元数据永远在上下文，细节按需加载 |
| Evaluation Toolkit | Ch.2 | 四道门：Trigger → 质量 → 轨迹 → 预算 |
| Context Overflow | Ch.3 | 多个 Skill 调用后上下文膨胀，质量和成本双降 |
| 接力 vs 嵌套 | Ch.3 | 接力(Context释放) vs 嵌套(Context合并增长) |
| Token 预算上下限 | Ch.3 | 上限=窗口大小，下限=一次运行所需 |
| Production Degradation | Ch.3 | Overflow → 重试 → 更严重 Overflow 的循环 |
| DAG Orchestration | Ch.4 | 有向无环图，并行 + 依赖，无共享上下文 |
| Capability Profile | Ch.4 | Name/Schema/Dependencies 四字段 = 系统的目录 |
| Meta-Skills | Ch.4 | 生成或修改 SKILL.md 的 Skill |
| Convergence Problem | Ch.4 | 无法证明 Self-Improving 循环会收敛 |
| Context Debt | Ch.4 | Skill > 10 后维护成本折线 |
| 做/买/组合 | Ch.5 | 核心价值自己做，标准化组合，依赖多就买 |
| 治理层级 | Ch.6 | Read / Draft / Act 三级权限 |

---

## 四、文件索引

| 文件 | 内容 |
|------|------|
| `runtime/session_log.md` | 六课完整课堂日志 |
| `runtime/diary.md` | 六课学习日记（学生视角） |
| `runtime/progress.md` | 进度追踪表 |
| `runtime/review_queue.md` | 全部复习知识点队列 |
| `runtime/mistake_log.md` | 错题本 |
| `config/knowledge_points/ch01~06.md` | 六课知识点清单 |
| `story_progression/ch01~06.md` | 六课故事节点 |
| `memory/ch01.md` | Ch.1 教学记忆 |
| `memory/ch02.md` | Ch.2 教学记忆 |
| `config/system_core.md` | 核心教学引擎 |
| `config/course_catalog.md` | 课程目录（含 agent-skills） |
| `config/learner_profile.md` | 学习者档案（含教学模式偏好） |

---

*课程生成：天文台教学系统 · Agent Skills 课程*
*完结日期：2026-06-27*
