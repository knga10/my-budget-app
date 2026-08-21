# Getting the data out: four routes, no Python required

**You do not need to know Python to do this workshop.** Three of the four routes
below involve no code at all, and for the Cost of Living Calculator the fastest
one is copy and paste.

Everything here was tested against the real files before it was written.

---

## Pick your route in 20 seconds

```
Is your table in the Budget Outlook (chapters 1 to 4)?
│
├── YES ──────────────────────────► ROUTE 1: the official spreadsheet
│                                   Zero extraction. Treasury already did it.
│
└── NO, it's in Statements A to H, or Cost of Living / Housing / Wellbeing / Women's / First Nations
    │
    ├── I only need one or two tables ──► ROUTE 2: copy and paste from Word
    │                                     Fastest no-code route. Works for
    │                                     almost every table in the Budget.
    │
    ├── I don't have Word, or the table is huge ──► ROUTE 3: attach the file and ask
    │                                     No code, but check the numbers.
    │
    └── I need many tables, or the same table from several files ──► ROUTE 4: let Claude run code
                                          You still write no code. Claude does.
```

---

## Route 1: Use the spreadsheet Treasury already published

**Almost nobody knows this exists.** Alongside the PDFs and Word files, ACT
Treasury publishes **"2026-27 ACT Budget tables [XLS 172 KB]"** on the
[Budget Papers and Statements page](https://www.treasury.act.gov.au/budget/budget-2026-27/budget-papers-and-statements).
It's in the repo at `data/source/ACT-Government-2026-27-Budget-tables.xlsx`.

It contains **65 tables across 14 sheets**, already as clean spreadsheet rows.
No merged-cell problems in the data. No parsing.

**For the Cost of Living Calculator, this is your route.** Both tables you need
are sitting in the sheet called `Chapter 3.3`:

- Table 3.3.1, the concessions summary (8 concession types, take-up, dollars)
- Table 3.3.2, the nine household scenarios

We checked every figure against the Word version. They match.

### What to do

1. Open the `.xlsx`. Click the `Chapter 3.3` tab. Scroll to row 13.
2. Either work in Excel directly, or attach the whole `.xlsx` to a Claude chat and say:

> I've attached the official ACT Budget tables spreadsheet.
> Look at the sheet called "Chapter 3.3". It has two tables stacked in it.
> Give me Table 3.3.2 as a CSV with one row per household per year, with the
> household name and suburb carried down as their own columns.
> Then show me the first five rows so I can check it.

That's the entire extraction step. About 90 seconds.

### What this route covers, and what it doesn't

| In the spreadsheet | Not in the spreadsheet |
|---|---|
| Economic parameters, fiscal strategy | Accountability Indicators (53 tables) |
| **Cost of living: concessions + household scenarios** | Changes to Appropriation (54 tables) |
| Revenue, rates, duty rates, Commonwealth grants | Per-directorate Infrastructure Programs |
| Expenses by function, new policy decisions | Operating statements per agency |
| Infrastructure investment program (summary level) | Anything inside Statements A to H |

So: **Cost of Living Calculator, Concession Finder and Budget Diff can start
here. Promise Tracker and What's Being Built cannot.** Those live only in the
Statements, so use Route 2.

---

## Route 2: Copy and paste the table out of Word

This is the one people don't believe works. It does, and it's better than the
obvious code approach.

### Why it works

When you copy a table in Word, the clipboard gives you one tab-separated line
per row, **with each merged cell appearing exactly once**. That is precisely the
thing that trips up naive Python parsing.

We measured the real tables. Table 3.3.2, the biggest one in the Cost of Living
Statement at 29 rows by 14 columns, comes out at **2,494 characters**. That is
a short paste. Pretty much every table in this Budget fits:

| Table | Size | Characters | Paste it? |
|---|---|---|---|
| Cost of Living, concessions (3.3.1) | 10 × 5 | 1,063 | Yes |
| Cost of Living, households (3.3.2) | 29 × 14 | 2,494 | Yes |
| Statement G, infrastructure program | 65 × 8 | 5,663 | Yes |
| Statement B, changes to appropriation | 83 × 6 | 5,126 | Yes |
| Statement H, everything | up to 32 × 6 | under 2,300 | Yes |
| Statement G, accountability indicators | 146 × 6 | 11,443 | Borderline, split it in two |

### What to do

1. Open the `.docx` in Word (or Google Docs, or Pages).
2. Hover over the table, click the small cross handle at its top-left corner to
   select the whole table. `Cmd+C`.
3. Paste straight into the Claude chat. Then:

> That's Table 3.3.2 from the 2026-27 ACT Budget Cost of Living Statement,
> pasted out of Word.
>
> The first two lines are headers. After that the rows come in groups of three:
> a household name on its own line, then its 2025-26 figures, then its 2026-27
> figures.
>
> Turn it into a CSV with one row per household per year. Carry the household
> name down into its own column, and split the suburb out of it.
> Strip the dollar signs and commas so the numbers are plain numbers.
> Treat blank cells as empty, not zero.

4. Download the CSV. Open it.

### If your table is too big to paste

Split it. Select the first half of the rows, paste, then the second half. Tell
Claude "this is part 2 of the same table, same columns". It handles it fine.

### Bonus: the Excel detour

If you'd rather have a spreadsheet at the end anyway, paste the Word table into
Excel or Google Sheets first. It splits into columns automatically. Clean it up
by hand if you like, then `File > Save As > CSV` and upload that. You get the
same result and you stay in a tool you already know.

---

## Route 3: Attach the file and just ask

No code, no copy-paste. Attach the `.docx` and ask for the table.

> I've attached the 2026-27 ACT Budget Cost of Living Statement.
> Find Table 3.3.2 and give me its contents as a CSV, one row per household
> per year.

**This works.** Claude reads the document directly. But be aware of what's
happening: it is transcribing about 250 numbers by reading them, not by
computing them. Transcription is where quiet errors come from.

**So this route is only safe if you do the check in the next section.** With the
check, it's fine. Without it, don't demo the result.

Best for: small tables, or a document you can't open in Word.

---

## Route 4: Let Claude write and run the code

You still don't write any code. Claude writes it, runs it in its own sandbox,
and hands you a file. This is on **every plan including Free**.

Worth it when you want **many tables at once**, or the same table shape pulled
from several statements. One script, 53 accountability indicator tables.

### The prompt, and the important bit about it

Here's what the earlier draft of these notes got wrong. It told you to write:

> ~~Use `row._tr.tc_lst` instead of `row.cells` so merged cells don't repeat.~~

That's a fine instruction, and it's useless to you, because if you knew to say
that you wouldn't need this guide. **You don't need to know the fix. You need to
know the check.**

Say this instead:

> Attached is the 2026-27 ACT Budget Cost of Living Statement.
> Write and run a script that extracts Table 3.3.2 to a CSV I can download.
>
> This table has merged cells and money formatted like `$29,900`, so I expect
> the first attempt to have problems. So before you show me anything:
>
> 1. Extract it.
> 2. Check your own work: for every row, does
>    `disposable income - (all the taxes) + (all the concessions)` equal the
>    published `net disposable income`?
> 3. If most rows don't reconcile, your columns are misaligned. Work out why,
>    fix it, and run it again.
> 4. Only then show me the result, and show me the reconciliation table so I
>    can see it passed.

You have described the outcome and the test. Claude works out the library
detail. That's the transferable skill, not the API name.

---

## The check that makes every route safe

Whichever route you took, run this before you build anything:

> For every row of this data, check whether
> `disposable_income - (sum of the five tax columns) + (sum of the five
> concession columns)` equals `net_disposable_income`.
> Show me all 18 rows: calculated value, published value, difference.
> Flag anything off by more than $2.

Read the result like this:

| What you see | What it means | Do this |
|---|---|---|
| Every row reconciles | Your data is right | Go build |
| One or two rows off, rest perfect | Likely an error in the published table | **Flag it in your app, don't fix it** |
| Most rows off | Your columns are shifted | Go back a step, try a different route |

When we ran this, **17 of 18 rows reconciled to the dollar**. One was out by
$899. That's a finding worth putting on screen, not a bug worth hiding.

### Finding the check for other tables

Every table has one. Look for:

- a **Total** row (Table 3.3.1 has one: does it equal the sum above it?)
- a **Change** column (does it equal this year minus last year?)
- a **Four Year Investment** column (does it equal the four year columns added up?)
- a **Total New Works** row in the infrastructure tables

If you genuinely can't find one, ask: *"what in this table should equal the sum
or difference of other parts of it?"*

---

## Which route for which idea card

| Idea card | Route | Why |
|---|---|---|
| **Cost of Living Calculator** | 1, then 2 as backup | It's in the official spreadsheet, `Chapter 3.3` |
| **Am I Missing Money?** (concessions) | 1 | Same sheet, Table 3.3.1, 8 rows |
| **Budget Diff** (new policy decisions) | 1 | Table 3.2.2, detailed initiatives by agency |
| **Promise Tracker** (indicators) | 4 | 53 tables across Statements, needs a script |
| **What's Being Built and When** | 2 | Statement G table 9, 65 rows, 5,663 chars, pastes fine |
| **Who Do I Call?** | 3 | It's prose, not tables. Just ask |
| **Housing Pathway** | 3 | Narrative statement, zero tables |
| **Wellbeing Lens** | 3 | Seven totals stated in the text |
| **Education Explainer** | 2 or 4 | Statement F, 39 tables, depends how many you want |
| **Plain English Translator** | 3 | No extraction needed at all |

---

## The one-line version

> **Check the official spreadsheet first. If it's not there, copy the table out
> of Word and paste it. If that's awkward, attach the file and ask. Only reach
> for code when you want many tables at once. Then, whatever you did, run the
> reconciliation check before you build anything.**

---

## Sources

- [Budget Papers and Statements, Budget 2026-27](https://www.treasury.act.gov.au/budget/budget-2026-27/budget-papers-and-statements): where the XLS and Word versions live
- [Create and edit files with Claude](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude): code execution is available on all plans, 30MB per file
- [Upload files to Claude](https://support.claude.com/en/articles/8241126-upload-files-to-claude)
- Table sizes and reconciliation results measured directly from the files in `budgetstatements/` and `ACT-Government-2026-27-Budget-tables.xlsx`
