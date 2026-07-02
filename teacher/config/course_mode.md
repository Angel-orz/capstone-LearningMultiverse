# course_mode.md — Teaching Mode Configuration

> User selects teaching mode when starting a new course. The selection is recorded in the `mode_preference` field of `learner_profile.md`.
> Mode remains consistent within the same course and cannot be switched mid-course (to prevent teaching content discontinuities).

---

## Mode Selection

### Rough Mode (Overview) — Suitable for quick overview or review

| Feature | Description |
|------|------|
| **Content Density** | Focus on core concepts and key conclusions; omit some detailed cases and extended discussions |
| **Analogy Usage** | Primarily analogies, 1-2 core analogies per knowledge point |
| **Textbook Reference** | Selective reference to core textbook ideas, not fully page-by-page coverage |
| **Teaching Pace** | Faster progression; each knowledge point's P1-P5 flow compressed to P1→P3→P5 |
| **Probing Depth** | Move forward when the student answers core concepts correctly; no deep probing on edge details |
| **Suitable For** | Review, overview, learners with limited time |

### Detailed Mode (In-depth) — Suitable for systematic learning, deep understanding

| Feature | Description |
|------|------|
| **Content Density** | Cover most textbook content, including detailed cases and edge cases |
| **Analogy Usage** | Multiple analogies approaching the same concept from different angles |
| **Textbook Reference** | Page-by-page progression, covering main content and examples in the textbook |
| **Teaching Pace** | Steady progression; full P1-P5 flow for each knowledge point |
| **Probing Depth** | Thorough probing to confirm understanding, including application-level extension questions |
| **Suitable For** | Beginners starting from scratch, learners who want to build solid knowledge systems |

---

## Time Estimation Formula

Estimate study time per lesson and entire course based on total textbook pages and selected mode.

### Base Parameters

| Parameter | Rough Mode | Detailed Mode |
|------|---------|---------|
| **Pages per minute** | 0.30-0.35 pages/min | 0.15-0.20 pages/min |
| **Time per page** | ~3 min | ~5-7 min |
| **Base time per lesson** | 25 min + 5 min buffer | 45 min + 10 min buffer |

### Formula

```
Estimated time per lesson = (pages per lesson × minutes per page) + fixed buffer
Total course time = Σ lesson time + (review time × number of reviews)

Rough mode example (8 pages/lesson):
  Time per lesson = 8 × 3 + 5 = 29 min ≈ 30 min
  14 lessons total ≈ 7 hours

Detailed mode example (8 pages/lesson):
  Time per lesson = 8 × 5 + 10 = 50 min ≈ 50 min
  14 lessons total ≈ 12 hours
```

### Quick Reference by Page Count

| Pages per Lesson | Rough Mode (incl. buffer) | Detailed Mode (incl. buffer) |
|---------|------------------|------------------|
| 5 pages | ~20 min | ~35 min |
| 8 pages | ~30 min | ~50 min |
| 10 pages | ~35 min | ~60 min (1h) |
| 12 pages | ~40 min | ~75 min (1h15m) |
| 15 pages | ~50 min | ~90 min (1h30m) |

### Current Course Estimate

**ml-yearning** (118 pages, 14 lessons, ~8-9 pages per lesson):
| Mode | Avg per Lesson | Total Duration | Recommended Daily Lessons | Suggested Completion Period |
|------|---------|-----------|------------|------------|
| Rough | ~25-30 min | ~6-7 hours | 3-4 lessons | 4-5 days |
| Detailed | ~45-55 min | ~11-13 hours | 2 lessons | 7-8 days |

---

## Teaching Mode Selection Flow

At the start of a new course, present the following options to the user:

```
Welcome aboard the train! Before we begin, let me confirm two things —

📚 **Course**: {Course Name} ({Textbook Name}, {Total Pages} pages, {Number of Lessons} lessons)

🎯 **Teaching Mode** — which one would you like?

  [1] Rough Mode — Focus on core concepts, ~{X} min per lesson, ~{Y} hours total
       Great for a quick start or limited time

  [2] Detailed Mode — Covers more textbook details, ~{A} min per lesson, ~{B} hours total
       Great for systematic learning and deep understanding

Which one would you like? 1 or 2?
```

After selection, record in learner_profile.md and maintain this mode throughout the course.

---

## Mode Impact on Teaching Flow

### Pre-Lesson Preparation Differences

| Step | Rough Mode | Detailed Mode |
|------|---------|---------|
| P0 Milestone Keywords | 2-3 core keywords | 3-5 keywords + sub-concepts |
| Textbook Reading | Selectively read core paragraphs | Read full page range |
| P0.5 Brainstorming | Concise, 1 counter-intuitive inference | 2-3 counter-intuitive inferences + applications |
| Teaching Pitfall | 1 main pitfall | 1-2 pitfalls as backup |

### P1-P5 Flow Differences

- **P1 Recon**: Rough → 2-3 probing questions; Detailed → 3-5 in-depth probing questions
- **P2 Pre-emptive Failure**: Rough → Quickly expose typical errors; Detailed → Give students ample time to trial and error
- **P3 Contradiction Exposure**: Rough → 1 core contradiction; Detailed → Multi-layered contradiction exposure
- **P4 Reconstruction**: Rough → 1 analogy + core reasoning chain; Detailed → Multiple analogies + extended discussion
- **P5 Naming**: Same for both — naming right belongs to the student

### Post-Lesson Update Differences

- **Rough Mode**: session_log writes 100-150 word summary, only marks core knowledge points
- **Detailed Mode**: session_log writes 200-300 word detailed summary, fully marks all discussed knowledge points

### Review Module Differences

- **Rough Mode**: Pre-lesson quick review (1-2 questions, 5 min), no post-lesson summary
- **Detailed Mode**: Pre-lesson review (2-3 questions, 8-10 min) + post-lesson summary (3-5 min, student recaps lesson key points)
