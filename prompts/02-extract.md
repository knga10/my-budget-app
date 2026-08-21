# 2. Get the data out

Full routes in [`../EXTRACTING-DATA.md`](../EXTRACTING-DATA.md). Short version:
**check the official spreadsheet first, then copy-paste from Word, then just
ask, and only then reach for code.**

## Route 1, the official spreadsheet

> I've attached the official ACT Budget tables spreadsheet.
> Look at the sheet called "Chapter 3.3". It has two tables stacked in it.
> Give me Table 3.3.2 as a CSV with one row per household per year, with the
> household name and suburb carried down as their own columns.
> Then show me the first five rows so I can check it.

## Route 2, pasted out of Word

> That's Table [N] from [statement], pasted out of Word.
>
> The first [two] lines are headers. After that the rows come in groups of
> [three]: a [household name] on its own line, then its [2025-26] figures, then
> its [2026-27] figures.
>
> Turn it into a CSV with one row per [household] per [year]. Carry the
> [household name] down into its own column. Strip the dollar signs and commas
> so the numbers are plain numbers. Treat blank cells as empty, not zero.

## Route 4, let Claude run a script

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

**Whichever route you took: download the file and open it.** Looking at five
rows in the chat is not the same as seeing the file.
