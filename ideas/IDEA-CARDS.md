# Ten things you could build

Pick one. Each card names the **exact file and table**, so you don't spend ten
minutes hunting. The route column points at
[`EXTRACTING-DATA.md`](../EXTRACTING-DATA.md).

**Bring your own idea instead if you have one.** These exist so nobody stares at
a blank page at 0:35.

**Want to browse the data and find your own question?** Use
[`prompts/06-explore-the-data.md`](../prompts/06-explore-the-data.md). Give it
10 minutes, then commit to something.

---

## Easy

### 1. Cost of Living Calculator
Pick the closest of nine published household scenarios, see your net disposable
income change from 2025-26 to 2026-27, split into the five taxes and five
concessions that caused it.

- **Source:** Cost of Living Statement, Table 3.3.2 (29 x 14)
- **Route:** 1 (it's in the official spreadsheet, sheet `Chapter 3.3`)
- **Safety net:** `data/extracted/household-scenarios.csv`
- **Why it works:** already clean, 9 rows, real suburbs, and the numbers are personal
- **Worked example in this repo:** `examples/cost-of-living-calculator/`

### 2. Am I Missing Money?
Answer six questions, get the concessions you probably qualify for, with dollar
values and how many households already claim them.

- **Source:** Cost of Living Statement, Table 3.3.1 (10 x 5)
- **Route:** 1
- **Safety net:** `data/extracted/concessions.csv`
- **Why it works:** 8 rows. Highest emotional payoff per row in the whole Budget

### 3. Who Do I Call?
Type a problem in plain English, get the directorate, output class and budget
line responsible for it.

- **Source:** the "Purpose" and "Output Class" sections of any statement
- **Route:** 3 (it's prose, just ask)
- **Why it works:** mostly text matching, very demo-able, no numbers to get wrong

### 4. Housing Pathway
Renter, first home buyer, or waiting on social housing. Show only the measures
on that person's path.

- **Source:** Housing Statement (1,903 words, zero tables)
- **Route:** 3
- **Why it works:** no spreadsheet crutch, forces you to design for text

### 5. Wellbeing Lens
Show the seven budget categories mapped to wellbeing domains, and be honest
about what that framing hides.

- **Source:** Wellbeing Budget Statement, the "Wellbeing Domains" section
- **Route:** 3
- **Watch out:** these totals are quoted in **$ million** in prose, while the
  Statements are in `$'000`. Don't mix them

---

## Medium

### 6. Promise Tracker
Every accountability indicator where the 2025-26 estimated outcome missed its
target, flagged automatically.

- **Source:** 53 Accountability Indicator tables across Statements A to H
- **Route:** 4 (too many tables to paste)
- **Safety net:** `data/extracted/accountability-indicators.csv` (365 rows)
- **Watch out:** 115 rows are missing a target. That's normal, indicators get
  added and discontinued. Filter, don't assume a bug

### 7. What's Being Built, and When
A timeline of infrastructure projects by value and physical completion date.

- **Source:** Statement G Table 9 (65 rows), plus 20 more across the statements
- **Route:** 2 for one table (5,663 characters, pastes fine), 4 for all of them
- **Safety net:** `data/extracted/infrastructure-program.csv` (254 rows)
- **Why it works:** completion dates make a view nobody has published

### 8. Budget Diff
Every initiative added or removed since the 2025-26 Budget, biggest first.

- **Source:** 54 Changes to Appropriation tables, or Table 3.2.2 in the spreadsheet
- **Route:** 1 for the summary, 4 for the per-agency detail
- **Safety net:** `data/extracted/changes-to-appropriation.csv` (1,081 rows)
- **Why it works:** the negative numbers are the story and nobody reads them

### 9. Education Explainer
What the Budget funds per output class across public primary, high, secondary
college and disability education.

- **Source:** Statement F (39 tables)
- **Route:** 2 or 4
- **Why it works:** parent audience, immediate relevance

### 10. Plain English Translator
Paste any budget line or indicator, get a human explanation with a link to the
anchored source heading.

- **Source:** any statement in `data/markdown/`
- **Route:** 3, no extraction at all
- **Why it works:** almost pure prompt design. A good landing spot if the
  extraction step is stressing you out

---

## Two ideas we're asking you not to build

The **Aboriginal and Torres Strait Islander Statement** and the **Women's Budget
Statement** are in this repo and you're welcome to use them. But they are not
datasets to score or rank, and the Women's Statement case studies describe real
people.

**Present, don't rank.** Make the content findable and readable, preserve the
framing and the acknowledgements, link to the source. Don't build a relevance
score over either of them.
