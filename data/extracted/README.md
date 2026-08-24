# Pre-extracted CSVs

Your safety net. If you're stuck at the 0:55 data checkpoint, grab one of these
and keep building.

**Read the reconciliation column before you trust a file.** We ran the check on
each one and we're telling you what we found, including where it isn't clean.
That's the habit we want you to copy.

| File | Rows | Source | Reconciliation |
|---|---:|---|---|
| `household-scenarios.csv` | 18 | Cost of Living Statement, Table 3.3.2 | **17 of 18 rows reconcile to the dollar.** One does not, see below |
| `concessions.csv` | 9 | Cost of Living Statement, Table 3.3.1 | 8 concession types plus a Total row. Total matches the sum |
| `infrastructure-program.csv` | 254 | 21 Infrastructure Program tables, Statements A to H | **178 of 182 checkable rows reconcile.** 4 do not, see below |
| `accountability-indicators.csv` | 365 | 53 Accountability Indicator tables, Statements A to H | No arithmetic check possible. 115 rows are missing a target, which is normal: indicators get added and discontinued |
| `changes-to-appropriation.csv` | 1081 | 54 Changes to Appropriation tables, Statements A to H | Not reconciled. Many rows are section headings with no figures. Filter those out before you sum anything |

---

## The known discrepancies

### `household-scenarios.csv`, the Cook household, 2025-26

The published net disposable income is **$56,300**. The components
(`disposable_income - taxes + concessions`) sum to **$55,401**. A gap of **$899**.

The 2026-27 row for the same household reconciles to the dollar, so this is not
a column-alignment problem in our extraction.

**We have not corrected it.** The CSV carries the published figure. If you build
on this data, show the published number and flag the gap. That decision is the
difference between a demo and something people can trust.

### `infrastructure-program.csv`, 4 rows

Four project rows have a `four_year_investment` that doesn't equal the sum of
the four year columns. These are tables where the column count differs slightly
from the dominant shape, so a value has landed one column off. Spot them with:

```
four_year_investment != spend_2026_27 + spend_2027_28 + spend_2028_29 + spend_2029_30
```

Drop them, or go back to the markdown and read those four rows by hand.
Don't silently include them in a total.

---

## Columns

Money is in **`$'000`** in every file except `household-scenarios.csv`, which is
in **whole dollars**, because that's how the source table publishes it. Each file
that uses thousands carries a `unit` column so you can't lose track.

Every file carries `statement`, `agency`, `table` and `caption` columns so you
can trace any row back to the exact table it came from. Keep those columns in
your app, they're how you build a citation.

---

## Rerun the check yourself

> For every row of this CSV, check whether [the total column] equals the sum of
> [the component columns]. Show me all rows with the calculated value, the
> published value, and the difference. Flag anything off by more than $2.
