# PM OS

My personal product operating system, built with Claude Code. The first tool is `/find-jobs`.

**At a glance:** An AI agent that finds senior roles matching my profile, verifies every posting, scores fit honestly, and never shows me the same job twice. So far: 3 runs, 126 roles reviewed, 17 saved.

## The problem

Searching for a senior product role was a heavy, anxious operational task.

- I spent hours opening links across company career sites and job boards, then filtering them by hand.
- I lost track of what I had already seen or rejected, so every search carried a lot of mental load.
- Titles don't line up across companies. A "Director" at a startup can be a "Principal PM" at a big tech company. Keyword filters either missed roles that fit or flooded me with ones that didn't.
- I had to remember to search early in the week so I could plan my applications.

## Why AI

- I write my preferences and experience once, and every run reuses them.
- It reads unstructured job descriptions the way a person would, and judges fit against my actual experience rather than keywords.
- The searching, opening, filtering, scoring and tracking happen without me writing any code.

## How it works

1. **Read context.** Loads my preferences and experience brief from a private folder.
2. **Search.** Checks company career pages and public job boards, in an order that rotates across companies.
3. **Verify.** Opens every candidate posting and confirms it is real and still open.
4. **Hard gates.** Every job must pass my location and level rules. A job that fails either gate is skipped.
5. **Score.** Rates fit as Strong, Medium or Stretch, with a 1–10 score, one line on why it fits and one line on the honest gap.
6. **Save.** Adds jobs that clear the bar to my tracker.
7. **Log.** Records every job it checked, saved or skipped, with a reason, so it never shows me the same job twice.
8. **Summary.** Tells me in plain language what it checked, what it saved, why it stopped, and my top matches.

See `examples/job-tracker.example.csv` for what the tracker looks like.

## Key product decisions

- **Grounding.** It never saves a posting it hasn't opened, and never invents or guesses a link.
- **Hard gates vs soft scoring.** Location and level are yes/no rules. A high fit score can't override them.
- **Honest scoring.** Every saved job has a gaps field, and there's a Stretch tier so weaker fits are labelled as weaker, not hidden or inflated.
- **No padding.** If only a few jobs clear the bar, it returns fewer jobs. It never lowers the bar to hit a target.
- **No duplicates.** A seen-jobs log catches jobs I've already seen, including reposts with a new link.
- **Effort budget.** Each run has limits on how many postings it opens, in total and per company.
- **Human in the loop.** The AI finds and scores. I decide what to apply to.
- **Privacy by design.** My personal settings live in a `private/` folder that is never uploaded. The skills themselves are generic and read from that folder.

## What testing taught me

I tested every run and changed the tool based on what I saw.

- **The per-company cap cut off focused searches.** My first single-company run opened only 5 postings out of about 170 listed, because a "5 per company" limit stopped it. I asked why, traced it to that rule, and changed the cap to apply only to broad runs. Focused runs now search by role type and location until they run out of new roles.
- **Big companies crowded out the rest.** A broad run filled its whole target from two large companies. I added a cap of 3 saved jobs per company per run, and made broad runs start with the companies searched least recently.
- **A city outside my preferences raised a question.** That led to hard gates for location and level, checked before any scoring. The tracker now records which city let each role through.
- **Remote roles needed their own rules.** "Remote" can quietly mean US hours or another country's work authorization. I added a separate remote eligibility gate, plus a small budget for remote searches so they can't crowd out everything else.

## Results so far

Across 3 runs:

- 126 roles reviewed and logged
- 22 postings opened and verified, 17 saved to my tracker
- 104 roles ruled out from search results alone (wrong location, too junior, or not in my lanes)
- 6 companies covered
- Of the 17 saved: 6 Strong, 3 Medium, 8 Stretch

These runs happened before the hard gates existed. 1 of the 17 saved roles would now fail the level gate, which is exactly the problem the gates fix. And 8 of 17 being Stretch is one of the first things the planned scoring eval will look at.

## What v1 can't do yet

- No scheduled runs or notifications. I start each run myself.
- It doesn't use LinkedIn.
- Some career sites load their listings in ways the tool can't fully browse.
- I haven't measured scoring accuracy yet.
- It doesn't draft applications.
- The tracker is a CSV file, not a live sheet.

## What's next

1. Scheduled runs twice a week, with a notification when they finish.
2. An eval that compares the AI's fit scores with my own judgment on a set of jobs.
3. The next PM OS skills.

## Use it yourself

1. Copy the files in `examples/` into a `private/` folder.
2. Rename them to `preferences.md` and `job-tracker.csv`, and replace the made-up values with your own.
3. Add an `experience-brief.md` to `private/` describing your experience and your honest gaps.
4. Run `/find-jobs` in Claude Code.

## How it was built

I made the product decisions and did the testing. Claude Code did the building.
