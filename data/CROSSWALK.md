# Does my statement table have a twin in the spreadsheet?

**Read this before you extract anything out of Word.** Some of the tables in
Statements A to H already exist, in clean spreadsheet form, in
`source/ACT-Government-2026-27-Budget-tables.xlsx`. Not as a copy of the same
table, but as the **whole-of-government version of the same numbers**.

If yours has a twin, you can skip the messiest part of the extraction.

---

## The crosswalk

| Your statement table | Twin in the spreadsheet | What the twin gives you | What you lose |
|---|---|---|---|
| **Changes to Appropriation** (54 tables) | **Table 3.2.2**, sheet `Chapter 3.2`, "Detailed initiatives by lead agency" | Every new initiative, grouped under 35 agency headings, split Net cost / Net capital, four years | The technical adjustments, rollovers and transfers. The statement version has those, 3.2.2 only has new policy decisions |
| **Infrastructure Program** (21 tables) | **Table 3.7.2**, sheet `Chapter 3.7`, "Summary of GGS Capital Works Program by agency" | New Capital Works / Asset Renewal / Works-in-progress per agency, four years | **Physical completion dates.** Those only exist in the statement. If your idea is about *when* things finish, you need Word |
| **Operating Statement, Balance Sheet, Cash Flow** (125 tables) | **Chapter 4.1**, Tables 4.1.1 to 4.1.19 | The same line items at whole-of-government level | Per-agency detail. 4.1 is the aggregate only |
| **Accountability Indicators** (53 tables) | **None. There is no twin.** | | Nothing to lose. The spreadsheet contains zero mentions of accountability indicators. Word or the markdown is your only source |
| **Cost of Living Statement** tables | **Tables 3.3.1 and 3.3.2**, sheet `Chapter 3.3` | Both tables complete and identical to the Word version | Nothing. Use the spreadsheet |

We checked the overlap rather than assuming it. **82 initiative names in Table
3.2.2 match, word for word, items in the statements' Changes to Appropriation
tables.** Same initiatives, cleaner container.

---

## How to decide, in 30 seconds

```
Is your table about ...
│
├── a household, a concession, or cost of living  ──► Chapter 3.3.  Use the spreadsheet.
│
├── money given to a NEW initiative               ──► Table 3.2.2.  Use the spreadsheet,
│                                                     then Word only if you need
│                                                     rollovers and transfers too.
│
├── capital works spending by agency              ──► Table 3.7.2 for the dollars,
│                                                     Word for completion dates.
│
├── whole-of-government financials                ──► Chapter 4.1.
│
└── what an agency PROMISED to deliver            ──► No twin. Word or markdown only.
```

---

## The paste that answers it for you

Attach **both** the spreadsheet and your statement (or its `.md`), then:

> I've attached two things: the official ACT Budget tables spreadsheet, and
> [statement name] from the 2026-27 ACT Budget.
>
> I'm interested in [Table N / the topic] in the statement.
>
> Don't extract anything yet. Tell me:
>
> 1. Does the spreadsheet contain an equivalent of this table? Name the sheet and
>    the table number if so.
> 2. If it does, what's **in the statement version but missing from the
>    spreadsheet version**? Be specific about columns.
> 3. Given that, which should I extract from, and do I need both?
>
> Be honest if there is no equivalent. Saying "no twin, use the statement" is a
> useful answer.

**Why question 2 is the important one.** The spreadsheet is almost always
cleaner and almost always less detailed. The trade is real, and you want to make
it on purpose rather than discover it at 1:10 when the column you needed isn't
there.

---

## The trap this exists to prevent

The spreadsheet is grouped **by agency**, and the statements are **one file per
agency group**. So the same initiative appears in both, with the same name, and
it's easy to assume they carry the same columns.

They don't. Table 3.2.2 splits every initiative into **Net cost** and **Net
capital** rows. The statement's Changes to Appropriation table splits by
**appropriation type** (Controlled Recurrent Payments, Capital Injections,
Expenses on Behalf of the Territory) across separate tables.

**Do not add figures from the two sources together.** Pick one, say which one
you used in your footer, and stay there.
