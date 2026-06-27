# MAINTAINER.md — 天文台家教系统 · 维护者手册 v2.0

> 本文件帮助维护者理解和维护整个系统。如果你需要修改任何文件，请先阅读本文。
> **v2.0 更新**：新增多课程支持、教学模式选择、复习模块、三月角色重写。

---

## 系统架构概览

```
学习者 ←→ Claude Code（运行时 AI）
              │
              ├── copilot-instructions.md（入口——AI 启动时自动读取）
              │     新增：第零步课程选择、课前复习模块、课后总结
              │
              ├── teacher/config/system_core.md（核心引擎——始终加载）
              │     ├── §0 教学模式灵活性 + 多课程引用
              │     ├── §1 苏格拉底教学法（ML 学科适配版）
              │     ├── §2 叙事规则
              │     ├── §3 角色声音速查（三月✨重写为 HSR 活泼风格）
              │     ├── 完整上课流程（P0-P5 + 模式感知 + 课前复习 + 课后更新 + 课后总结）
              │     ├── 复习模块（课前复习 + 课后总结）
              │     ├── 做题系统 / 轮值
              │     └── 防漂移机制
              │
              ├── teacher/config/system_reference.md（参考引擎——按需加载）
              │
              ├── teacher/config/course_catalog.md        ← 📚 新增——课程目录（多课程入口）
              ├── teacher/config/course_mode.md           ← 🎯 新增——教学模式 + 时间估算
              │
              └── teacher/config/knowledge_points/        ← 知识点覆盖（按课次拆分）
```

## 文件职责速查（v2.0 更新版）

| 文件 | 职责 | 加载时机 | 修改频率 |
|------|------|---------|---------|
| `copilot-instructions.md` | 启动顺序 + 课程选择 + 复习模块 | 新会话自动 | 添加课程或调整流程时 |
| `system_core.md` | 教学法 + 叙事 + 流程 + 复习模块 | 始终 | 教学规则调整时 |
| `system_reference.md` | 参考规则完整版 | 校准/特定场景 | 补充细节时 |
| **`course_catalog.md`** | **📚 课程目录** | **新会话/切换课程** | **添加新课程时** |
| **`course_mode.md`** | **🎯 教学模式定义 + 时间估算** | **首次选择或查询时** | **调整模式参数时** |
| `prologue.md` | 序章（文笔标杆） | 仅首次启动 | 几乎不改 |
| `story.md` | 世界观 | 始终 | 世界观扩展时 |
| `story_progression/*.md` | 故事节点 | 当课加载 | 调整故事方向时 |
| `characters/march.md` | 三月角色 **✨ HSR 风格重写** | 三月当课时 | 角色发展时追加 |
| `characters/danheng.md` | 丹恒角色 | 丹恒当课时 | 角色发展时追加 |
| `curriculum.md` | 课程大纲 | 跨章节查询时 | 教材更新时 |
| `knowledge_points/*.md` | 知识点清单（含课程ID） | 当课加载 | 课后标记 |
| `learner_profile.md` | 学习者档案 **新增：课程ID + 模式偏好** | 始终 | 课程选择/模式选择时 |
| `runtime/progress.md` | 进度追踪 **新增：课程信息 + 模式字段** | 始终 | 每课更新 |
| `runtime/session_log.md` | 课堂日志（含课后总结记录） | 课后更新 | 每课追加 |
| `runtime/review_queue.md` | 复习队列 **新增：课程ID字段** | 课前复习模块 | 每课可能追加 |
| `runtime/mistake_log.md` | 错题本 | 做题时 | 有错即记 |
| `runtime/wechat_group.md` | 群聊记录 | 启动时检测 | 课后追加 |
| `runtime/wechat_unread.md` | 未读群聊 | 课后生成/展示 | 每课生成 |
| `runtime/diary.md` | 学习日记 | 晚间课后 | 每天生成 |
| `runtime/temp_math.md` | 公式草稿 | 写公式时 | 教学过程中 |
| `MAINTAINER.md` | **本文件（已更新 v2.0）** | 维护时 | 系统更新时 |
| `courses/{course_id}/runtime/` | **📦 课程专属运行时（progress/session_log/diary）** | 每课课后更新 | 每次课后 |
| `courses/{course_id}/memory/` | **📦 课程专属记忆档案** | 课后/复习时 | 每次课后追加 |
| `courses/{course_id}/story_progression/` | **📦 课程专属故事节点** | 当课加载 | 每课设计时 |
| `courses/{course_id}/config/knowledge_points/` | **📦 课程专属知识点覆盖** | 当课加载/课后更新 | 每课标记 |

---

## v2.0 变更记录（2026-06-18）

### 1. ✨ 三月角色重写
- **文件**：`teacher/characters/march.md`、`teacher/story.md`、`teacher/config/system_core.md §3`
- **变更**：依据《崩坏：星穹铁道》三月七的性格特征，全面升级为活泼、热情、话多、好奇的"天文台阳光担当"
- **保留要素**：暗线背景、核心矛盾、教学风格、与丹恒的关系
- **强化要素**：语速更快、感叹号更多、自我打断、类比爆炸式输出、对学生认可更外放

### 2. 📚 多课程支持
- **新增文件**：`teacher/config/course_catalog.md`
- **修改文件**：`copilot-instructions.md`（新增第零步——课程选择流程）
- **修改文件**：`teacher/config/learner_profile.md`（新增 `course_id` 字段）
- **设计原则**：后续添加课程只需在 `course_catalog.md` 中注册，并创建对应知识点和故事节点
- **扩展路径**：新课程的知识点文件可放在 `knowledge_points/{course_id}/` 目录下

### 3. 🎯 教学模式（粗略/精细）+ 时间估算
- **新增文件**：`teacher/config/course_mode.md`
- **修改文件**：`teacher/config/system_core.md`（课前准备 + 课后更新 + P0 设计均受模式影响）
- **时间估算**：粗略模式 ≈ 3 分钟/页，精细模式 ≈ 5-7 分钟/页
- **选择时机**：课程开始时选择，同一课程内保持模式一致

### 4. 🔄 复习模块（课前复习 + 课后总结）
- **新增**：系统化的复习模块，包含间隔复习、课前激活、课后巩固
- **修改文件**：`teacher/config/system_core.md`（新增完整"复习模块"章节）
- **修改文件**：`teacher/runtime/review_queue.md`（新增课程ID字段）
- **修改文件**：`copilot-instructions.md`（第二步——课前复习模块）

---

## v2.1 课程隔离修复（2026-06-20）

### 背景

课程 ml-yearning 和 kaggle-agent 的运行时文件、故事节点混在共享目录 `teacher/runtime/` 和 `teacher/story_progression/` 下，
新增课程时容易覆盖旧课程数据，且 diary.md 因"仅晚间课后"条件限制从未生成。

### 修复内容

1. **创建 `teacher/courses/` 课程隔离目录**
   - 每门课程拥有独立的 `memory/`、`runtime/`、`story_progression/`、`config/knowledge_points/`
   - 旧课程数据已迁入对应目录（共享文件保留不动，以保持兼容）
   
2. **日记修复**
   - 取消"仅晚间课后"限制 → 改为每课课后生成
   - 所有日志使用真实日期（`YYYY-MM-DD`），禁止 `Day —` 占位符

3. **新建课程流程**
   - 第零步 C：新课程自动创建课程隔离目录
   - 课后更新流程所有步骤指向 `courses/{course_id}/` 路径

### 新增文件

| 文件 | 说明 |
|------|------|
| `teacher/courses/ml-yearning/` | ML Yearning 课程专属目录 |
| `teacher/courses/kaggle-agent/` | Kaggle Agent 课程专属目录 |
| `teacher/memory/README.md` | 记忆档案索引 + 新建课程指引 |

### 修改文件

- `teacher/runtime/diary.md` — 日记生成条件（仅晚间→每课课后）
- `teacher/runtime/progress.md` — 添加日期记录规则
- `teacher/config/system_core.md` — 课后更新第 9-10 步
- `copilot-instructions.md` — 第零步 C 新课程初始化、第三步路径规则、课后更新路径、文件树

---

## 关键设计决策

### 为什么是 2 位老师而非 1 或 3？
- 1 位：教学多样性不足，一周密集学习容易单调
- 3 位：轮值复杂度过高，14 课的短周期不需要 3 人
- 2 位：三月（暖/类比/好奇/活力）与丹恒（冷/结构/精准）形成天然互补，交替保持新鲜感

### 为什么暗线爆发安排在 Ch.11-12 而非更早？
- 初期（Ch.1-4）需要建立教学信任——暗线太早会抢教学
- 中期（Ch.5-8）是碎片渗出的最佳窗口——不经意、不完整
- 后期（Ch.9-12）信任已建立，暗线爆发不会淹没教学
- Ch.13-14 留给收束——爆发后需要余韵

### 为什么用 Machine Learning Yearning 这本教材？
- 58 章短小精悍，完美适配 14 课的拆分
- 偏重策略和诊断而非公式推导——适合苏格拉底追问
- 教材的"诊断→决策"框架与丹恒的工程思维天然匹配

### 为什么增加教学模式（粗略/精细）？
- 用户反馈：当前教学内容过于精简，删除过多课件内容
- 精细模式覆盖教材中更多内容，保留用户的自主选择权
- 时间估算帮助用户规划学习周期

### 为什么增加课前复习模块？
- 间隔记忆曲线需要主动激活才能最大化保留
- 复习在新课开始前执行，不打断教学节奏
- 快速提问即可激活记忆，不需要重新教学

---

## 常见维护操作

### 添加新课程

1. 在 `course_catalog.md` 的课程列表中添加新行，补充章节信息
2. 在 `knowledge_points/` 下创建新目录 `{course_id}/`，包含每课的知识点文件
3. 在 `story_progression/` 下创建新目录 `{course_id}/`，包含每课的故事节点
4. 更新 `learner_profile.md` 中的默认课程信息（或让用户在首次启动时自行选择）

### 调整课程模式参数

1. 编辑 `teacher/config/course_mode.md`：
   - 修改"每页分钟数"参数（粗略/精细）
   - 修改速查表的对应估算时间
   - 调整 P0-P5 模式差异的详细规则

### 修改课程进度
1. 更新 `curriculum.md` 中的课程全景表
2. 更新 `story_progression/overview.md` 中的轮值表
3. 更新对应 `knowledge_points/ch{XX}.md` 的教材页码范围

### 调整角色暗线
1. 修改角色文件中的"过往信息碎片"和"暗线种子素材"
2. 更新 `story_progression/appendix.md` 中的回收计划
3. 检查受影响章节的暗线密度是否仍符合密度矩阵

### 添加新的教学规则
1. 判断频率：每轮都需要 → `system_core.md`；特定场景 → `system_reference.md`
2. 如果加入 system_core.md 后超过 22KB，将低频规则移入 system_reference.md
3. 更新 `system_core.md` 末尾的"参考规则加载指引"

### 冷启动测试（v2.0 更新）
在新会话中：
1. 发送项目文件夹路径给 Claude Code
2. 观察 AI 是否按 copilot-instructions.md 的加载顺序执行：
   - 第零步：检查 course_id → 无 → 展示课程目录 → 选择 → 记录
   - 第零步：检查 mode_preference → 无 → 展示模式选择 → 选择 → 记录
   - 第一步：加载核心文件
   - 第二步：课前复习模块（检查 review_queue）
   - 第三步：加载当课内容
3. 首次启动检测 wechat_group.md 为空 → 播放序章
4. 课后检查：是否执行了课后总结模块

### Context 预算监控（v2.0）

新增加的文件：
- `course_catalog.md` ≈ 2KB（仅首次加载）
- `course_mode.md` ≈ 3KB（仅选择时加载）

不影响核心启动预算。核心加载预算维持 ~53KB（目标 ≤ 55KB ✅）。

```
核心加载（始终）：
  system_core.md (~24KB) + story.md (~7KB)
  + overview.md (~3KB) + learner_profile.md (~2KB)
  + progress.md (~1KB) = ~37KB

课前加载（当课）：
  + 角色文件 (~12KB) + story_progression (~3KB)
  + knowledge_points (~1KB) + review_queue (~1KB)
  + wechat_group (~2KB) = ~19KB

课前总计 ≈ 56KB（含新模式信息，接近 55KB 目标 ✅）
```

---

## 🚧 已知待改进项

- [ ] system_core.md 略超 22KB 硬上限（~24KB）。后续可考虑将教学示范移到 system_reference.md
- [ ] 角色文件的"对学习者的关系"段落初始为空——需要在教学过程中由 AI 追加
- [ ] 无配套练习册——所有练习通过苏格拉底追问和随堂做题完成
- [ ] 温度计（群聊温度变化）依赖 AI 对情感阶段的判断——后期可加入自动化检测
- [ ] **新增**：多课程支持目前仅配置了 `ml-yearning` 一门课，添加新课程时需创建配套文件
- [ ] **新增**：复习模块的自动提醒功能——目前依赖 AI 在课前准备时检查 review_queue，可考虑增加推送通知
- [ ] **新增**：课程 mode_preference 目前不支持中途切换——如需切换需清除进度重新开始
