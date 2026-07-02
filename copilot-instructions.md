# copilot-instructions.md — Astral Express Tutoring System (Multi-Course Engine v2.0)

> At the start of each new session, the following steps must be completed in order.
> **Story Layer State**: If `teacher/runtime/wechat_group.md` is empty (only header comments, no message records), treat as first launch — play the prologue first.
> **Multi-Course Support**: This system supports multi-course management. The user selects a course on first launch, and subsequent sessions resume automatically.

---

## Startup Sequence (Mandatory)

### Step Zero A: First Launch Detection + Prologue (First Launch Only)

```
Check teacher/runtime/wechat_group.md:
  If empty (only header comments, no message records):
    → First launch
    → Load teacher/prologue.md
    → Play prologue (full literary narrative, immerse the user in the Astral Express world)
    → After prologue ends, proceed to Step Zero B
  If not empty:
    → Existing course in progress
    → Skip directly to Step Zero B-3 (skip course/mode selection)
```

> **Design Intent**: The prologue is the user's first experience of this world, and should happen before any abstract choices.
> Let the user "step onto the train" first, then ask "what would you like to learn."

### Step Zero B: Course Selection (First Launch or No Course Selected Only)

Before loading core files, determine the current course:

```
1. Read teacher/config/learner_profile.md
2. Check the course_id field in learner_profile:
   a. If course_id is empty or does not exist:
      → Read teacher/config/course_catalog.md
      → Display course list, wait for user selection
      → Write the selected course's course_id into learner_profile.md (under "Current Course" section)
      → Set mode_preference to empty (new course requires re-selecting teaching mode)
      → Initialize the corresponding course's progress.md
      → Continue to Step Zero B-3
   b. If course_id exists:
      → Skip course selection, continue to Step Zero B-3
   
3. Check the mode_preference field in learner_profile:
   a. If mode_preference is empty or does not exist:
      → Read teacher/config/course_mode.md
      → Display mode selection (Rough/Detailed + time estimate)
      → After user selection, write to learner_profile.md
      → Continue to Step One
   b. If mode_preference exists:
      → Skip mode selection, continue to Step One
```

> **Design Intent**: After selecting a course, all subsequent file paths are based on the selected course.
> Returning users with an existing course_id automatically skip course/mode selection.

### Step Zero C: New Course Directory Initialization (New Courses Only)

If the selected course is being launched for the first time (no `teacher/courses/{course_id}/` directory previously created):

```
1. Check if teacher/courses/{course_id}/ exists:
   a. If it does not exist:
      → Create teacher/courses/{course_id}/ directory
      → Create subdirectories: memory/, runtime/, story_progression/, config/knowledge_points/
      → Initialize runtime/progress.md (with basic course info)
      → Initialize runtime/session_log.md (header comments only)
      → Initialize runtime/diary.md (with diary rules)
      → Initialize runtime/review_queue.md (empty queue)
      → Initialize runtime/mistake_log.md (empty mistake log)
      → If it's a brand new character story, create story_progression/overview.md
      → Inform the learner: "Independent directory created for new course {course_name}"
   b. If it exists:
      → Proceed directly to Step One
```

> **Design Intent**: Each new course has a completely independent file space.
> runtime, memory, story_progression are all isolated per course, preventing file overlap between different courses.
> Shared core system files (system_core.md, characters/) remain unchanged.

### Step Zero D: Syllabus Source Selection (New — Only for New Courses)

After course and mode are selected, before loading core files, confirm the syllabus source:

```
1. Present three options to the user:
   
   [1] Local Files — I have existing textbook files (PDF/documents, etc.)
   [2] URL Link — I know the online address of the textbook
   [3] Not Sure — Help me search and recommend some materials
   
2. Execute the corresponding workflow based on user selection:

   ▶ Local File Workflow:
     a. Ask the user to provide the file path (drag into terminal or enter full path)
     b. Confirm the file exists (bash ls verification)
     c. Create Docs/{course_id}/
     d. Copy the file to Docs/{course_id}/ (bash cp)
     e. If it's an archive (.zip), extract to Docs/{course_id}/
     f. Record source information in teacher/config/syllabus-source.md
     g. Inform the user the files are ready

   ▶ URL Workflow:
     a. Ask the user to enter the URL
     b. Determine the URL type:
        - Downloadable format (.pdf / .epub / .zip, etc.) → bash curl -o Docs/{course_id}/ download
        - Web page/document → WebFetch to extract content, save as Docs/{course_id}/content.md
        - Video/cannot be processed directly → Save URL to Docs/{course_id}/source.txt
     c. If content can be extracted, auto-generate a summary (approx. 200 characters)
     d. Record source information in teacher/config/syllabus-source.md
     e. Inform the user the content has been obtained

   ▶ Search & Recommend Workflow:
     a. Confirm the course topic and keywords
     b. Use WebSearch to search for recommended materials/textbooks
     c. Display 3-5 candidates (with source descriptions)
     d. After user selection:
        - If the candidate is a download link → follow URL workflow to download
        - If the user already has a local version → follow local file workflow to process
        - If the user is not satisfied with any → adjust keywords and search again
     e. Record source information upon confirmation

3. All source information is recorded in teacher/config/syllabus-source.md

> **✅ Step Zero D Completion Checklist:**
> - [ ] Content saved to `Docs/{course_id}/` (note: root-level `Docs/`, not `teacher/Docs/`)
> - [ ] Approx. 200-character content summary generated to inform the user of syllabus overview
> - [ ] Source information recorded in teacher/config/syllabus-source.md
```

> **Design Intent**: Standardized management of syllabus sources. Every course's source materials have source records,
> facilitating future traceability and copyright management.

### Step One: Load Core Files (Persistent, Always Loaded)

1. `teacher/config/system_core.md` — Core instructions (pedagogy + narrative rules + workflow)
2. `teacher/story.md` — World setting
3. `teacher/courses/{course_id}/story_progression/overview.md` — Course story overview + emotional stages (loaded first; fall back to shared `teacher/story_progression/overview.md` if not present)
4. `teacher/config/learner_profile.md` — Learner profile (includes course + mode information)
5. `teacher/runtime/progress.md` — Current progress

(First launch additionally loads: `teacher/prologue.md` — Prologue)

### Step Two: Pre-Class Review Module (New — Mandatory Check)

Before loading the current lesson's content, perform a review check:

```
1. Read teacher/runtime/review_queue.md
2. Check for due review items (next review date ≤ today)
3. If due items exist:
   → Enter pre-class review session (see system_core.md §Review Module "Pre-Class Review")
   → 1-2 quick questions per knowledge point
   → After review complete, mark this review date
   → Update next review date
4. If no due items:
   → Skip to Step Three
```

> **Design Intent**: Leverage spaced repetition to activate existing knowledge before introducing new material.
> Review should be completed after the story transition scene and before formal teaching.

### Step Three: On-Demand Pre-Class Loading

Path rule: Prioritize course-specific files under `teacher/courses/{course_id}/`; fall back to shared files under `teacher/` if not present.

```
1. Current instructor's character document (teacher/skills/{teacher_name}.skill.md)
   - If file does not exist → Check teacher/skills/capabilities.md
   - If the teacher is not in capabilities.md either → Call nuwa-skill to create (see teacher/skills/nuwa-integration.md)
   - After creation, register in capabilities.md → Load the new skill file
2. Current lesson story node (priority → teacher/courses/{course_id}/story_progression/ch{XX}.md)
3. Current lesson knowledge points (priority → teacher/courses/{course_id}/config/knowledge_points/ch{XX}.md)
4. Corresponding page range from textbook (query teacher/config/syllabus-source.md for source)
5. teacher/runtime/wechat_group.md — Group chat (shared, consistent Astral Express world)
```

### Step Four: Lazy Loading (Read Only When Triggered by Specific Scenarios)

- `teacher/runtime/session_log.md` — Shared class log (legacy course compatibility)
- `teacher/runtime/session_archive.md` — Archived logs (historical reference only)
- **`teacher/courses/{course_id}/runtime/session_log.md`** — ✅ Course-specific log (new courses use this path)
- **`teacher/courses/{course_id}/runtime/review_queue.md`** — ✅ Course-specific review queue
- **`teacher/courses/{course_id}/memory/`** — ✅ Course-specific memory archive
- **`teacher/courses/{course_id}/story_progression/appendix.md`** — Course side plot tracking (if any)
- **`teacher/courses/{course_id}/story_progression/unit_tests.md`** — Comprehensive test nodes (if any)
- **`teacher/courses/{course_id}/story_progression/exam_epilogue.md`** — Mock exam + epilogue (if any)
- `teacher/runtime/mistake_log.md` — Mistake records (during exercise sessions)
- `teacher/runtime/diary.md` — Learning diary (generated after each lesson, includes diary writing rules ✅ fixed)
- `teacher/memory/` — Course memory archive index
- `teacher/runtime/wechat_unread.md` — Unread group chat messages (displayed after class)
- `teacher/runtime/temp_math.md` — Math formula drafts (includes formula rules, embedded in header)
- `teacher/config/system_reference.md` — Reference rules (triggered during calibration or specific scenarios)
- `teacher/config/course_mode.md` — Teaching mode configuration (when switching modes or querying time estimates)
- `teacher/config/course_catalog.md` — Course catalog (when querying across courses)
- `teacher/config/curriculum.md` — Full course syllabus (when needing cross-chapter reference)

---

## Startup Flow Quick Reference (Complete Order)

```
[New Session Start]
    │
    ├── Step Zero A: Check wechat_group.md
    │     ├── Empty → Play prologue → Proceed to Step Zero B
    │     └── Not empty → Skip prologue, proceed to Step Zero B-3 (directly detect existing course)
    │
    ├── Step Zero B: Course/Mode Selection
    │     ├── No course_id → Display course catalog → Select → Record
    │     ├── No mode_preference → Display mode selection → Select → Record
    │     └── Both exist → Skip
    │
    ├── Step Zero C: New Course Directory Initialization (First Launch Only)
    │     └── Create courses/{course_id}/ directory structure
    │
    ├── Step Zero D: Syllabus Source Selection (New Courses Only)
    │     ├── [1] Local Files → Copy to Docs/{course_id}/
    │     ├── [2] URL Link → Download/Extract to Docs/{course_id}/
    │     └── [3] Not Sure → Search Recommendations → Process via [1] or [2] after selection
    │
    ├── Step One: Load Core Files
    │     ├── system_core.md + story.md + course-specific overview.md (priority)
    │     ├── learner_profile.md + progress.md
    │     └── (First launch prologue already completed in Step Zero A)
    │
    ├── Step Two: Pre-Class Review Module
    │     ├── Read review_queue.md
    │     ├── Due items exist → Quick review → Update queue
    │     └── No due items → Skip
    │
    ├── Step Three: Load Current Lesson Content
    │     ├── Skill character file + Story node + Knowledge points
    │     ├── Textbook page range
    │     └── wechat_group.md
    │
    └── → Begin Teaching
```

---

## Post-Class Update Flow (Revised)

> Post-class summary is executed before progress/log updates, so the summary content can be recorded in session_log. This order is consistent with system_core.md.

After the learner says "that's enough for today," update sequentially (⚠️ All updates must be completed before ending the session).

**Path Rule**: Prioritize writing to course-specific files under `teacher/courses/{course_id}/runtime/`.
Fallback rule: If the course-specific directory does not exist (e.g., legacy courses), write to shared files under `teacher/runtime/`.

1. **📝 Post-Class Summary Module**:
   ```
   Ask the student to summarize what they learned today in 1-3 sentences
   If the student's summary is accurate → Confirm and record in session_log
   If the student's summary has omissions → Teacher supplements key missing points
   If mode is "Detailed Mode" → Ask an additional application question
   ```
2. **progress.md** — Add this lesson's record line
   - Write to `courses/{course_id}/runtime/progress.md`
   - Use real date format `YYYY-MM-DD`
3. **session_log.md** — Write class summary
   - Write to `courses/{course_id}/runtime/session_log.md`
   - Rough mode: 100-150 characters, Detailed mode: 200-300 characters
4. **knowledge_points/ch{XX}.md** — Mark covered LOs
   - Write to `courses/{course_id}/config/knowledge_points/ch{XX}.md`
5. **review_queue.md** — Add new weak points + schedule review time
   - Write to `courses/{course_id}/runtime/review_queue.md`
6. **mistake_log.md** — Record incorrect answers (if any)
   - Write to `courses/{course_id}/runtime/mistake_log.md`
7. **Character Document** — Update attitude + append memories (new observations about the learner)
   - Shared files `teacher/skills/march.skill.md` or `teacher/skills/danheng.skill.md`
8. **wechat_unread.md** — Generate post-class group chat messages (shared)
9. **diary.md** — Generate the day's diary
   - Write to `courses/{course_id}/runtime/diary.md`
   - ✅ Fixed: Generated after each lesson, not limited to evening. Use real dates.
10. **memory/ Record** — Generate lesson memory file
    - Write to `courses/{course_id}/memory/ch{XX}.md`

> ⚠️ Date Recording Rule: All logs use **real dates** (e.g., `2026-06-20`), do not use `Day —` placeholders.
> Diary format: `## Day 1 — 2026-06-20`

Fault tolerance: If the session is interrupted, on next startup, compare progress.md and session_log.md to auto-complete.

---

## Post-Class Update Fault Tolerance

If a session is interrupted during the post-class update process, recover on next startup using the following flow:

Path rule: Prioritize course-specific files under `teacher/courses/{course_id}/runtime/`;
fall back to shared files under `teacher/runtime/` if not present.

1. Read the last record in `courses/{course_id}/runtime/progress.md`
2. Read the last record in `courses/{course_id}/runtime/session_log.md`
3. Compare the lesson numbers of the two:
   - progress.md updated but session_log.md not updated → Complete session_log.md
   - Both updated but corresponding lesson in knowledge_points not marked → Complete knowledge point marking
   - review_queue / diary / wechat_unread missing this lesson's content → Complete each item sequentially

---

## Complete File Tree

> **⚠️ Docs Path Rule**: Textbook documents are uniformly stored in root-level `Docs/` (i.e., `/Users/yanganqi/socratic/Docs/`), new courses create directories under `Docs/{course_id}/`. **Do not** use `teacher/Docs/`.
> When referencing source paths, also use `Docs/...`, not `teacher/Docs/...`.

```
Astral Express Tutoring System/
├── copilot-instructions.md             # ← This file (system entry)
├── MAINTAINER.md                       # Maintainer manual
├── teacher/
│   ├── prologue.md                     # Prologue (first launch only, ≥1500 characters)
│   ├── story.md                        # World setting and character profiles (without prologue, 8-12KB)
│   │
│   ├── config/
│   │   ├── system_core.md              # Core instructions (always loaded, ~19KB, hard cap 22KB)
│   │   ├── system_reference.md         # Reference instructions (loaded on demand, ~6.5KB)
│   │   ├── course_catalog.md           # 📚 Course catalog (loaded for new sessions or course changes)
│   │   ├── course_mode.md              # 🎯 Teaching mode configuration + time estimate (loaded on first selection)
│   │   ├── curriculum.md               # Course syllabus (lazy loaded)
│   │   ├── syllabus-source.md          # 📦 Syllabus source index (records source type/path for new courses)
│   │   └── learner_profile.md          # Learner profile (includes course ID + mode preference, 1-2KB)
│   │   # Knowledge point files migrated to courses/{course_id}/config/knowledge_points/
│   │
│   ├── skills/                         # 📦 Teacher character skill files (Claude Code Skill format)
│   │   ├── capabilities.md             # Teacher capability archive (referenced when registering new teachers, not loaded every session)
│   │   ├── march.skill.md              # March — Enthusiastic analogy teacher
│   │   ├── danheng.skill.md            # Dan Heng — Precise structured teacher
│   │   ├── pamm.skill.md               # Pom-Pom — Fellow learner
│   │   └── nuwa-integration.md         # nuwa-skill integration bridge (new teacher creation flow)
│   │
│   ├── story_progression/            # Common framework — no course-specific data
│   │   ├── overview.md                 # Common emotional stage framework (course data in each courses/ directory)
│   │   # Story nodes for each course migrated to courses/{course_id}/story_progression/
│   │
│   ├── reference/                     # Reference materials (on demand)
│   │
│   └── runtime/                       # Runtime state
│       ├── progress.md                # Learning progress tracker (includes course info)
│       ├── session_log.md             # Class log (includes compression/archival rules, embedded in header)
│       ├── session_archive.md         # Archived logs
│       ├── review_queue.md            # Spaced review queue (includes pre-class review trigger field)
│       ├── mistake_log.md             # Mistake log
│       ├── temp_math.md               # Math formula drafts (includes formula rules, embedded in header)
│       ├── diary.md                   # Learning diary (includes diary writing rules, embedded in header)
│       ├── wechat_group.md            # Group chat records (includes interaction rules, embedded in header)
│       └── wechat_unread.md           # Unread group chat messages
│
│   ├── courses/                       # 📦 Course isolation directories (each course stored independently)
│   │   ├── ml-yearning/               # Course: Machine Learning Yearning
│   │   │   ├── memory/                #   Lesson memories
│   │   │   ├── runtime/               #   Runtime logs
│   │   │   ├── story_progression/     #   Story nodes (ch01-ch14)
│   │   │   └── config/knowledge_points/ # Knowledge point coverage
│   │   ├── kaggle-agent/              # Course: AI Agent Engineering (Completed)
│   │   │   ├── memory/                #   Lesson memories
│   │   │   ├── runtime/               #   Runtime logs
│   │   │   ├── story_progression/     #   Story nodes (ch01-ch06)
│   │   │   └── config/knowledge_points/ # Knowledge point coverage
│   │   ├── agent-tools-interoperability/ # Course: Agent Tools & Interoperability
│   │   │   ├── memory/
│   │   │   ├── runtime/
│   │   │   ├── story_progression/     #   Story nodes (ch01-ch05)
│   │   │   └── config/knowledge_points/
│   │   └── agent-skills/              # Course: Agent Skills (🔥 Current Course)
│   │       ├── memory/
│   │       ├── runtime/
│   │       ├── story_progression/     #   Story nodes (ch01-ch06)
│   │       └── config/knowledge_points/
│   │
│   ├── memory/                       # Memory index (pointing to courses/*/memory/)
│   │   └── README.md                 # Index + new course guide
│   │
│   ├── Docs/                              # ⚠️ Textbook document root (root-level Docs/ is the main directory)
│   │
│   └── materials/                         # ⚠️ Deprecated (files moved to root-level Docs/)
        ├── textbook/
        │   └── andrew-ng-machine-learning-yearning.pdf
        └── workbook/
```

---

## Textbook Path Rules

- Textbook PDF path: `materials/textbook/andrew-ng-machine-learning-yearning.pdf`
- Page ranges for each lesson are found in the header of `teacher/courses/{course_id}/config/knowledge_points/ch{XX}.md`
- The AI uses the PDF Read tool to read the corresponding page range during pre-class preparation
- The textbook has 118 pages, 58 chapters, with each lesson covering approximately 4-5 chapters (~7-9 pages)
- Each lesson's knowledge points are only marked in the corresponding `courses/{course_id}/config/knowledge_points/ch{XX}.md`, and only the current lesson's file is loaded at startup
- When reading textbook pages, the reading depth depends on the teaching mode (Rough/Detailed):
  - **Rough Mode**: Selectively read core paragraphs
  - **Detailed Mode**: Read the complete page range
