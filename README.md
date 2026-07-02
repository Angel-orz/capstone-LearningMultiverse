# LearningMultiverse — Socratic Multi-Agent Tutoring System

**AI Agents: Intensive Vibe Coding Capstone Project** | *Freestyle Track*

> A narrative-driven, Socratic tutoring system powered by multiple AI agents. Learn by traveling, talking, and discovering — guided by characters who teach through questions, not lectures.

---

## 📖 My Story

I'm a software engineer who joined the *AI Agents: Intensive Vibe Coding Course* to dive into the latest in AI Agent technology. On the very first day of the course, I built the first version of LearningMultiverse — originally a simple tool to read and interact with the course whitepaper through a conversational interface.

But as the course progressed, something unexpected happened. Each new concept I learned — agents, tools, memory, evaluation, skills — found its way into the project. What started as a reading companion grew into something much more ambitious: a full-fledged multi-agent Socratic tutoring system where two AI teachers (March and Dan Heng) guide you through complex topics using questions, metaphors, and narrative immersion.

This project is the result of that evolution — a living demonstration of the AI Agent concepts I learned throughout the course.

---

## 🚂 What Is LearningMultiverse?

LearningMultiverse transforms AI-powered tutoring from a sterile Q&A exchange into a **narrative-driven journey**. You step aboard a train traveling through the stars. Two teachers — March (energetic, metaphor-driven) and Dan Heng (precise, systematic) — take turns guiding you. A fellow student, Pom-Pom, learns alongside you. Lessons unfold as conversations, mistakes become teaching tools, and you name the concepts you discover yourself.

### The Problem It Solves

Most AI tutoring systems fall into one of two traps:
- **Answer-giving bots**: They tell you the answer, robbing you of the discovery process
- **Dry flashcards**: They test recall without building deep understanding

LearningMultiverse takes a third path: **guided discovery through Socratic dialogue**. It doesn't tell you the answer — it asks you questions until you discover it yourself. The narrative (a train traveling through space, two teachers with distinct personalities, a fellow student) isn't decoration — it's a cognitive framework that makes learning feel like exploration rather than instruction.

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                     copilot-instructions.md                   │
│                    (System Entry Point)                       │
└──────────────────────────┬───────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────┐
│                    Agent Coordination Layer                   │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │    March     │  │   Dan Heng   │  │     Pom-Pom      │  │
│  │  Energetic   │  │   Precise    │  │  Peer Learner    │  │
│  │  Analogy-    │  │  Systematic  │  │  Companion       │  │
│  │  Driven      │  │  Structured  │  │  Perspective     │  │
│  └──────┬───────┘  └──────┬───────┘  └────────┬─────────┘  │
│         │                 │                    │            │
│         └─────────────────┴────────────────────┘            │
│                           │                                 │
│              Socratic Engine (system_core.md)                │
│         Teaching rules, narrative standards,                 │
│         5-tier support gradient (S5→S1)                     │
└──────────────────────────┬───────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────┐
│                         Tools                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Knowledge   │  │    Review    │  │    Story         │  │
│  │  Retrieval   │  │    Queue     │  │    Engine        │  │
│  │  (course     │  │  (spaced     │  │  (narrative      │  │
│  │   content)   │  │  repetition) │  │   progression)   │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
└──────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────┐
│                    Sessions & Memory                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Progress    │  │  Session     │  │    Diary         │  │
│  │  Tracking    │  │  Logs        │  │    (reflection)  │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│  ┌──────────────┐  ┌──────────────┐                          │
│  │  Mistake     │  │  Review      │                          │
│  │  Log         │  │  Queue       │                          │
│  └──────────────┘  └──────────────┘                          │
└──────────────────────────────────────────────────────────────┘
```

---

## 📚 Course Concepts Demonstrated

### 1️⃣ Agent (Multiple Independent Agents)
Each teacher is a distinct AI agent with:
- **A unique personality** defined in `teacher/skills/` skill files
- **A distinct teaching methodology**: March uses analogy and metaphor; Dan Heng uses structure and precision
- **Independent state**: Each agent tracks observations about the learner

### 2️⃣ Multi-Agent System
Agents don't just exist in isolation — they collaborate:
- **Automatic rotation**: March teaches odd-numbered lessons, Dan Heng teaches even-numbered ones
- **Complementary style**: March builds intuitive understanding; Dan Heng reinforces with structure
- **Shared context**: Both agents read the same learner profile, progress, and session logs
- **Pom-Pom as peer learner**: A non-teacher agent who learns alongside you, adding a collaborative dimension

### 3️⃣ MCP / Tools Integration
The system uses tools to enhance teaching:
- **Knowledge Retrieval**: Reads course materials (PDFs, documents) to ground teaching in real curriculum
- **Review Queue**: A spaced-repetition tool scheduling reviews at 1/3/7/14-day intervals
- **WeChat Group Chat**: A simulated group chat tool for post-lesson social interaction
- **Syllabus Source Management**: Tracks where course materials come from (local files, URLs, search results)

### 4️⃣ Skills (Claude Code Skills)
Each teacher is implemented as a **Claude Code Skill**:
- `march.skill.md` — March's teaching persona (analogy-driven, energetic)
- `danheng.skill.md` — Dan Heng's teaching persona (precision, structure)
- `pamm.skill.md` — Pom-Pom's peer-learner persona
- Skills are hot-loaded per session based on which teacher is on duty

### 5️⃣ Sessions / Memory
The system maintains persistent learning state:
- **Progress tracking**: What lessons were completed, by which teacher, on what date
- **Session logs**: Detailed records of each teaching session
- **Learner profile**: Preferences, knowledge gaps, learning patterns
- **Diary**: Post-lesson reflections written from the learner's perspective
- **Spaced repetition memory**: Review schedule optimized for long-term retention

### 6️⃣ Evaluation (Adaptive Assessment)
The system continuously evaluates and adapts:
- **5-tier Support Gradient** (S5→S1): Pure Socratic → Directional hints → Counter-examples → Analogies → Minimal explanation. Drops one level at a time when the learner struggles, rises back immediately when they succeed.
- **6 Learner Types** (E1-E6): The system identifies learner patterns (blank page, overconfident, jumping ahead, frustrated, distracted, questioning) and adjusts strategy accordingly.
- **Self-check mechanism**: Every 5 turns, the system runs a self-check against three core Socratic rules.
- **Mistake log**: All wrong answers are recorded and form the basis for future review.

### ✅ Security & Privacy (Design Philosophy)
The system is designed with **Privacy by Design** as a core principle (see [Security Features](#-security-features) section for details):

- **Local-first architecture**: All learner data (progress, session logs, diary, mistakes) is stored in local files — **never sent to any external server**
- **Environment-based configuration**: API keys and sensitive settings are configured via `.env`, never hardcoded
- **Input validation**: Course names and file paths are validated to prevent injection attacks
- **Profile isolation**: Each learner's data is stored in isolated directories

This isn't a tacked-on feature — it's a fundamental architectural choice. Learning is deeply personal data, and it should stay on your machine.

---

## 🎬 Demo: "What Is an AI Agent?"

Here's a real interaction showing how the multi-agent system works:

### 🚂 Session Start
```
[The train compartment's warm lights flicker on. A whiteboard covers one 
wall. On the left side of the table: a camera, some hair clips, a white 
porcelain teacup. On the right: a neat notebook and a military-green 
thermos. March is already in her seat, flipping through photos on her 
camera. She looks up.]
```

**March:** "Oh! You're here! Good timing — I was just thinking about something. You know how everyone's been talking about 'AI Agents' this whole course?"

**You:** "Yeah, but I'm still not 100% sure I can define it clearly."

**March:** "Perfect! Don't define it yet. Let me ask you something first —"

*She sets down her camera and turns toward you, pulling one knee up onto the seat.*

**March:** "Imagine you're on a train — this train, actually. You have a destination. You have a bag of tools. And along the way, you have to make decisions: Do I get off here? Do I ask someone for directions? Do I use this tool or that one?"

**You:** "OK..."

**March:** "Now — what's the difference between you, a person on a train making decisions, and a rock that's also on the train but just sits there?"

*She grins — she knows she's set up something good.*

**You:** "...One of us is making choices?"

**March:** "**Yes!!** Say it again, I want to hear you say it!"

*She's practically bouncing in her seat.*

---

### 🎭 Teacher Handoff (Next Session — Dan Heng)

```
[The next day. March's teacup is still on the windowsill — clean, upside 
down. A different thermos sits on the opposite side of the table. 
Dan Heng is already there, reading. He doesn't look up immediately.]
```

**Dan Heng:** "March told me you talked about agents yesterday."

*He closes his notebook.*

**Dan Heng:** "She said you got to 'agents make choices.' That's correct. Let's go deeper."

**You:** "OK."

**Dan Heng:** "An AI agent takes in a goal, perceives its environment, uses tools, and decides on actions. The decision loop is what makes it an agent."

*He writes on the whiteboard:*
```
Goal → Perceive → Reason → Act → Observe → Repeat
```

**Dan Heng:** "March gave you the 'why.' I'll give you the 'what.' Now — what part of this loop do you think is the hardest to get right?"

---

## 🧪 Evaluation Cases

| # | Scenario | Test | Expected Outcome |
|---|----------|------|-----------------|
| 1 | **First Launch** | Start a new session with an empty `wechat_group.md` | System detects first launch → plays prologue → prompts course selection → board the train |
| 2 | **Socratic Questioning** | Ask "What is overfitting?" | System doesn't explain — asks probing questions: "Imagine you memorize all the answers to a practice test. What happens when the real test has new questions?" |
| 3 | **Support Gradient** | Give 3 wrong answers in a row on the same concept | System drops one support level (S5→S4) and provides a directional hint. On correct answer, immediately rises back to S5 |
| 4 | **Spaced Repetition** | Complete Lesson 1, start Lesson 2 the next day | System detects review_queue has items due → runs quick review of Lesson 1 before starting Lesson 2 |
| 5 | **Agent Handoff** | Complete an odd-numbered lesson (March), start the next lesson | System switches to Dan Heng — narrative transition shows March's teacup still on the table, Dan Heng's thermos in its place. Teaching style shifts noticeably |
| 6 | **Learner Mode Preference** | Learner sets mode_preference to "direct instruction" in their profile | System overrides default Socratic behavior — now explains concepts directly, only asking confirmation questions afterward |

---

## 🔒 Security Features

### Local-First Architecture (Privacy by Design)
All learner data — progress, session logs, diary entries, mistake logs, review schedules — is stored **entirely in local files**. No data is ever transmitted to external servers. This is a deliberate architectural decision: learning is deeply personal, and your data should stay on your machine.

### Environment-Based Configuration
- All configurable values (API keys, feature flags, paths) are managed through `.env`
- A template (`.env.example`) documents all available options
- `.env` is in `.gitignore` — **never committed to version control**
- Startup validation checks for required environment variables

### Input Validation
- Course names are validated against the course catalog (no arbitrary strings accepted)
- File paths for syllabus sources are sanitized to prevent path traversal
- Any content generated by tools (WebFetch, file reads) is validated before storage

### Data Isolation
- Each learner has an isolated profile in `teacher/config/learner_profile.md`
- Runtime data is stored separately from system configuration
- Personal learning data is never mixed with shared system files

---

## 🗂️ Project Structure

```
LearningMultiverse/
├── copilot-instructions.md        # System entry point (loaded by Claude Code)
├── .env.example                   # Environment configuration template
├── .gitignore                     # Security-aware ignore rules
├── README.md                      # ← This file
│
├── teacher/
│   ├── config/
│   │   ├── system_core.md         # Core rules: Socratic method, narrative, flow
│   │   ├── system_reference.md    # Reference rules (loaded on demand)
│   │   ├── course_catalog.md      # 📚 Available courses
│   │   ├── course_mode.md         # 🎯 Teaching modes (rough / detailed)
│   │   ├── curriculum.md          # Full curriculum structure
│   │   ├── syllabus-source.md     # 📦 Syllabus source tracking
│   │   └── learner_profile.md     # Learner profile & preferences
│   │
│   ├── skills/                    # 📦 Claude Code Skill files (teacher personas)
│   │   ├── march.skill.md         # March — energetic, analogy-driven teacher
│   │   ├── danheng.skill.md       # Dan Heng — precise, systematic teacher
│   │   ├── pamm.skill.md          # Pom-Pom — peer learner companion
│   │   ├── capabilities.md        # Teacher capability registry
│   │   └── nuwa-integration.md    # New teacher creation bridge
│   │
│   ├── prologue.md                # Story prologue (first launch only)
│   ├── story.md                   # Worldbuilding & character settings
│   ├── story_progression/         # Narrative emotional framework
│   │   └── overview.md            # Emotional stages & transition rules
│   │
│   └── memory/                    # Memory archive index
│       └── README.md              # Index & new course instructions
```

---

## 🚀 Getting Started

### Prerequisites
- **Claude Code** (with filesystem access)
- Git (for version control)

### Local Setup

```bash
# 1. Clone the repository
git clone https://github.com/Angel-orz/capstone-LearningMultiverse.git
cd capstone-LearningMultiverse

# 2. Configure environment (optional)
cp .env.example .env
# Edit .env with your preferences

# 3. Launch the system
claude

# 4. First launch automatically:
#    - Plays the prologue (if wechat_group.md is empty)
#    - Prompts you to select available course(s)
#    - Guides you through mode selection (rough / detailed)
#    - Begins your first lesson
```

---

## 🏁 Submission Notes

- **Track**: Freestyle
- **Course**: AI Agents: Intensive Vibe Coding Course (Kaggle × Google, June 2026)
- **Author**: Anqi Yang
- **Role**: Software Engineer & AI Learner

---

## 🙏 Acknowledgments

- Built during the **AI Agents: Intensive Vibe Coding Course** (Kaggle × Google, June 2026)
- Inspired by the Socratic Novel framework — combining Socratic teaching with narrative-driven learning
- Character personas adapted from **Honkai: Star Rail** (March 7th, Dan Heng, Pom-Pom)
- Core teaching methodology draws from **Andrew Ng's Machine Learning Yearning**
