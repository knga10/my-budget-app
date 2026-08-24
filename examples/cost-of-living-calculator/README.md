# Worked example: Cost of Living Calculator

A finished build of idea card 1, so you can see where you're heading. Two files,
exactly the pattern in the root `index.html` and `data.js`.

- `data.js` : 9 household scenarios from Table 3.3.2
- `index.html` : the UI

Put both in one folder and open `index.html`, or upload both to your repo.

## What it does

Pick the closest of nine published household scenarios, see net disposable
income for 2026-27 and the change on last year, broken into the five taxes and
five concessions that caused it.

## The bit worth copying

Select the **Cook** household. A data note appears saying the published figures
for 2025-26 don't reconcile, by $899.

That check runs live, on whichever household you've selected, and it isn't
hardcoded. We show the published figure and flag the gap rather than quietly
correcting it. **That's the habit to copy**, not the layout.

## The bit worth demoing

Select **Wright**: a couple buying their first house in 2026-27. Conveyance duty
goes from $0 to $48,358, and the concession cancels every dollar of it. Net
effect on the year: **+$675**. The whole stamp duty policy on one screen.

## Source

Table 3.3.2, 2026-27 ACT Budget Cost of Living Statement. Also available in
`data/source/ACT-Government-2026-27-Budget-tables.xlsx`, sheet `Chapter 3.3`.
