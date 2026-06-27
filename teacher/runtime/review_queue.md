# review_queue.md — 间隔复习队列

> 复习间隔硬编码：课后 1 天 / 3 天 / 7 天 / 14 天
> AI 在每课**课前复习环节**检查本文件中的到期复习项。
> 每课课后新增本课薄弱点。
>
> 教学模式影响：
> - **粗略模式**：每个知识点 1 次课前复习激活 + 1 次间隔复习
> - **精细模式**：每个知识点 课前复习 + 课后总结 + 2~3 次间隔复习

## 队列格式

`| {知识点} | {掌握程度} | {添加日期} | {下次复习日期} | {已复习次数} | {课程ID} |`

### 掌握程度标记

- `概念 ✓ / 应用 ✓` = 完全掌握
- `概念 ✓ / 应用 ~` = 概念理解，应用待强化
- `概念 ~ / 应用 ~` = 部分掌握，两个维度都需要复习
- `概念 ? / 应用 ?` = 状态不明

### 复习日期计算规则

```
第 1 次复习：添加日期 + 1 天
第 2 次复习：第 1 次复习日期 + 2 天（实际间隔 2 天，累计 3 天）
第 3 次复习：第 2 次复习日期 + 4 天（实际间隔 4 天，累计 7 天）
第 4 次复习：第 3 次复习日期 + 7 天（实际间隔 7 天，累计 14 天）
```

---

## 活跃队列

| 知识点 | 掌握程度 | 添加日期 | 下次复习日期 | 已复习次数 | 课程ID |
|--------|---------|---------|-------------|-----------|--------|
| 训练集与测试集的划分目的 | 概念 ✓ / 应用 ✓ | Day 1 | Day 2 | 0 | ml-yearning |
| 早停法（Early Stopping） | 概念 ✓ / 应用 ~ | Day 1 | Day 2 | 0 | ml-yearning |
| 过拟合的直觉理解 | 概念 ✓ / 应用 ~ | Day 1 | Day 4 | 0 | ml-yearning |
| Vibe Coding 光谱（Vibe → Agentic Engineering） | 概念 ✓ / 应用 ✓ | Day — | Day +1 | 0 | kaggle-agent |
| Context Engineering 六种上下文类型 | 概念 ✓ / 应用 ✓ | Day — | Day +1 | 0 | kaggle-agent |
| 静态 vs 动态上下文分类 | 概念 ✓ / 应用 ✓ | Day — | Day +3 | 0 | kaggle-agent |
| Progressive Disclosure 模式 | 概念 ✓ / 应用 ✓ | Day — | Day +3 | 0 | kaggle-agent |
| Factory Model（角色定位：设计生产代码的系统） | 概念 ✓ / 应用 ✓ | Day — | Day +1 | 0 | kaggle-agent |
| Harness 7 组件（指令/工具/沙箱/编排/护栏/记忆/可观测） | 概念 ✓ / 应用 ✓ | Day — | Day +1 | 0 | kaggle-agent |
| Memory vs Knowledge 分类（来源决定归属） | 概念 ✓ / 应用 ✓ | Day — | Day +3 | 0 | kaggle-agent |
| Factory vs Harness 区分（思考方式 vs 技术架构） | 概念 ✓ / 应用 ✓ | Day — | Day +3 | 0 | kaggle-agent |
| MCP 协议核心概念（发现/配置/连接） | 概念 ✓ / 应用 ✓ | 2026-06-21 | 2026-06-24 | 1 | kaggle-agent |
| NxM 原型问题与 MCP 解决原理 | 概念 ✓ / 应用 ✓ | 2026-06-21 | 2026-06-24 | 1 | kaggle-agent |
| MCP 调试方法（Inspector/stdio vs SSE） | 概念 ✓ / 应用 ✓ | 2026-06-21 | 2026-06-24 | 1 | kaggle-agent |
| Vibe Coder Toolkit 最佳实践 | 概念 ✓ / 应用 — | 2026-06-21 | 2026-06-24 | 0 | kaggle-agent |
| A2A 协议概念（Agent Card/Discovery/Task 生命周期） | 概念 ✓ / 应用 ✓ | 2026-06-21 | 2026-06-24 | 1 | kaggle-agent |
| MCP vs Context Engineering vs Harness 三层区分 | 概念 ✓ / 应用 — | 2026-06-21 | 2026-06-24 | 0 | kaggle-agent |
| A2A 协议三要素与工作原理 | 概念 ✓ / 应用 ✓ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| 智能体架构四模式（Simple/并行/Chain/Agent Team） | 概念 ✓ / 应用 ✓ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| Bounded vs Unbounded Domain 边界判定 | 概念 ✓ / 应用 ~ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| GOTO Problem（够用但不完整的信息传递陷阱） | 概念 ✓ / 应用 ~ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| Skill 解剖结构（Trigger/Instruction/Tools/Examples） | 概念 ✓ / 应用 ✓ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| 两条构建路径（翻译已知 vs 结晶新知） | 概念 ✓ / 应用 ✓ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| Skill vs MCP vs AGENTS.md 三层分工 | 概念 ✓ / 应用 ✓ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| Skill 评估三维度（输出质量/工具轨迹/Token 预算） | 概念 ✓ / 应用 ~ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| 工具轨迹分析方法 | 概念 ✓ / 应用 ~ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| 7-Pillar Agent Security Architecture | 概念 ✓ / 应用 — | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| 数据保护三维度（传输/存储/上下文边界） | 概念 ✓ / 应用 — | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| High-Risk Authorization 模式 | 概念 ✓ / 应用 ~ | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |
| Output Evaluation vs Trajectory Evaluation | 概念 ✓ / 应用 — | 2026-06-22 | 2026-06-23 | 0 | kaggle-agent |

## 已完成复习

（初始为空）
