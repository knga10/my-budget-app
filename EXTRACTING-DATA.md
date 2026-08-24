# Getting the data out: four routes, no Python required

**You do not need to know Python to do this workshop.** Three of the four routes
below involve no code at all, and for the Cost of Living Calculator the fastest
one is copy and paste.

Everything here was tested against the real files before it was written.

> **This file is the reasoning. The pastes live in
> [`prompts/01-extract.md`](prompts/01-extract.md).**
>
> Read this once, ideally before the day, to understand why the routes exist and
> which one suits your table. On the day, work from the prompt file, so there's
> only ever one copy of each prompt to keep correct.
>
> **If you took Path 3** in `prompts/00-start-here.md`, your data is already
> extracted and you can skip this entirely.

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
2. Either work in Excel directly, or attach the whole `.xlsx` to a Claude chat.

**The paste:** [`prompts/01-extract.md` → Route 1](prompts/01-extract.md#route-1).

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
3. Paste straight into the Claude chat, then use
   **[`prompts/01-extract.md` → Route 2](prompts/01-extract.md#route-2)**.
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

**The paste:** [`prompts/01-extract.md` → Route 3](prompts/01-extract.md#route-3).

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

**The paste:** [`prompts/01-extract.md` → Route 4](prompts/01-extract.md#route-4).
It states the outcome and the test, and lets Claude correct itself.

---

## The check that makes every route safe

Whichever route you took, **run the reconciliation check before you build
anything**. It is the single step that separates a demo from something you'd put
your name on, and it's the same check for all four routes.

**The paste and how to read the result:**
[`prompts/02-verify.md`](prompts/02-verify.md).

When we ran it on Table 3.3.2, **17 of 18 rows reconciled to the dollar**. One
was out by $899. That's a finding worth putting on screen, not a bug worth
hiding.

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
