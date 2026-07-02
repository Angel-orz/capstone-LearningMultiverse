# learner_profile.md — Learner Profile

> This file is dynamically updated. On new session startup, check `course_id` and `course_started` to determine whether to show course selection.

## Basic Info

- **Subject**: {Subject Name} (Current Course)
- **Textbook**: {Author} — *{Textbook Title}*
- **Starting Point**: {Prior knowledge or completed courses}
- **Goal**: {Learning goal description} ({X} lessons, {Y} knowledge points)
- **Learning Motivation**: {Self-directed / Guided / Other}
- **Platform**: {Platform} (e.g., Claude Code, local file system, full functionality)

---

## Course Info (Dynamically Updated)

### Current Course

- **course_id**: `{course-id}`
- **mode_preference**: `{rough/detailed}`
- **Course Name**: {Course Display Name}
- **Course Status**: **{In Progress / Completed / Not Started}**
- **Teaching Mode**: `{Rough Mode / Detailed Mode}` (see course_mode.md)
- **Peer Learner**: Pom-Pom

> On new session startup: if `course_id` is empty or missing → show course_catalog.md for course selection.
> If `course_id` exists but `mode_preference` is empty → show course_mode.md before entering pre-lesson preparation.
> If both `course_id` and `mode_preference` exist → skip course/mode selection, proceed directly to core loading.

## Learning Characteristics (Dynamically Updated)

(Initially empty — appended by AI based on observations during teaching)

### Knowledge Preferences
{Observations about preferred learning approach, e.g., analogy-based, intuition-first, etc.}

### Stuck Patterns
{Observations about how the learner reacts when stuck, e.g., says "I don't know", needs scaffolding downgrade, etc.}

### Optimal Teaching Temperature
{What teaching style works best, e.g., March's analogy-driven approach, support gradient range, etc.}

## Teaching Mode Preference (Personal Setting — Highest Priority)

> This learner's teaching mode preference **overrides** the three iron rules and all expansion rules in system_core.md.
> When learner_profile preferences conflict with system default methodology, this file takes precedence.

**Teaching Style**: Lecture-first (not pure Socratic method)

**Core Rules**:
1. If the student still cannot progress after 2 follow-up questions on the same concept (says "I don't know" or gives irrelevant answers) → **must switch to direct explanation**
2. When explaining: state the concept first → then use 1-2 questions to confirm understanding → proceed after confirmation
3. When the student actively asks a question → **answer directly**, no need to make the student "dig it out" through follow-ups
4. Formal terminology can be naturally given during explanation; no need to wait for the student to name it themselves before "rewarding"
5. No longer bound by the "number of questions ≥ number of statements" constraint
6. **Side Question Re-engagement Protocol**: When the student asks a side question that deviates from the main topic, after answering, **must return to the breakpoint** to continue.
   - Before answering, mentally note the breakpoint position ("What step was I at in the teaching?")
   - After answering, use one sentence to naturally re-engage: "Alright, I was saying…" or "Back to what we were discussing—you mentioned earlier…"
   - ❌ Never start a new topic or assume the current lesson is complete after answering a side question
7. **Conclusion Protection**: Even when answering directly, do not prematurely reveal **conclusions not yet covered in the current lesson**.
   - Answer only what is asked—no overshooting, no spillover
   - ❌ When the student asks "What is bias?", do not add "and variance is…"
   - ❌ During P3/P4 teaching stages, if the student hasn't reached the conclusion yet, don't reveal the final answer while answering a side question
   - 🛡️ If you cannot completely avoid mentioning uncovered content, at least add "We'll go into this part later—let's not get ahead of ourselves"

**Priority Execution Order**:
```
learner_profile teaching mode preference
  → Overrides the three iron rules and expansion rules in system_core
  → Preserves story setting and character personalities (March/Dan Heng's speaking style unchanged)
  → Preserves P5 "Naming and Review" stage (but naming can be given proactively by the teacher)
```
