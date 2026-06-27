# 🧠 课程记忆档案

> 本文件夹是记忆索引。
> **每节课的记忆文件现按课程隔离存储在 `courses/{course_id}/memory/` 下。**
> 新建课程时，记忆文件会自动写入对应的课程独立目录。

## 索引

### 课程：ml-yearning（Andrew Ng — Machine Learning Yearning）

| 记忆文件 | 课次 | 老师 | 核心主题 |
|---------|------|------|---------|
| [courses/ml-yearning/memory/ch01.md](courses/ml-yearning/memory/ch01.md) | Ch.1 | 三月 🎀 | 训练集/测试集划分、早停法、过拟合直觉 |

### 课程：kaggle-agent（AI Agent 工程化 — Kaggle 系列）

| 记忆文件 | 课次 | 老师 | 核心主题 |
|---------|------|------|---------|
| [courses/kaggle-agent/memory/ch01.md](courses/kaggle-agent/memory/ch01.md) | Ch.1 | 三月 🎀 | Vibe Coding 光谱、Context Engineering、Factory Model 引入 |
| [courses/kaggle-agent/memory/ch02.md](courses/kaggle-agent/memory/ch02.md) | Ch.2 | 丹恒 🗡️ | Factory Model、Harness 7 组件、Memory vs Knowledge |
| [courses/kaggle-agent/memory/ch03.md](courses/kaggle-agent/memory/ch03.md) | Ch.3 | 三月 🎀 | MCP 协议、NxM 问题、A2A 引入 |
| [courses/kaggle-agent/memory/ch04.md](courses/kaggle-agent/memory/ch04.md) | Ch.4 | 丹恒 🗡️ | A2A 三要素、架构四模式、GOTO Problem |
| [courses/kaggle-agent/memory/ch05.md](courses/kaggle-agent/memory/ch05.md) | Ch.5 | 三月 🎀 | Agent Skills、翻译已知/结晶新知、三层分工 |
| [courses/kaggle-agent/memory/ch06.md](courses/kaggle-agent/memory/ch06.md) | Ch.6 | 丹恒 🗡️ | 7-Pillar Security、Evaluation、生产实践 |

### 课程：agent-tools-interoperability（Agent Tools & Interoperability）

| 记忆文件 | 课次 | 老师 | 核心主题 |
|---------|------|------|---------|
| [courses/agent-tools-interoperability/memory/ch01.md](courses/agent-tools-interoperability/memory/ch01.md) | Ch.1 | 三月 🎀 | MCP 回顾、MCP vs Skills、调试实操 |
| [courses/agent-tools-interoperability/memory/ch02.md](courses/agent-tools-interoperability/memory/ch02.md) | Ch.2 | 丹恒 🗡️ | Contextual Overload、A2A 演进、GOTO |
| [courses/agent-tools-interoperability/memory/ch03.md](courses/agent-tools-interoperability/memory/ch03.md) | Ch.3 | 三月 🎀 | Agent Card、Registry、通信链路 |
| [courses/agent-tools-interoperability/memory/ch04.md](courses/agent-tools-interoperability/memory/ch04.md) | Ch.4 | 丹恒 🗡️ | A2UI、Generative UI、Canvas |
| [courses/agent-tools-interoperability/memory/ch05.md](courses/agent-tools-interoperability/memory/ch05.md) | Ch.5 | 三月 🎀 | AP2/UCP 商业协议、Autonomous Procurement |

## 文件路径规则

每门课程的所有材料都隔离在独立的目录中：

```
teacher/courses/{course_id}/
├── memory/               # 每课记忆（按章节）
├── runtime/              # 运行时记录（progress, session_log, diary 等）
├── story_progression/    # 故事节点
└── config/
    └── knowledge_points/ # 知识点覆盖
```

## 新建课程流程

1. AI 在 `teacher/courses/` 下创建 `{course_id}/` 目录
2. 创建 `memory/`、`runtime/`、`story_progression/`、`config/knowledge_points/` 子目录
3. 初始化 `runtime/progress.md`、`runtime/session_log.md`、`runtime/diary.md`
4. 后续所有课后更新写入该目录下的对应文件
5. 共享系统文件（system_core.md、characters/）保持不变

## 生成规则

- **生成时机**：每课课后更新流程的第 10 步
- **路径**：`teacher/courses/{course_id}/memory/ch{XX}.md`
- **内容来源**：结合 session_log.md + 课堂对话记录
