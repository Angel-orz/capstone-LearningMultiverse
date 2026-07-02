# Memory Archive

> This folder is the memory index.
> **Memory files for each lesson are now isolated per course, stored under `courses/{course_id}/memory/`.**
> When creating a new course, memory files are automatically written to the corresponding course-specific directory.

## Index

### Course: ml-yearning (Andrew Ng — Machine Learning Yearning)

| Memory File | Lesson | Teacher | Core Topic |
|---------|------|------|---------|
| [courses/ml-yearning/memory/ch01.md](courses/ml-yearning/memory/ch01.md) | Ch.1 | March 🎀 | Training/test set split, early stopping, overfitting intuition |

### Course: kaggle-agent (AI Agent Engineering — Kaggle Series)

| Memory File | Lesson | Teacher | Core Topic |
|---------|------|------|---------|
| [courses/kaggle-agent/memory/ch01.md](courses/kaggle-agent/memory/ch01.md) | Ch.1 | March 🎀 | Vibe Coding Spectrum, Context Engineering, Factory Model Introduction |
| [courses/kaggle-agent/memory/ch02.md](courses/kaggle-agent/memory/ch02.md) | Ch.2 | Dan Heng 🗡️ | Factory Model, Harness 7 Components, Memory vs Knowledge |
| [courses/kaggle-agent/memory/ch03.md](courses/kaggle-agent/memory/ch03.md) | Ch.3 | March 🎀 | MCP Protocol, NxM Problem, A2A Introduction |
| [courses/kaggle-agent/memory/ch04.md](courses/kaggle-agent/memory/ch04.md) | Ch.4 | Dan Heng 🗡️ | A2A Three Elements, Architecture Four Patterns, GOTO Problem |
| [courses/kaggle-agent/memory/ch05.md](courses/kaggle-agent/memory/ch05.md) | Ch.5 | March 🎀 | Agent Skills, Translating Known/Crystallizing New Knowledge, Three-Layer Division of Labor |
| [courses/kaggle-agent/memory/ch06.md](courses/kaggle-agent/memory/ch06.md) | Ch.6 | Dan Heng 🗡️ | 7-Pillar Security, Evaluation, Production Practice |

### Course: agent-tools-interoperability (Agent Tools & Interoperability)

| Memory File | Lesson | Teacher | Core Topic |
|---------|------|------|---------|
| [courses/agent-tools-interoperability/memory/ch01.md](courses/agent-tools-interoperability/memory/ch01.md) | Ch.1 | March 🎀 | MCP Review, MCP vs Skills, Debugging Practice |
| [courses/agent-tools-interoperability/memory/ch02.md](courses/agent-tools-interoperability/memory/ch02.md) | Ch.2 | Dan Heng 🗡️ | Contextual Overload, A2A Evolution, GOTO |
| [courses/agent-tools-interoperability/memory/ch03.md](courses/agent-tools-interoperability/memory/ch03.md) | Ch.3 | March 🎀 | Agent Card, Registry, Communication Links |
| [courses/agent-tools-interoperability/memory/ch04.md](courses/agent-tools-interoperability/memory/ch04.md) | Ch.4 | Dan Heng 🗡️ | A2UI, Generative UI, Canvas |
| [courses/agent-tools-interoperability/memory/ch05.md](courses/agent-tools-interoperability/memory/ch05.md) | Ch.5 | March 🎀 | AP2/UCP Business Protocols, Autonomous Procurement |

## File Path Rules

All materials for each course are isolated in their own directory:

```
teacher/courses/{course_id}/
├── memory/               # Per-lesson memory (by chapter)
├── runtime/              # Runtime records (progress, session_log, diary, etc.)
├── story_progression/    # Story nodes
└── config/
    └── knowledge_points/ # Knowledge point coverage
```

## New Course Workflow

1. AI creates `{course_id}/` directory under `teacher/courses/`
2. Create subdirectories: `memory/`, `runtime/`, `story_progression/`, `config/knowledge_points/`
3. Initialize `runtime/progress.md`, `runtime/session_log.md`, `runtime/diary.md`
4. All subsequent post-lesson updates are written to the corresponding files in this directory
5. Shared system files (system_core.md, characters/) remain unchanged

## Generation Rules

- **Generation Timing**: Step 10 of the post-lesson update workflow
- **Path**: `teacher/courses/{course_id}/memory/ch{XX}.md`
- **Content Source**: Combined session_log.md + classroom conversation records
