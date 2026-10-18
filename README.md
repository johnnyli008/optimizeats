# ATS Resume Builder

A fast, private, ATS-optimized resume builder in a **single HTML file**. Paste a job description, get an instant keyword-match score, close the gaps, and print a clean, recruiter-ready resume to PDF — all without your data ever leaving your browser.

No installation. No accounts. No server. No tracking. Open the file and start typing.


## Features

- **ATS Keyword Match** — paste any job description and the analyzer extracts the skills and phrases recruiters' ATS filters scan for, then checks your resume against them in real time as you type.
- **Weighted match score (0–100%)** — multi-word skill phrases count double; plurals, variants, and common synonyms are recognized automatically.
- **One-click keyword gaps** — missing keywords appear as red chips; click the **+** on a chip to add it straight into your Skills list.
- **Resume Health Check** — seven structural checks (summary length, skills count, bullets per role, dates, and more) with a live pass/fail list.
- **Print-perfect preview** — on-demand, paginated preview on US Letter or A4 with a word/page estimate, and a print stylesheet that strips all UI so the PDF comes out clean.
- **Copy & paste backup** — your entire resume (including the job description and paper preference) exports as formatted JSON you can copy anywhere and restore later with one click.
- **Autosave** — every keystroke is saved to your browser's local storage (debounced), with a subtle "Saved" indicator and a manual `Ctrl/Cmd + S` shortcut.
- **Sample data included** — first run opens pre-filled with a complete Senior Project Manager example so you can see how everything works before entering your own details.

## Quick Start

1. Download `ats-resume-maker.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox, or Safari).
3. Click **Clear** in the top bar to wipe the sample data and start fresh — or just type over it.
4. When you're done, hit **Preview & Print** and choose **Print / Save PDF**.

That's it. There is nothing to install and nothing to configure.

## How to Use

### 1. Paste the job description first

The **ATS Keyword Match** box sits at the top for a reason: the job description drives everything else. Paste the full posting and the analyzer immediately shows:

- Your **match score**, color-coded: green (80%+), amber (60–79%), red (below 60%)
- **Green chips** for keywords already present in your resume (up to 14 shown)
- **Red chips** for missing keywords (up to 10 shown) — each with a **+** button that appends the keyword to your Skills section

The matcher is deliberately forgiving. It understands that "led a team", "managed teams", and "team leadership" all demonstrate *team leadership*; that "SQL" or "analyzed data" counts for *data analysis*; and that "managed", "management", and "manager" are the same root skill. Write naturally — the analyzer does the translation.

### 2. Fill in the editor

Work top to bottom through the cards:

- **Contact** — name plus a single line for phone, email, links, and location (pipe-separated reads best).
- **Professional Summary** — aim for 3–4 sentences that mirror the exact job title you're applying for. The health check wants 30+ words.
- **Skills** — hard skills first; these are what ATS filters weigh most heavily. One skill per line.
- **Work Experience** — most recent role first. Use the arrow buttons to reorder entries and **×** to remove them. Write quantified achievements ("Cut delivery time 23%..."), one per line — the health check requires at least two bullets per role.
- **Education** — degree, school, and year; add as many entries as you need.

### 3. Watch the Health Check

The **Resume Health Check** card continuously validates seven things:

| Check | Requirement |
|---|---|
| Name and contact details | Both fields filled |
| Summary length | 30 words or more |
| Skills listed | 6 or more |
| Work experiences | At least 2 filled roles |
| Dates on every role | Every titled role has dates |
| Achievement bullets | 2+ per role |
| Education section | At least one entry |

Aim for 7 of 7 before you print — each failed check is a common reason resumes get filtered out or skimmed past.

### 4. Preview and print to PDF

Click **Preview & Print** in the top bar. The preview shows exactly what will be printed, on your chosen paper size (US Letter or A4), with an estimated page count and total word count. Click **Print / Save PDF** and select "Save as PDF" as the destination in your browser's print dialog. All editor chrome, buttons, and backgrounds are automatically excluded from the output.

Keep it to one page where possible — the word counter makes it easy to tell when you're drifting past.

## Backup & Restore

Everything lives in your browser's local storage, which means clearing browser data also clears your resume. The **Backup** link in the footer protects you from that.

**To back up:**
1. Click **Backup** at the bottom of the editor.
2. Click **Copy JSON** — your entire resume is copied to the clipboard as readable, formatted JSON.
3. Paste it anywhere safe: a notes app, an email to yourself, a password manager, a dotfile.

**To restore:**
1. Click **Backup** (on any browser or device).
2. Paste a previously saved backup JSON into the text box.
3. Click **Apply pasted JSON** — all fields, entries, the job description, and settings are restored instantly.

The JSON is plain text and human-readable, so you can even inspect or hand-edit it if you ever need to.

## Privacy

- **Nothing is uploaded. Ever.** The file makes no network requests — there are no APIs, no analytics, no fonts fetched, no CDNs.
- All data is stored in your browser's local storage under the key `ats-resume-builder-v2`.
- Closing the tab, going offline, or using it on a plane changes nothing — it works fully offline.
- The only ways your data leave the browser are actions you take yourself: copying the backup JSON or printing to PDF.

## Tips for Beating the ATS

- **Mirror the job title.** If the posting says "Senior Project Manager", your summary should contain exactly that phrase.
- **Hard skills before soft skills** in the Skills list — scanners and recruiters both look there first.
- **Quantify everything.** "Managed a $3.2M budget with 12% cost reduction" beats "responsible for budget" every time.
- **Use the red chips as a checklist.** Each one is a keyword the posting almost certainly screens for. Add the ones that are genuinely true for you — never keyword-stuff skills you don't have.
- **Re-run the match per application.** Paste each new job description; a 90% match for one role may only be 65% for a similar-sounding one.
- **Check the health score last.** It catches the structural omissions (missing dates, thin bullets) that keyword matching can't.

## Technical Notes

- **Single file, zero dependencies.** The entire app — styles, templates, matcher, and UI — is one self-contained HTML file of roughly 40 KB with no build step.
- **Vanilla JavaScript**, no frameworks; runs in every evergreen browser (Chrome, Edge, Firefox, Safari) and adapts down to phone screens with compact icon buttons.
- **Autosave** is debounced at 250 ms; `Ctrl/Cmd + S` forces a save and suppresses the browser's own save dialog.
- **The matcher** extracts the top recurring phrases and single keywords from the job description (phrases weighted 2x), then matches them against your resume using light stemming plus built-in synonym groups — all locally, in milliseconds.
- **Printing** dynamically sets the `@page` size to match your Letter/A4 selection, and if you print straight from the editor, the app temporarily switches to the preview view so the output is always clean.
- **For developers:** the sample resume lives in the `SAMPLE` constant, the storage schema is normalized by `normalize()`, and the matcher pipeline (`computeMatch`) is a single self-contained function — easy to extend with new synonyms or checks.
