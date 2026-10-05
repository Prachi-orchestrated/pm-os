# PM OS

My personal product management operating system, built and maintained with Claude Code.

## Who I am
Prachi Singhal, a product leader with ~16 years of experience (~11 in product), who started as a software engineer.
I build AI platforms (agentic systems, RAG, evals and quality gates), personalization, and commercial and partnership products at consumer scale.
Recent work at Expedia Group: Global Product Lead for AI trip-planning and conversational AI products. Earlier: Bharti Airtel, UnitedHealth Group, Max Life Insurance, Infosys.
MBA from IIM Ahmedabad. Domains: travel, telecom, healthtech, insurance.

## How I work with you
- I'm a non-coder. Explain what you're doing in plain language, without jargon.
- One small step at a time. Check with me before anything big or irreversible.
- I make the product decisions and do the testing; you do the building.
- Prefer shipping working outputs over theory.
- Show me a plan and wait for my OK before building anything new.

## Folder map
- `private/`: my personal files, used as context: resume (`resume.pdf`), job preferences (`preferences.md`) and experience brief (`experience-brief.md`). Kept out of Git.
- `knowledge/`: reusable notes and reference material (frameworks, research, learnings).
- `projects/`: one subfolder per project.
  - `projects/job-search/`: my job search workstream.
- `.claude/skills/`: my custom skills (slash commands).

## Rules
- Never copy contact details (phone, email, address) or content from `private/` into files outside `private/`. This repo is public. The only exception is the short summary in "Who I am" above.
- Ask before deleting anything.
- Keep everything simple enough for me to maintain myself.
- Run a privacy check and show me the file list before every upload.
- Never invent links or data. Every output must come from a source you actually opened.
- Keep personal settings in `private/`, and keep skills generic so they read from there.

## Changelog
- 2026-10-04: Set up PM OS: created folders, moved personal files into `private/`, added `.gitignore` and this CLAUDE.md.
- 2026-10-04: Added /find-jobs skill (`.claude/skills/find-jobs/`): finds, verifies and scores jobs into `private/job-tracker.csv`, logging every job checked in `private/seen-jobs.csv`.
- 2026-10-04: Updated /find-jobs: 5-per-company limit now applies only to broad runs; single-company runs search more thoroughly (by role type and location) and log every opened posting.
- 2026-10-04: Updated /find-jobs: single-company runs ignore the 10-saved target; roles ruled out from search results are logged as skipped ("not opened") without counting toward the 40.
- 2026-10-05: Updated /find-jobs: added hard location and level gates before scoring; broad runs save at most 3 jobs per company and search least recently searched companies first.
- 2026-10-05: Updated /find-jobs: added a remote track to broad runs (up to 10 of 40 postings) with a remote hard gate, and more specific work_mode values.
- 2026-10-05: Updated /find-jobs: remote track now opens at most 5 postings and saves at most 3 remote roles per broad run.
- 2026-10-05: Published PM OS to GitHub as a public repo (github.com/Prachi-orchestrated/pm-os). Skill rules now point to private/preferences.md instead of restating personal details; added examples/ with made-up preferences and tracker files.
- 2026-10-05: Added README.md, and new working rules in CLAUDE.md (plan before building, privacy check before every upload, no invented links or data, generic skills).
