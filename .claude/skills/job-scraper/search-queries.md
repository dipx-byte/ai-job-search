# Search Queries for Job Scraper

<!-- Customized for Jakarta / Indonesia job market (Oct 2026). Re-run /setup to refine. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Market: **Indonesia — Jakarta / Jabodetabek** (plus remote roles open to Indonesia).

Primary:
- **linkedin.com/jobs** — covered by the `linkedin-search` CLI. Always pass `--location "Jakarta, Indonesia"` (or `"Indonesia"` with `--remote remote`).
- **id.jobstreet.com** — Indonesia's largest general board (WebSearch fallback until a CLI is added with `/add-portal`).
- **glints.com/id** — startups and scale-ups, strong for growth/ops/marketing roles.
- **kalibrr.com** — tech, startups and corporate roles in Indonesia.
- **dealls.com** — startup and professional roles in Jakarta.

Secondary:
- `freehire-search` CLI for tech/data roles (`--country` Indonesia or remote).
- Company career pages via `site:` searches (sports, lifestyle, hospitality, logistics/transport, associations).

Danish demo portals (jobindex, jobnet, jobbank, jobdanmark) stay `enabled: false`.

## Query Categories

Write every category in **English and Bahasa Indonesia** — Indonesian postings mix both. Organize by function, not exact title.

### Priority 1: Growth, Operations & Systems

```
site:linkedin.com/jobs "growth specialist" Jakarta
site:linkedin.com/jobs "operations specialist" OR "business operations" Jakarta
site:id.jobstreet.com "growth" "operations" Jakarta
site:glints.com/id "growth" OR "operations" Jakarta
site:kalibrr.com "community" OR "growth" Jakarta
"spesialis operasional" OR "staf operasional" Jakarta lowongan
```

Titles to try as variants: Growth Specialist, Growth Associate, Operations Specialist, Business Operations Associate, Community Manager, Program/League Coordinator, Systems & Operations Analyst, Business Process Analyst.

### Priority 2: Data, Reporting & Automation

```
site:linkedin.com/jobs "data analyst" OR "reporting analyst" Jakarta
site:linkedin.com/jobs "business intelligence" OR "dashboard" Jakarta
site:id.jobstreet.com "data analyst" OR "admin data" Jakarta
site:glints.com/id "data analyst" OR "MIS" Jakarta
"analis data" OR "staf MIS" OR "admin data" Jakarta lowongan
```

Titles: Data Analyst, Reporting Analyst, MIS Staff, BI Analyst (junior), Automation/No-code Specialist, Google Workspace / Apps Script admin.

### Priority 3: Visual Content & Marketing

```
site:linkedin.com/jobs "content designer" OR "graphic designer" Jakarta
site:glints.com/id "graphic designer" OR "content creator" Jakarta
site:id.jobstreet.com "desain grafis" OR "visual content" Jakarta
"digital marketing" OR "social media specialist" Jakarta lowongan
```

Titles: Visual Content Designer, Graphic Designer (Canva/Figma), Social Media Specialist, Digital Marketing Executive, Marketing Communications Officer.

### Priority 4: Administration, Secretariat & Project Admin

```
site:id.jobstreet.com "sekretariat" OR "staf sekretariat" Jakarta
site:id.jobstreet.com "project admin" OR "project administrator" Jakarta
site:linkedin.com/jobs "project coordinator" OR "program officer" Jakarta
"staf administrasi" OR "admin proyek" Jakarta lowongan
```

Titles: Secretariat Staff, Project Admin/Coordinator, Program Officer (associations, NGOs, industry bodies), Executive/Office Admin.

## Location Filter

Acceptable:
- Jakarta (all areas) and South Tangerang / BSD
- Depok, Bekasi, Tangerang — borderline depending on office location
- Remote or hybrid open to Indonesia-based candidates
- Cikarang — borderline (check commute or hybrid terms)

Exclude: on-site roles outside Jabodetabek unless relocation is explicitly wanted.

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
