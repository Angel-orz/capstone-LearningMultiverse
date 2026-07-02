# curriculum.md — Course Curriculum

> This file is lazily loaded. Page ranges for each lesson's textbook content are embedded in the header of corresponding `knowledge_points/ch{XX}.md` files, so there is no need to read this file per lesson. Read only when needing to view the full course structure or for cross-chapter queries.

## Course Overview

| Lesson | Teacher | Textbook Chapters | Core Knowledge Points | Pages |
|------|------|---------|----------|------|
| Ch.1 | March | 1-4 | ML strategy, how to use this book, prerequisites, scale-driven | 1-10 |
| Ch.2 | Dan Heng | 5-8 | Dev/test sets, same distribution, set size, single evaluation metric | 10-18 |
| Ch.3 | March | 9-12 | Optimizing/satisficing metrics, accelerate iteration, changing metrics, summary | 18-25 |
| Ch.4 | Dan Heng | 13-16 | First system, error analysis, parallel evaluation, cleaning mislabeled data | 26-34 |
| Ch.5 | March | 17-20 | Eyeball/black-box sets, set size, error analysis summary, bias & variance | 34-43 |
| Ch.6 | Dan Heng | 21-24 | Bias-variance examples, comparing optimal error, addressing bias/variance, trade-offs | 44-52 |
| Ch.7 | March | 25-28 | Reducing avoidable bias, training set error analysis, reducing variance, learning curves | 53-62 |
| Ch.8 | Dan Heng | 29-32 | Plotting training error, interpreting high bias, other scenarios, plotting learning curves | 63-69 |
| Ch.9 | March | 33-36 | Human-level performance, defining human-level, surpassing humans, mismatched training/test distributions | 70-78 |
| Ch.10 | Dan Heng | 37-40 | Data utilization decisions, inconsistent data, data weighting, generalizing to dev set | 79-86 |
| Ch.11 | March | 41-44 | Identifying bias/variance/data mismatch, addressing mismatch, synthetic data, optimization verification | 87-96 |
| Ch.12 | Dan Heng | 45-48 | Optimization verification formula, reinforcement learning example, end-to-end learning, more examples | 97-104 |
| Ch.13 | March | 49-52 | End-to-end pros/cons, Pipeline data availability, task simplicity, learning to output directly | 105-111 |
| Ch.14 | Dan Heng | 53-58 | Component error analysis, error attribution, formula, human comparison, diagnosing pipelines, teams | 112-118 |

## Textbook Info

- **Textbook**: Andrew Ng — *Machine Learning Yearning* (2018)
- **Total Pages**: 118 pages
- **Total Chapters**: 58 chapters
- **Path**: `materials/textbook/andrew-ng-machine-learning-yearning.pdf`

## Knowledge Map

```
ML Strategy Basics (Ch.1-4)
  ├── Why strategy is needed
  ├── Scale-driven ML progress
  └── Setting up dev/test sets
        ↓
Evaluation & Iteration (Ch.5-12)
  ├── Single evaluation metric
  ├── Error analysis
  ├── Bias & variance diagnosis
  ├── Learning curves
  ├── Human-level performance
  └── Data distribution issues
        ↓
Advanced Decisions (Ch.13-44)
  ├── Data weighting & handling inconsistencies
  ├── Synthetic data generation
  ├── Optimization verification testing
  └── End-to-end vs Pipeline
        ↓
Diagnosis & Attribution (Ch.45-58)
  ├── Error attribution
  ├── Pipeline component selection
  └── Comprehensive diagnosis
```

## Workbook Path

No accompanying workbook. Practice is done through Socratic questioning and in-class problem-solving during teaching. Incorrect answers are recorded in `teacher/runtime/mistake_log.md`.
