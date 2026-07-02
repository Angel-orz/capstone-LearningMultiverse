# syllabus-source.md — Syllabus Source Index

> This file records textbook source information for each course.
> When adding a new course, the startup workflow (Step Zero D) guides the user to select a source and records it here.
> Files are stored in the `Docs/{course_id}/` directory.

---

## Source Type Description

| Type | code | Description | Storage Location |
|------|------|-------------|---------|
| Local file | `local` | User-specified local path, copied to project | `Docs/{course_id}/` |
| URL | `url` | Download or extract content from URL | `Docs/{course_id}/` |
| Search recommendation | `search` | Auto-search recommendations, processed as local/url after selection | `Docs/{course_id}/` |

---

## Course Textbook Sources

| Course ID | Source Type | Original Path/URL | Local Copy Path | Notes |
|---------|---------|-------------|-------------|------|
| ml-yearning | local | `materials/textbook/andrew-ng-machine-learning-yearning.pdf` | `Docs/andrew-ng-machine-learning-yearning.pdf` | Local textbook |
| kaggle-agent | local | `Docs/Kaggle/` (multi-file) | `Docs/Kaggle/` | Local textbook collection |
| agent-tools-interoperability | local | `Docs/Kaggle/Agent Tools & Interoperability_Day_2.pdf` | `Docs/Kaggle/` | Local textbook |
| agent-skills | local | `Docs/Kaggle/Agent Skills_Day_3.pdf` | `Docs/Kaggle/` | Local textbook |
| claude-101 | url | `https://anthropic.skilljar.com/claude-101` | `Docs/claude-101/lessons_markdown/` | SkillJar online course, login required |
| agent-security-eval | local | `Docs/Kaggle/Vibe Coding Agent Security and Evaluation_Day_4.pdf` | `Docs/Kaggle/` | Local textbook |

---

## New Course Textbook Source Record

```markdown
| {course_id} | {local/url/search} | {original path or URL} | {copy path} | {notes} |
```

## Textbook File Management Rules

1. **Local files**: Copy to `Docs/{course_id}/`, preserve original extension
2. **URL files**:
   - Downloadable formats (PDF, epub, etc.) → `curl -o Docs/{course_id}/{filename}`
   - Web page content → Extract via `WebFetch` and save as `Docs/{course_id}/content.md`
   - Also generate `Docs/{course_id}/source.txt` to record the original URL
3. **Search recommendations**:
   - Show 3-5 candidates after searching
   - After user selection, process via local or url workflow
   - If the user selects the online version of a recommended textbook → url workflow
   - If the user provides a locally downloaded version → local workflow
