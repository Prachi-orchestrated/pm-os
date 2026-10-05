---
name: find-jobs
description: Search the web for open product roles that match Prachi's preferences, verify each posting, score fit, and save matches to private/job-tracker.csv. Optional focus after the command, e.g. "/find-jobs Acme Corp" or "/find-jobs chief of staff".
argument-hint: "[optional focus: company, role or lane]"
---

# /find-jobs

Find real, open roles that fit me, score them honestly, and save the good ones to my tracker.

**Focus for this run:** $ARGUMENTS
(If this is empty, do a general search. If it names a company, role or lane, search only for that, still following every rule below.)

---

## Limits for this run (edit these numbers to change behaviour)
- **Target:** about 10 saved matches.
- **Stop after:** 40 postings opened in total, even if fewer than 10 were saved.
- **Per company:** open at most 5 postings from any one company. This applies only to broad runs. When the focus names one company (e.g. `/find-jobs Acme Corp`), skip this limit and use the 40-postings limit instead.
- **Saved per company:** save at most 3 jobs from any one company per run. This applies only to broad runs. Once a company has 3 saved, stop opening its postings and move on to the next company.
- **Remote track (broad runs only):** open at most 5 remote postings and save at most 3 remote roles per run (see Step 3). Any unused remote budget goes to the normal company search.
- **Old posting warning:** flag postings older than 60 days.

---

## Step 1: Read my context
- Read `private/experience-brief.md` and `private/preferences.md`.
- Read `private/resume.pdf` only if you need more detail to judge a specific role.
- Never copy contact details or private content anywhere outside `private/`.

## Step 2: Load (or create) my two files
Both files live in `private/`. If one doesn't exist, create it with just this header row:

**`private/job-tracker.csv`**
```
date_found,posted_date,company,title,location,work_mode,level,lane,fit,score,why_fit,gaps,link,source,status,notes
```

**`private/seen-jobs.csv`**
```
date_checked,company,title,location,link,decision,reason
```

Read both files so you know which jobs I've already seen.

## Step 3: Search
If a focus was given, skip straight to it.

**Broad runs: search the least recently searched companies first**, so each run covers different companies:
1. Make one list of all companies from `preferences.md`: the dream companies plus the "Also worth checking" list.
2. For each company, find the most recent `date_checked` for that company in `seen-jobs.csv`.
3. Search companies in this order:
   - Companies never searched (no rows in `seen-jobs.csv`) come first.
   - Then companies by oldest last-searched date first.
   - If two companies are tied, dream companies go first, then the order they appear in `preferences.md`.
4. Only after working through the list, consider any other company with a strong match.
5. Before searching, write down the company order you will use, so it can go in the summary.

**Broad runs: remote track.** Run this first in every broad run, before the company search, so it always gets covered:
- Search for remote roles at strong companies based in the regions my remote rules in `preferences.md` allow. Use one search per remote search region listed there (e.g. "remote Region A", "remote Region B"), combined with my role lanes (e.g. "<role lane> remote Region A").
- Use company career pages and Greenhouse, Lever, Ashby and Workday boards, as for normal searches.
- Open at most 5 remote postings, and save at most 3 remote roles. Stop the remote track as soon as either limit is reached. Every remote role must pass the remote gate in Step 6 as well as the level gate.
- The per-company limits (5 opened, 3 saved) also apply to remote roles.

Rules:
- Match my **role lanes**, **level** and **location/remote rules** from `preferences.md`. Respect the "Skip" list.
- Prefer company career pages and public job boards: Greenhouse, Lever, Ashby, Workday and company websites.
- Don't rely on LinkedIn (it usually blocks automated access).

**When the focus is one company, search more thoroughly:**
- Use the company's own careers search page wherever possible. Third-party job boards are a backup and often list stale roles.
- Run several separate searches, one per role type: product manager (covering every title my level rules in `preferences.md` allow), partnerships / business development, strategy / chief of staff, and commercial / monetization.
- Repeat those searches for each of my on-site/hybrid locations in `preferences.md`, plus country-wide or remote where my remote rules allow.
- Look past the first page of results.
- Keep going until the searches stop turning up new relevant roles, or until the 40-postings limit is reached.

## Step 4: Open and verify every posting
- Open the actual posting page for every candidate job.
- Confirm it is real and still open (e.g. it has an apply button or no "closed" or "no longer accepting" message).
- **Never save a job you haven't opened. Never invent or guess a link.** Use the exact URL of the page you opened.
- If the page won't load, or you can't tell whether it's open, don't save the job. Log it in seen-jobs as `skipped` with the reason "couldn't verify".
- Note the posted date if the page shows one.
- **Every posting you open must be logged in `seen-jobs.csv`**, even if it turns out not to match. Log non-matches as `skipped` with the reason (e.g. "level too junior", "City X only", "sales quota").
- **Roles ruled out from search results alone** (e.g. wrong location or clearly too junior): don't open them, but log them in `seen-jobs.csv` as `skipped`, with "not opened" in the reason (e.g. "City X only, not opened"). Use the exact link shown in the search results. These don't count toward the 40-postings limit and are never saved to the tracker.

## Step 5: Skip duplicates
Before scoring, skip a job if it's already in `seen-jobs.csv` or `job-tracker.csv`, **or** if it already came up earlier in this run. A job counts as a duplicate if:
- the **link** matches, **or**
- the **company + title + location** all match (this catches reposts with a new link; the same title in a different city is NOT a duplicate).

Don't add duplicates to seen-jobs again.

## Step 6: Hard gates (check before scoring)
Every job must pass **both** gates before it is scored. If it fails either gate, it is skipped: log it in `seen-jobs.csv` as `skipped` with the gate it failed (e.g. "Failed location gate: City X only") and never save it. **A high fit score never overrides a gate.**

**Location gate.** The job passes only if at least one location it offers is:
- one of my on-site/hybrid locations in `preferences.md` (including that location's wider metro area, if `preferences.md` names one), or
- a remote option that passes the remote gate below.

A job listing several cities (e.g. "City X / City A") passes if any one of them is on my list. In the tracker, list all its locations in `location` and say in `notes` which location passes (e.g. "Passes location gate via City A"). Jobs that need relocation, or that are remote from a region my preferences skip, fail.

**Remote gate** (for any job saved because it is remote). Use the remote rules in `preferences.md`. It passes only if **all** of these are true:
- The company is based in a region my remote rules allow.
- The posting allows someone based in my home country, in one of the remote forms my rules accept (e.g. remote in my country, remote in my region, or global remote).
- It does **not** require working hours my rules exclude.
- It does **not** require living in, or having work authorization for, any country my rules exclude.

If any of these fails, skip the job and log the exact reason in `seen-jobs.csv` (e.g. "Failed remote gate: requires Country Y right to work", "Failed remote gate: Region Z hours required", "Failed remote gate: Region Z residents only"). If the posting doesn't say whether someone based in my home country can apply, treat the gate as failed and log "couldn't confirm remote eligibility".

**Level gate.** The job passes only if it matches my level rules in `preferences.md`, including any separate title rules for big tech companies (where titles often run lower than at startups).

Titles on my "skip" level list, and titles below the lowest level `preferences.md` allows for that kind of company (e.g. "Product Manager II" where only Senior and above is allowed), fail.

If the posting doesn't make the location or level clear, treat the gate as failed and log the reason "couldn't confirm location" or "couldn't confirm level".

## Step 7: Score fit
Use the "How to score fit" section of `preferences.md`:
- **fit:** Strong / Medium / Stretch
- **score:** 1-10
- **why_fit:** one line on why it matches
- **gaps:** one line with the honest gap

Be honest. Use the "Gaps to be honest about" in `experience-brief.md`.

## Step 8: Save
**Save to the tracker** only if the job passed both hard gates (Step 6), the company has fewer than 3 jobs saved this run (broad runs only), and the job is:
- Strong, or
- Medium, or
- Stretch **at a dream company**

For each saved job, add a row to `job-tracker.csv`:
- `date_found`: today's date (YYYY-MM-DD)
- `posted_date`: from the posting (YYYY-MM-DD), or leave blank if not shown
- `work_mode`: On-site / Hybrid / Remote, as specific as possible. For remote roles, say where it's remote from, e.g. "Remote (India)", "Remote (APAC)" or "Remote (global)".
- `lane`: e.g. AI/ML product, Growth, Commercial PM, Chief of Staff
- `source`: where you found it, e.g. Greenhouse, company careers page
- `status`: `New`
- `notes`: anything useful. If the posting looks older than 60 days, write "Posting may be old (over 60 days)".

**Log every job you checked**, saved or not, in `seen-jobs.csv`, with `decision` set to `saved` or `skipped` and a short `reason` (e.g. "Strong fit", "level too junior", "US remote", "couldn't verify", "closed").

**No padding:** if fewer than 10 good matches exist, save only those. Never lower the bar to reach the target.

### CSV safety rules
- Wrap **every** field in double quotes, e.g. `"City A, Country"`.
- If text contains a double quote, write it twice: `"The ""AI"" team"`.
- Only add new rows at the bottom. Never change or delete existing rows.

## Step 9: Stop
Stop searching when you reach either the target number of saved matches or the 40-postings limit, whichever comes first.

**When the focus is one company:** ignore the 10-saved target. Keep going until the searches stop finding new relevant roles, or until you reach 40 opened postings.

## Step 10: Summary
End with a short, plain-language summary:
- How many relevant postings the searches found, how many you opened, and why you stopped (target reached, 40-postings limit, or no more relevant roles)
- For broad runs: the company order you searched in, and which companies you reached
- For broad runs: the remote track. How many remote postings you opened, how many were saved, and the main reasons remote roles failed. If no remote roles passed, say so plainly (e.g. "No remote roles passed this run"). Never lower the bar to save one.
- Jobs checked, saved and skipped (with the main skip reasons, including how many failed each hard gate)
- If fewer than 10 were saved, say so plainly and why (e.g. "only 6 roles met the bar")
- Top 3 matches: company, title, fit, score, and link
- Anything I should know (e.g. sites that wouldn't load)
