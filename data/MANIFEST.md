# What's in these files

Everything here came from the [official 2026-27 ACT Budget papers](https://www.treasury.act.gov.au/budget/budget-2026-27/budget-papers-and-statements).
Nothing has been edited except format.

## The 13 statements, as markdown

Converted from the official Word versions. Every heading has an HTML anchor, so
you can link a figure straight to the paragraph it came from, the way Budget
Buddy v1 does.

| File | Statement | Words | Tables | Table rows | What it's good for |
|---|---|---:|---:|---:|---|
| [`01-cost-of-living.md`](markdown/01-cost-of-living.md) | Cost of Living Statement | 2,514 | 2 | 39 | **Best place to start.** 9 household scenarios by suburb, 8 concession types with dollar values |
| [`02-housing.md`](markdown/02-housing.md) | Housing Statement | 1,903 | 0 | 0 | Narrative only. 30,000 homes by 2030, stamp duty, Build-to-Rent, Missing Middle |
| [`03-wellbeing.md`](markdown/03-wellbeing.md) | Wellbeing Budget Statement | 3,488 | 2 | 2 | Seven category totals stated in prose, mapped to wellbeing domains |
| [`04-womens.md`](markdown/04-womens.md) | Women's Budget Statement | 5,437 | 5 | 5 | Four pillars, case studies. Present, don't rank |
| [`05-first-nations.md`](markdown/05-first-nations.md) | Aboriginal and Torres Strait Islander Statement | 3,083 | 0 | 0 | Narrative. Present, don't rank |
| [`10-statement-a-executive-and-offices.md`](markdown/10-statement-a-executive-and-offices.md) | Statement A | 3,668 | 41 | 580 | Executive, Integrity Commission, Auditor-General, Electoral Commission |
| [`11-statement-b-cmtedd.md`](markdown/11-statement-b-cmtedd.md) | Statement B | 48,198 | 169 | 2,477 | The biggest file. CMTEDD plus 12 authorities: CIT, City Renewal, Icon Water, ICRC |
| [`12-statement-c-health-and-community.md`](markdown/12-statement-c-health-and-community.md) | Statement C | 17,190 | 119 | 1,157 | Canberra Health Services, Housing ACT, ACT Local Hospital Network |
| [`13-statement-d-justice.md`](markdown/13-statement-d-justice.md) | Statement D | 12,230 | 66 | 892 | Justice and Community Safety, Legal Aid, Public Trustee |
| [`14-statement-e-city-and-environment.md`](markdown/14-statement-e-city-and-environment.md) | Statement E | 12,772 | 41 | 639 | Transport Canberra, Suburban Land Agency, Gambling and Racing |
| [`15-statement-f-education.md`](markdown/15-statement-f-education.md) | Statement F | 6,624 | 39 | 481 | Primary, high, secondary college and disability education outputs |
| [`16-statement-g-infrastructure.md`](markdown/16-statement-g-infrastructure.md) | Statement G | 3,325 | 14 | 413 | **65-row infrastructure program table** with physical completion dates |
| [`17-statement-h-digital.md`](markdown/17-statement-h-digital.md) | Statement H | 3,300 | 21 | 228 | Small and clean. Good file for a first pass |
| | **Total** | **123,732** | **519** | **6,913** | |

## The 519 tables come in only six shapes

Write one parser and it works across all 13 files.

| Table type | Count | Shape |
|---|---:|---|
| Changes to Appropriation | 54 | Initiative name x 5 years, `$'000` |
| Accountability Indicators | 53 | Indicator x (25-26 target, 25-26 outcome, 26-27 target) |
| Operating Statement | 52 | Standard financials |
| Cash Flow | 44 | Standard financials |
| Balance Sheet | 29 | Standard financials |
| Infrastructure Program | 21 | Project x value x year splits x completion date |

## `source/` : the official spreadsheet

`ACT-Government-2026-27-Budget-tables.xlsx` is Treasury's own published
spreadsheet, **65 tables across 14 sheets**, already clean. Almost nobody opens
it. **Check here before you extract anything.**

It covers the Budget Outlook (chapters 1 to 4), including Table 3.3.1 and
Table 3.3.2 on the sheet `Chapter 3.3`.

**It does not repeat Statements A to H, but it does contain whole-of-government
versions of some of their tables.** Which ones, and what each version leaves
out, is in [`CROSSWALK.md`](CROSSWALK.md). Worth two minutes before you extract
anything out of Word.

## `extracted/` : pre-extracted CSVs, your safety net

If you get stuck at the data checkpoint, use these and keep building.
See [`extracted/README.md`](extracted/README.md) for row counts and the
reconciliation report for each one.

## The original Word and PDF files

Not in this repo, to keep it small. Download them from the
[Budget Papers and Statements page](https://www.treasury.act.gov.au/budget/budget-2026-27/budget-papers-and-statements)
if you want to copy tables straight out of Word (which is
[Route 2](../EXTRACTING-DATA.md) and often the fastest thing you can do).
