# 1. Get the data out

**This file has the pastes. [`EXTRACTING-DATA.md`](../EXTRACTING-DATA.md) has the
reasoning**, the evidence, and the coverage tables. If you just want to get
moving, stay here.

---

## Do you even need this file?

| You came from | Do this |
|---|---|
| **Path 3** in [`00-start-here.md`](00-start-here.md) | **Skip this file entirely.** Your data is already extracted. Go to [`02-verify.md`](02-verify.md) |
| **Path 1 or Path 2** | Pick a route below |

---

## Pick your route in 20 seconds

| | Route | Use it when | Code? |
|---|---|---|---|
| **1** | [The official spreadsheet](#route-1) | Your table is in the Budget Outlook, chapters 1 to 4 | None |
| **2** | [Copy and paste from Word](#route-2) | One or two tables from any statement | None |
| **3** | [Attach the file and ask](#route-3) | No Word, or it's prose not tables | None |
| **4** | [Let Claude run a script](#route-4) | Many tables, or one shape across many files | Claude's, not yours |

**Start at 1 and stop when one works.** Most people land on 1 or 2.

Why these four, how big each table is, and which route suits which idea card:
[`EXTRACTING-DATA.md`](../EXTRACTING-DATA.md).

---

<a id="route-1"></a>

## Route 1 · The official spreadsheet

ACT Treasury already published 65 Budget tables as a spreadsheet. It's in the
repo at `data/source/ACT-Government-2026-27-Budget-tables.xlsx`.

**Attach the `.xlsx`**, then:

> I've attached the official ACT Budget tables spreadsheet.
> Look at the sheet called "[Chapter 3.3]". It has [two] tables stacked in it.
> Give me Table [3.3.2] as a CSV with one row per [household] per [year], with
> the [household name and suburb] carried down as their own columns.
> Then show me the first five rows so I can check it.

**Doesn't repeat Statements A to H**, but it does hold whole-of-government
versions of some of their tables. Accountability indicators have no equivalent
at all. Check [`data/CROSSWALK.md`](../data/CROSSWALK.md) before you give up on
this route and start copying out of Word.

---

<a id="route-2"></a>

## Route 2 · Copy and paste out of Word

Open the `.docx` in Word, click the small cross handle at the table's top-left
to select the whole table, `Cmd+C`, and paste it straight into the chat.

**Word's clipboard resolves merged cells correctly on its own**, which is the
nastiest problem in these files, gone for free. Almost every table in this
Budget is under 6,000 characters pasted.

> That's Table [N] from [statement], pasted out of Word.
>
> The first [two] lines are headers. After that the rows come in groups of
> [three]: a [household name] on its own line, then its [2025-26] figures, then
> its [2026-27] figures.
>
> Turn it into a CSV with one row per [household] per [year]. Carry the
> [household name] down into its own column. Strip the dollar signs and commas
> so the numbers are plain numbers. Treat blank cells as empty, not zero.

**Too big to paste?** Split it. Paste the first half, then the second, saying
"this is part 2 of the same table, same columns".

---

<a id="route-3"></a>

## Route 3 · Attach the file and just ask

No code, no copy-paste. Best for **prose** (the Housing, Wellbeing, First
Nations and Women's statements have few or no tables) or a document you can't
open in Word.

**Attach the `.docx` or the `.md` from `data/markdown/`**, then:

> I've attached [statement] from the 2026-27 ACT Budget.
> Find [Table N / the section on X] and give me its contents as a CSV, one row
> per [thing].
> Keep the original wording for any labels. Don't summarise or round anything.

**This is transcription, not computation.** Claude is reading numbers off a page
rather than parsing them, which is where quiet errors come from. **Route 3 is
only safe if you run the check in [`02-verify.md`](02-verify.md).** With the
check it's fine. Without it, don't demo the result.

---

<a id="route-4"></a>

## Route 4 · Let Claude write and run a script

You still write none of it. Worth it for **many tables at once**, or the same
table shape pulled from several statements. One script, 53 indicator tables.

**Describe the outcome and the test, not the fix.** You don't need to know the
library, you need to know the check.

> Attached is [statement]. Write and run a script that extracts Table [N] to a
> CSV I can download.
>
> This table has merged cells and money formatted like `$29,900`, so I expect
> the first attempt to have problems. Before you show me anything:
>
> 1. Extract it.
> 2. Check your own work: for every row, does [the total column] equal
>    [the components added up]?
> 3. If most rows don't reconcile, your columns are misaligned. Work out why,
>    fix it, and run it again.
> 4. Only then show me the result, and show me the reconciliation table so I can
>    see it passed.

---

## Whichever route you took

**Download the file and open it.** In Excel, Numbers, anything. Looking at five
rows in the chat is not the same as seeing the file.

**Then go to [`02-verify.md`](02-verify.md).** Do not start building until the
numbers reconcile. That is the whole point of the 0:55 checkpoint.

**Stuck?** Take a pre-extracted CSV from `data/extracted/` and move on. It is a
designed shortcut, not a failure.
