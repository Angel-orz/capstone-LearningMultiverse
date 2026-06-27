# LearningMultiverse

An immersive Socratic learning system that transforms AI-powered tutoring into a narrative-driven journey. Built for Claude Code.

## Overview

LearningMultiverse is not a traditional e-learning platform. It's a **living virtual world** where you learn by traveling, talking, and discovering — guided by AI characters who teach through the Socratic method rather than lectures.

You step aboard a train traveling through the stars. Two teachers — March (energetic, metaphor-driven) and Dan Heng (precise, minimal) — take turns guiding you. A fellow student, Pom-Pom, learns alongside you. Lessons unfold as conversations, mistakes become teaching tools, and you name the concepts you discover yourself.

---

## How It Works

| Component | What It Does |
|-----------|-------------|
| **`teacher/config/system_core.md`** | Core teaching rules (Socratic method, narrative standards, character voices) |
| **`teacher/characters/`** | Character profiles for March, Dan Heng, and Pom-Pom |
| **`teacher/courses/{course_id}/`** | Per-course files: knowledge points, story progression, runtime logs |
| **`teacher/runtime/`** | Shared runtime state (progress, review queue, WeChat group) |
| **`copilot-instructions.md`** | Startup sequence — loaded each session by Claude Code |

---

## Courses

| Course | Lessons | Status |
|--------|---------|--------|
| **Machine Learning Strategy & Diagnosis** (Andrew Ng's ML Yearning) | 14 | ✅ Complete |
| **AI Agent Engineering** (Kaggle Agent Series) | 6 | ✅ Complete |
| **Agent Tools & Interoperability** | 5 | ✅ Complete |
| **Agent Skills** (Build, Evaluate, Productionize) | 6 | 🔥 Active |

---

## Teaching Philosophy

- **Socratic Method**: Questions over answers. The teacher never tells — they ask until you discover.
- **Narrative Immersion**: Lessons happen inside a story. Prose quality is a first-class requirement.
- **Spaced Repetition**: Built-in review queue with 1/3/7/14-day intervals.
- **Adaptive Difficulty**: 5-tier support gradient (S5 pure Socratic → S1 minimal explanation).
- **Multi-Modal Modes**: Rough mode (fast overview) vs. Detailed mode (deep dive), chosen per course.

---

## Getting Started

1. Open the project in **Claude Code**
2. The system detects if it's your first launch → plays the prologue → guides you through course selection
3. Choose a course and learning mode (rough / detailed)
4. Step aboard the train — your first lesson begins

> **Prerequisites**: Claude Code with file system access.

---

## Project Structure (Simplified)

```
LearningMultiverse/
├── copilot-instructions.md        # Startup entry point
├── teacher/
│   ├── config/                    # Core rules, learner profile
│   ├── characters/                # Teacher personalities
│   ├── courses/                   # Per-course data (knowledge, story, logs)
│   │   ├── ml-yearning/
│   │   ├── kaggle-agent/
│   │   ├── agent-tools-interoperability/
│   │   └── agent-skills/
│   ├── story_progression/         # Generic emotional-stage framework
│   └── runtime/                   # Shared runtime state
├── materials/                     # Textbooks (PDF)
└── Docs/                          # Reference materials
```

---

## Adding a New Course

1. Create `teacher/courses/{course_id}/` with `memory/`, `runtime/`, `story_progression/`, `config/knowledge_points/` subdirectories
2. Add course metadata to `teacher/config/course_catalog.md`
3. Define knowledge points per lesson
4. Write story progression nodes — each chapter as a standalone file
5. Initialize runtime files (progress, session_log, review_queue, diary)

---

## Acknowledgments

Built on the SocraticNovel framework — a methodology combining Socratic teaching with narrative-driven learning. Inspired by Andrew Ng's *Machine Learning Yearning* and the Kaggle Agent Series.
