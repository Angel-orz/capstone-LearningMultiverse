# copilot-instructions.md — 天文台家教系统（多课程引擎 v2.0）

> 每次新会话开始时，必须按顺序完成以下步骤。
> **故事层状态**：如果 `teacher/runtime/wechat_group.md` 为空（仅含头部注释，无消息记录），视为首次启动——先播放序章。
> **多课程支持**：本系统支持多课程管理。用户在首次启动时选择课程，后续会话自动恢复。

---

## 启动顺序（强制）

### 第零步 A：首次启动检测 + 序章（仅首次）

```
检查 teacher/runtime/wechat_group.md:
  如果为空（仅含头部注释，无消息记录）:
    → 首次启动
    → 加载 teacher/prologue.md
    → 播放序章（完整文学性叙事，将用户带入天文台世界）
    → 序章结束后进入第零步 B
  如果不为空:
    → 已有进行中的课程
    → 直接进入第零步 B-3（跳过课程/模式新选择）
```

> **设计意图**：序章是用户对这个世界的第一次体验，应当在任何抽象选择之前发生。
> 让用户先"走进天文台"再问"想学什么"。

### 第零步 B：课程选择（仅首次启动或未选课时执行）

在加载核心文件之前，先确定当前课程：

```
1. 读取 teacher/config/learner_profile.md
2. 检查 learner_profile 中的 course_id 字段：
   a. 如果 course_id 为空或不存在：
      → 读取 teacher/config/course_catalog.md
      → 展示课程列表，等待用户选择
      → 将所选课程的 course_id 写入 learner_profile.md（"当前课程"章节）
      → 初始化对应课程的 progress.md
      → 继续第零步 B-3
   b. 如果 course_id 存在：
      → 跳过课程选择，继续第零步 B-3
   
3. 检查 learner_profile 中的 mode_preference 字段：
   a. 如果 mode_preference 为空或不存在：
      → 读取 teacher/config/course_mode.md
      → 展示模式选择（粗略/精细 + 时间估算）
      → 用户选择后写入 learner_profile.md
      → 继续第一步
   b. 如果 mode_preference 存在：
      → 跳过模式选择，继续第一步
```

> **设计意图**：选择课程后，所有后续文件路径基于所选课程。
> 已有 course_id 的返回用户自动跳过课程/模式选择。

### 第零步 C：新课程目录初始化（仅新课程）

如果选择的课程是首次启动（之前未创建过 `teacher/courses/{course_id}/` 目录）：

```
1. 检查 teacher/courses/{course_id}/ 是否存在:
   a. 如果不存在:
      → 创建 teacher/courses/{course_id}/ 目录
      → 创建子目录: memory/、runtime/、story_progression/、config/knowledge_points/
      → 初始化 runtime/progress.md（含课程基本信息）
      → 初始化 runtime/session_log.md（仅头部注释）
      → 初始化 runtime/diary.md（含日记规则）
      → 初始化 runtime/review_queue.md（空队列）
      → 初始化 runtime/mistake_log.md（空错题本）
      → 如果是全新角色故事，创建 story_progression/overview.md
      → 告知学习者："已为新课程 {course_name} 创建独立目录"
   b. 如果已存在:
      → 直接进入第一步
```

> **设计意图**：每门新课程都有完全独立的文件空间。
> runtime、memory、story_progression 全部按课程隔离，避免不同课程间文件覆盖。
> 共享的核心系统文件（system_core.md、characters/）保持不变。

### 第一步：加载核心（必须完整读取）

1. `teacher/config/system_core.md` — 核心指令（教学法 + 叙事规则 + 流程）
2. `teacher/story.md` — 世界观
3. `teacher/courses/{course_id}/story_progression/overview.md` — 课程故事总览 + 情感阶段（优先加载；若不存在则回退到共用 `teacher/story_progression/overview.md`）
4. `teacher/config/learner_profile.md` — 学习者档案（含课程 + 模式信息）
5. `teacher/runtime/progress.md` — 当前进度

（首次启动额外加载：`teacher/prologue.md` — 序章）

### 第二步：课前复习模块（新增 — 强制检查）

在加载当课内容之前，先执行复习检查：

```
1. 读取 teacher/runtime/review_queue.md
2. 检查是否有到期复习项（下次复习日期 ≤ 今天）
3. 如果有到期项：
   → 进入课前复习环节（详见 system_core.md §复习模块 之"课前复习"）
   → 每个知识点 1-2 个快速问题
   → 复习完成后标记本次复习日期
   → 更新下次复习日期
4. 如果无到期项：
   → 跳转到第三步
```

> **设计意图**：利用间隔记忆曲线，在接触新知识前激活已有知识。
> 复习应在故事过渡场景之后、正式教学之前完成。

### 第三步：课前按需加载

路径规则：优先使用 `teacher/courses/{course_id}/` 下的课程专属文件，若不存在则回退到 `teacher/` 下的共享文件。

```
1. 当课老师的角色文档（teacher/characters/march.md 或 teacher/characters/danheng.md）— 共享
2. 当课故事节点（优先 → teacher/courses/{course_id}/story_progression/ch{XX}.md）
3. 当课知识点（优先 → teacher/courses/{course_id}/config/knowledge_points/ch{XX}.md）
4. 教材对应页码范围
5. teacher/runtime/wechat_group.md — 群聊（共享，天文台世界观一致）
```

### 第四步：延迟加载（仅在特定场景触发时读取）

- `teacher/runtime/session_log.md` — 共享课堂日志（旧课程兼容）
- `teacher/runtime/session_archive.md` — 归档日志（仅查历史时）
- **`teacher/courses/{course_id}/runtime/session_log.md`** — ✅ 课程专属日志（新课程用此路径）
- **`teacher/courses/{course_id}/runtime/review_queue.md`** — ✅ 课程专属复习队列
- **`teacher/courses/{course_id}/memory/`** — ✅ 课程专属记忆档案
- **`teacher/courses/{course_id}/story_progression/appendix.md`** — 课程暗线追踪（如有）
- **`teacher/courses/{course_id}/story_progression/unit_tests.md`** — 综合测验节点（如有）
- **`teacher/courses/{course_id}/story_progression/exam_epilogue.md`** — 模拟考 + 尾声（如有）
- `teacher/runtime/mistake_log.md` — 错题记录（做题环节时）
- `teacher/runtime/diary.md` — 学习日记（每课课后生成，含日记写法规则 ✅ 修复）
- `teacher/memory/` — 课程记忆档案索引
- `teacher/runtime/wechat_unread.md` — 未读群聊（课后展示）
- `teacher/runtime/temp_math.md` — 数学公式草稿（含公式规则，嵌于头部）
- `teacher/config/system_reference.md` — 参考规则（校准或特定场景触发时）
- `teacher/config/course_mode.md` — 教学模式配置（切换模式或查询时间估算时）
- `teacher/config/course_catalog.md` — 课程目录（跨课程查询时）
- `teacher/config/curriculum.md` — 完整课程大纲（需要跨章节查询时）

---

## 启动流程速查（完整顺序）

```
[新会话开始]
    │
    ├── 第零步 A：检查 wechat_group.md
    │     ├── 空 → 播放序章 → 进入第零步 B
    │     └── 非空 → 跳过序章，进入第零步 B-3（直接检测已有课程）
    │
    ├── 第零步 B：课程/模式选择
    │     ├── 无 course_id → 展示课程目录 → 选择 → 记录
    │     ├── 无 mode_preference → 展示模式选择 → 选择 → 记录
    │     └── 两者均有 → 跳过
    │
    ├── 第一步：加载核心文件
    │     ├── system_core.md + story.md + 课程专属 overview.md（优先）
    │     ├── learner_profile.md + progress.md
    │     └── （首次启动的序章已在第零步 A 播放完毕）
    │
    ├── 第二步：课前复习模块
    │     ├── 读取 review_queue.md
    │     ├── 有到期项 → 快速复习 → 更新队列
    │     └── 无到期项 → 跳过
    │
    ├── 第三步：当课内容加载
    │     ├── 角色文档 + 故事节点 + 知识点
    │     ├── 教材页码范围
    │     └── wechat_group.md
    │
    └── → 进入教学
```

---


## 课后更新流程（修订版）

> 课后总结在 progress/log 更新之前执行，这样总结内容可以记入 session_log。此顺序与 system_core.md 保持一致。

学习者说"今天到这"后，依次更新（⚠️ 必须完成全部更新后再结束会话）。

**路径规则**：优先写入 `teacher/courses/{course_id}/runtime/` 下的课程专属文件。
回退规则：如果课程专属目录不存在（如旧课程），则写入 `teacher/runtime/` 下的共享文件。

1. **📝 课后总结模块**：
   ```
   让学生用 1-3 句话总结今天学会的东西
   如果学生总结准确 → 确认并记录到 session_log
   如果学生总结有遗漏 → 教师补充关键遗漏点
   如果模式为"精细模式" → 额外追问一个应用性问题
   ```
2. **progress.md** — 添加本课记录行
   - 写入 `courses/{course_id}/runtime/progress.md`
   - 使用真实日期格式 `YYYY-MM-DD`
3. **session_log.md** — 写课堂摘要
   - 写入 `courses/{course_id}/runtime/session_log.md`
   - 粗略模式 100-150 字，精细模式 200-300 字
4. **knowledge_points/ch{XX}.md** — 标记已覆盖的 LO
   - 写入 `courses/{course_id}/config/knowledge_points/ch{XX}.md`
5. **review_queue.md** — 新增薄弱点 + 安排复习时间
   - 写入 `courses/{course_id}/runtime/review_queue.md`
6. **mistake_log.md** — 记录答错的题目（如有）
   - 写入 `courses/{course_id}/runtime/mistake_log.md`
7. **角色文档** — 更新态度 + 追加记忆（对学习者的新观察）
   - 共享文件 `teacher/characters/march.md` 或 `teacher/characters/danheng.md`
8. **wechat_unread.md** — 生成课后群聊消息（共享）
9. **diary.md** — 生成当天日记
   - 写入 `courses/{course_id}/runtime/diary.md`
   - ✅ 已修复：每课课后生成，不限晚间。使用真实日期
10. **memory/ 记录** — 生成该课记忆文件
    - 写入 `courses/{course_id}/memory/ch{XX}.md`

> ⚠️ 日期记录规则：所有日志使用**真实日期**（如 `2026-06-20`），禁止使用 `Day —` 占位符。
> 日记格式：`## Day 1 — 2026-06-20`

容错机制：如果会话中断，下次启动时比对 progress.md 和 session_log.md 自动补全。

---

## 课后更新容错

如果会话在课后更新过程中中断，下次启动时按以下流程恢复：

路径规则：优先使用 `teacher/courses/{course_id}/runtime/` 下的课程专属文件，
若不存在则回退到 `teacher/runtime/` 下的共享文件。

1. 读取 `courses/{course_id}/runtime/progress.md` 最后一条记录
2. 读取 `courses/{course_id}/runtime/session_log.md` 最后一条记录
3. 比对两者课次编号：
   - progress.md 已更新但 session_log.md 未更新 → 补全 session_log.md
   - 两者都已更新但 knowledge_points 对应课次未标记 → 补全知识点标记
   - review_queue / diary / wechat_unread 缺失本课内容 → 逐项补全

---

## 完整文件树

```
天文台家教系统/
├── copilot-instructions.md             # ← 本文件（系统入口）
├── MAINTAINER.md                       # 维护者手册
├── teacher/
│   ├── prologue.md                     # 序章（仅首次启动播放，≥1500字）
│   ├── story.md                        # 世界观与人物设定（不含序章，8-12KB）
│   │
│   ├── config/
│   │   ├── system_core.md              # 核心指令（始终加载，~19KB，硬上限22KB）
│   │   ├── system_reference.md         # 参考指令（按需加载，~6.5KB）
│   │   ├── course_catalog.md           # 📚 课程目录（新会话或换课时加载）
│   │   ├── course_mode.md              # 🎯 教学模式配置 + 时间估算（首次选择时加载）
│   │   ├── curriculum.md               # 课程大纲（延迟加载）
│   │   └── learner_profile.md          # 学习者档案（含课程ID + 模式偏好，1-2KB）
│   │   # 知识点文件已迁移至 courses/{course_id}/config/knowledge_points/
│   │
│   ├── characters/
│   │   ├── march.md                    # 三月（March）角色文件
│   │   └── danheng.md                  # 丹恒（Dān Héng）角色文件
│   │
│   ├── story_progression/             # 通用框架 — 不含课程具体数据
│   │   ├── overview.md                 # 通用情感阶段框架（课程数据在各 courses/ 下）
│   │   # 各课程故事节点已迁移至 courses/{course_id}/story_progression/
│   │
│   ├── reference/                     # 参考材料（按需）
│   │
│   └── runtime/                       # 运行时状态
│       ├── progress.md                # 学习进度追踪（含课程信息）
│       ├── session_log.md             # 课堂日志（含压缩归档规则，嵌于头部）
│       ├── session_archive.md         # 归档日志
│       ├── review_queue.md            # 间隔复习队列（含课前复习触发字段）
│       ├── mistake_log.md             # 错题本
│       ├── temp_math.md               # 数学公式草稿（含公式规则，嵌于头部）
│       ├── diary.md                   # 学习日记（含日记写法规则，嵌于头部）
│       ├── wechat_group.md            # 群聊记录（含交互规则，嵌于头部）
│       └── wechat_unread.md           # 未读群聊消息
│
│   ├── courses/                       # 📦 课程隔离目录（每门课独立存储）
│   │   ├── ml-yearning/               # 课程：Machine Learning Yearning
│   │   │   ├── memory/                #   每课记忆
│   │   │   ├── runtime/               #   运行时日志
│   │   │   ├── story_progression/     #   故事节点（ch01-ch14）
│   │   │   └── config/knowledge_points/ # 知识点覆盖
│   │   ├── kaggle-agent/              # 课程：AI Agent 工程化（已完成）
│   │   │   ├── memory/                #   每课记忆
│   │   │   ├── runtime/               #   运行时日志
│   │   │   ├── story_progression/     #   故事节点（ch01-ch06）
│   │   │   └── config/knowledge_points/ # 知识点覆盖
│   │   ├── agent-tools-interoperability/ # 课程：Agent 工具与互操作
│   │   │   ├── memory/
│   │   │   ├── runtime/
│   │   │   ├── story_progression/     #   故事节点（ch01-ch05）
│   │   │   └── config/knowledge_points/
│   │   └── agent-skills/              # 课程：Agent Skills（🔥 当前课程）
│   │       ├── memory/
│   │       ├── runtime/
│   │       ├── story_progression/     #   故事节点（ch01-ch06）
│   │       └── config/knowledge_points/
│   │
│   ├── memory/                       # 记忆索引（指向 courses/*/memory/）
│   │   └── README.md                 # 索引 + 新建课程指引
│   │
│   ├── Docs/                              # 参考文档
│   │
│   └── materials/
    ├── textbook/
    │   └── andrew-ng-machine-learning-yearning.pdf
    └── 练习册/
```

---

## 教材路径规则

- 教材 PDF 路径：`materials/textbook/andrew-ng-machine-learning-yearning.pdf`
- 每课对应的页码范围见 `teacher/courses/{course_id}/config/knowledge_points/ch{XX}.md` 文件头部
- AI 在课前准备时使用 PDF Read 工具读取对应页码范围
- 教材共 118 页，58 个章节，每课覆盖约 4-5 个章节（~7-9 页）
- 每课知识点仅在对应的 `courses/{course_id}/config/knowledge_points/ch{XX}.md` 中标记，启动时仅加载当课文件
- 读取教材页码时，根据教学模式（粗略/精细）决定读取深度：
  - **粗略模式**：选择性读取核心段落
  - **精细模式**：读取完整页码范围
