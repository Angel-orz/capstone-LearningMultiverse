# course_catalog.md — 课程目录

> 本文件在新会话首次启动时加载。用户选择课程后，所选课程的 ID 记录到 learner_profile.md。
> 后续会话跳过课程选择，直接进入所选课程。

## 课程列表

| 课程ID | 课程名称 | 教材 | 总章节 | 总页数 | 课次数 | 授课教师 |
|--------|---------|------|--------|-------|--------|---------|
| ml-yearning | ML 策略与诊断 | Machine Learning Yearning | 58 | 118 | 14 | 三月 / 丹恒 |
| kaggle-agent | AI Agent 工程化 | Kaggle Agent 系列 Day 1-4 | 4 篇 | 203 | 6 | 三月 / 丹恒 |
| agent-tools-interoperability | Agent 工具与互操作 | Agent Tools & Interoperability Day 2 | 1 篇 | 49 | 5 | 三月 / 丹恒 |
| agent-skills | Agent Skills | Agent Skills Day 3 | 1 篇 | 62 | 6 | 三月 / 丹恒 |

---

### agent-tools-interoperability — Agent 工具与互操作

- **全称**：Agent Tools & Interoperability——从 MCP 到商业协议
- **教材**：Kanchana Patlolla 等 — *Agent Tools & Interoperability* (Kaggle Day 2, 2026)
- **总页数**：49 页
- **课次数**：5 课（每课约 9-10 页）
- **授课教师轮值**：三月（奇数课）、丹恒（偶数课）
- **同行学习者**：帕姆（Pom-Pom）
- **起点要求**：有 Agent 工程化基础知识（或完成 kaggle-agent 课程）
- **知识体系**：
  ```
  MCP 深化 (Ch.1) → A2A 架构 (Ch.2) → 协议实现 (Ch.3)
  → A2UI 交互 (Ch.4) → 商业协议 (Ch.5)
  ```
- **教材路径**：`Docs/Kaggle/Agent Tools & Interoperability_Day_2.pdf`

#### 课次划分

| 课次 | 教师 | 教材范围 | 页数 | 核心主题 |
|------|------|---------|------|---------|
| Ch.1 | 三月 | p6-16 | 11 | MCP 回顾与深化（发现/配置/连接/调试/最佳实践） |
| Ch.2 | 丹恒 | p17-23 | 7 | A2A 架构演进（内部/外部专业化、边界、GOTO） |
| Ch.3 | 三月 | p24-30 | 7 | A2A 实现（Agent Card、注册中心、协议扩展） |
| Ch.4 | 丹恒 | p31-42 | 12 | A2UI + Generative UI + Canvas |
| Ch.5 | 三月 | p43-49 | 7 | AP2 + UCP 商业协议 |

---

## 详细课程信息

### agent-skills — Agent Skills

- **全称**：Agent Skills——构建、评估与生产化
- **教材**：Tanvi Singhal 等 — *Agent Skills* (Kaggle Day 3, 2026)
- **总页数**：62 页
- **课次数**：6 课（每课约 10 页）
- **授课教师轮值**：三月（奇数课）、丹恒（偶数课）
- **同行学习者**：帕姆（Pom-Pom）
- **起点要求**：已完成 MCP 和 A2A 基础知识
- **知识体系**：
  ```
  Skill 构建 (Ch.1) → 评估方法 (Ch.2-3) → 生产化 (Ch.3)
  → Meta-Skills (Ch.4) → 组合实践 (Ch.5) → 案例研究 (Ch.6)
  ```
- **教材路径**：`Docs/Kaggle/Agent Skills_Day_3.pdf`

#### 课次划分

| 课次 | 教师 | 教材范围 | 页数 | 核心主题 |
|------|------|---------|------|---------|
| Ch.1 | 三月 🎀 | p6-11 | 6 | Skill 解剖 + 两条构建路径 + Skill vs MCP vs AGENTS.md |
| Ch.2 | 丹恒 🗡️ | p12-24 | 13 | 评估入门 + Evaluation Toolkit |
| Ch.3 | 三月 🎀 | p25-31 | 7 | Token 预算 + 生产化 + Context Overflow |
| Ch.4 | 丹恒 🗡️ | p32-38 | 7 | Meta-Skills + 组合与打包 |
| Ch.5 | 三月 🎀 | p39-42 | 4 | 最佳实践 + 决策指南 |
| Ch.6 | 丹恒 🗡️ | p43-62 | 20 | Cheatsheet + 零售案例研究 |

---

### ml-yearning — ML 策略与诊断

- **全称**：机器学习策略与诊断（Machine Learning Strategy & Diagnosis）
- **教材**：Andrew Ng — *Machine Learning Yearning* (2018)
- **总章节**：58 章
- **总页数**：118 页
- **课次数**：14 课（每课约 8-9 页 / 4-5 章）
- **授课教师轮值**：三月（奇数课）、丹恒（偶数课）
- **起点要求**：零基础
- **知识体系**：
  ```
  ML 策略基础 (Ch.1-4) → 评估与迭代 (Ch.5-12)
  → 高级决策 (Ch.13-44) → 诊断与归因 (Ch.45-58)
  ```
- **教材路径**：`materials/textbook/andrew-ng-machine-learning-yearning.pdf`

#### 课次划分

| 课次 | 教师 | 教材章节 | 页数范围 | 核心主题 |
|------|------|---------|---------|---------|
| Ch.1 | 三月 | 1-4 | 1-10 | ML 战略、规模驱动进步 |
| Ch.2 | 丹恒 | 5-8 | 10-18 | 开发/测试集、评估指标 |
| Ch.3 | 三月 | 9-12 | 18-25 | 优化/满足指标、迭代 |
| Ch.4 | 丹恒 | 13-16 | 26-34 | 误差分析、系统建立 |
| Ch.5 | 三月 | 17-20 | 34-43 | 集大小、偏差与方差 |
| Ch.6 | 丹恒 | 21-24 | 44-52 | 比较最优误差、权衡 |
| Ch.7 | 三月 | 25-28 | 53-62 | 减少偏差/方差、学习曲线 |
| Ch.8 | 丹恒 | 29-32 | 63-69 | 绘制训练误差、解读 |
| Ch.9 | 三月 | 33-36 | 70-78 | 人类级表现、分布差异 |
| Ch.10 | 丹恒 | 37-40 | 79-86 | 数据利用、加权 |
| Ch.11 | 三月 | 41-44 | 87-96 | 数据不匹配、人工合成 |
| Ch.12 | 丹恒 | 45-48 | 97-104 | 优化验证、端到端 |
| Ch.13 | 三月 | 49-52 | 105-111 | 端到端优劣、Pipeline |
| Ch.14 | 丹恒 | 53-58 | 112-118 | 误差归因、综合诊断 |

---

### kaggle-agent — AI Agent 工程化

- **全称**：AI Agent 工程化——从 Vibe Coding 到生产级智能体
- **教材**：Kaggle Agent 系列论文（Google, 2026）
  - Day 1：*The New SDLC With Vibe Coding* — Addy Osmani 等
  - Day 2：*Agent Tools & Interoperability* — Kanchana Patlolla 等
  - Day 3：*Agent Skills* — Tanvi Singhal 等
  - Day 4：*Vibe Coding Agent Security and Evaluation* — Sokratis Kartakis 等
- **总篇数**：4 篇
- **总页数**：203 页
- **课次数**：6 课（每课约 18-35 页）
- **授课教师轮值**：三月（奇数课）、丹恒（偶数课）
- **起点要求**：有基础软件开发经验
- **知识体系**：
  ```
  基础与范式 (Day 1) → 工具与架构 (Day 2)
  → 技能构建 (Day 3) → 安全与生产 (Day 4)
  ```
- **教材路径**：
  - Day 1：`Docs/Kaggle/Day_1_v3.pdf`
  - Day 2：`Docs/Kaggle/Agent Tools & Interoperability_Day_2.pdf`
  - Day 3：`Docs/Kaggle/Agent Skills_Day_3.pdf`
  - Day 4：`Docs/Kaggle/Vibe Coding Agent Security and Evaluation_Day_4.pdf`

#### 课次划分

| 课次 | 教师 | 教材 | 页数 | 核心主题 |
|------|------|------|------|---------|
| Ch.1 | 三月 | Day 1 p1-18 | 18 | Vibe Coding 光谱 + Context Engineering |
| Ch.2 | 丹恒 | Day 1 p19-38 | 20 | Factory Model + Harness Engineering |
| Ch.3 | 三月 | Day 2 p1-25 | 25 | MCP 协议 + 工具实操 |
| Ch.4 | 丹恒 | Day 2 p26-49 | 24 | A2A + 智能体架构模式 |
| Ch.5 | 三月 | Day 3 p1-35 | 35 | Agent Skills 构建与评估 |
| Ch.6 | 丹恒 | Day 3-4 p36-103 | 35+ | 安全架构 + 生产实践 |

---

## 扩展说明

### 添加新课程

后续添加课程时，按以下格式在"课程列表"表格中添加新行，并在下方补充详细章节信息：

```markdown
### {course-id} — {课程名称}
- **教材**：{作者} — {书名}
- **总章节**：{N} 章
- **总页数**：{N} 页
- **课次数**：{N} 课
- **授课教师**：{教师列表}
- **知识体系图**：{ASCII 图}
```

同时需要在以下位置添加课程对应内容：
- `teacher/config/knowledge_points/` — 按课次的知识点文件（课程ID为子目录名）
- `teacher/story_progression/` — 按课次的故事节点（课程ID为子目录名）
- `teacher/characters/` — 授课教师角色文件（可复用）
