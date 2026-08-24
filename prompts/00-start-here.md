# Start here

**Everyone opens this file, whatever state you're in.** Find yourself in the
table, go to that path, paste what it says.

| Where you're at | Go to |
|---|---|
| I've looked at the Budget documents **and I know what I want to build** | **[Path 1](#path-1)** |
| I've looked at the documents, **but I don't know what to build yet** | **[Path 2](#path-2)** |
| **I haven't looked at anything and I have no idea.** Just tell me what to do | **[Path 3](#path-3)** |

All three paths finish in the same place: a four-line brief and
**[the handoff](#the-handoff)**, which starts the build. **Nobody is behind.**
Path 3 is the most common at 0:25 and it's the fastest, because it does the
least deciding.

---

<a id="path-1"></a>

## Path 1 · I know what I'm building

**Attach:** your data file, or the statement it's in.

Paste this:

> I'm at a 2-hour workshop building a small civic web app from the 2026-27 ACT
> Budget. Here's my whole situation, so you don't have to ask.
>
> **What I'm building:** [one sentence. e.g. "a calculator that shows a Canberra
> household whether they're better or worse off next year"]
>
> **My data:** [e.g. "Table 3.3.2 of the Cost of Living Statement, 9 published
> household scenarios"], attached.
>
> Before we go further, in two sentences: is this actually buildable from this
> data in 45 minutes as a single HTML page, and is there anything I'd have to
> estimate or invent to make it work? Be blunt.

**Why the pushback question first.** Ninety seconds now beats discovering at
1:20 that your idea needed a number the Budget doesn't publish. If the answer
names anything you'd have to invent, adjust the idea before you continue.

Then go to **[the handoff](#the-handoff)**.

---

<a id="path-2"></a>

## Path 2 · I know my document, not my question

You've got a statement you care about. You just don't know what's in it, or
which bit would make a good tool.

**Attach:** one file from `data/markdown/` (or the original `.docx`).
**One file, not five.**

Not sure which? `data/MANIFEST.md` lists all 13. If you want a fast answer:
`01-cost-of-living.md` has the cleanest data in the Budget,
`16-statement-g-infrastructure.md` has projects with completion dates.

### Paste 1: map the document

> I've attached a statement from the 2026-27 ACT Budget.
> **Don't extract anything yet.**
>
> 1. List every table in this document: table number, caption, and its row and
>    column count.
> 2. For the three biggest, show me the first four rows exactly as they appear,
>    including blank cells.
> 3. Which table here would make the best small interactive tool for an ordinary
>    Canberra resident, and why? Judge it on: does it have a natural "pick one"
>    dimension, does it have a before and after, does it contain a number a
>    person would recognise as being about them, and is it small enough to build
>    in 45 minutes?
>
> Then stop and wait for me.

You now have a map of the document and a recommendation. Question 3 is doing the
real work: it stops you picking the biggest table instead of the most useful one.

### Paste 2: check whether your table already exists, cleanly

**Do this before you extract anything out of Word.** Some statement tables have
a whole-of-government twin in Treasury's spreadsheet, already tidy. If yours
does, you skip the messiest part of the job.

**Also attach `data/source/ACT-Government-2026-27-Budget-tables.xlsx`**, then:

> I've now also attached the official ACT Budget tables spreadsheet.
> I'm interested in Table [N] in the statement.
>
> Don't extract anything yet. Tell me:
> 1. Does the spreadsheet contain an equivalent of this table? Name the sheet and
>    table number if so.
> 2. If it does, what's **in the statement version but missing from the
>    spreadsheet version**? Be specific about columns.
> 3. Which should I extract from, and do I need both?
>
> Be honest if there is no equivalent. "No twin, use the statement" is a useful
> answer.

**The quick version, if you'd rather just look it up:**

| Your table is about | Where to get it |
|---|---|
| Households, concessions, cost of living | Spreadsheet, sheet `Chapter 3.3` |
| Money for a new initiative | Spreadsheet, **Table 3.2.2** (35 agencies) |
| Capital works dollars | Spreadsheet, **Table 3.7.2**. But **completion dates are Word only** |
| Whole-of-government financials | Spreadsheet, `Chapter 4.1` |
| What an agency **promised to deliver** | **No twin.** Word or markdown only |

Full detail, including what each twin leaves out:
[`data/CROSSWALK.md`](../data/CROSSWALK.md).

**Never add figures from both sources together.** They split the same money
differently. Pick one and say which in your footer.

### Paste 3: confirm the shape and get a brief

> Let's go with Table [N].
>
> 1. Describe its structure in plain English: what are the header rows, how are
>    the rows grouped, are there merged cells?
> 2. What would I have to estimate or invent to build a tool on it? If the answer
>    is "nothing", say so plainly.
> 3. Write me a four-line brief in this exact shape:
>    WHO the one person this is for. INPUT what they pick or tell it.
>    OUTPUT what they get back in one sentence. CONSTRAINT the one hard rule.

**If the structure description doesn't match what you see when you scroll to the
table, stop and fix that now.** Thirty seconds here saves fifteen minutes later.

Then go to **[the handoff](#the-handoff)**.

---

<a id="path-3"></a>

## Path 3 · I don't know the documents and I don't know what to build

Completely normal at 0:25, and it's the fastest path in the room because you
skip all the deciding. Here's the zero-decision version.

### Attach exactly these three files

From `data/extracted/`:

| File | Rows | What's in it |
|---|---:|---|
| `household-scenarios.csv` | 18 | 9 households, before and after |
| `infrastructure-program.csv` | 254 | Projects, dollars, completion dates |
| `accountability-indicators.csv` | 365 | What agencies promised vs delivered |

**Don't attach the statements. Don't attach the spreadsheet.** These three are
already parsed, they're small, and between them they cover money, time and
promises, which is most of what's interesting in a budget.

### Paste 1: find me something worth building

> I'm at a 2-hour workshop. In about 90 minutes I need to have shipped a small
> web app built on one slice of the 2026-27 ACT Budget. **I don't have an idea
> yet and I don't want to waste time browsing.** Help me find one, fast.
>
> I've attached three pre-extracted files from the Budget. Work only from these.
>
> Give me the **6 most interesting things** across them. For each: the finding in
> one plain sentence, the rows it comes from, and a one-line "so what" for an
> ordinary Canberra resident.
>
> Rank them by how much a resident would care, **not** by how big the numbers
> are. Skip anything that's just "this number is large".
>
> Two things about this data so you don't mislead me:
> - Rows named things like "2025-26 Budget" are baseline totals, not new
>   spending. Exclude them.
> - Rows with a name but no figures are section headings. Exclude them too.
>
> Then stop and wait for me. Don't build or extract anything yet.

### Paste 2: pick one and pressure-test it

> Number [3] interests me.
>
> 1. Show me every row it's based on, so I can see it with my own eyes.
> 2. Could I build a small single-page app around this in 45 minutes, with no
>    backend? What would I have to fabricate or estimate to make it work? If the
>    answer is "anything", say so plainly.
> 3. If it survives, write me a four-line brief in this exact shape:
>    WHO the one person this is for. INPUT what they pick or tell it.
>    OUTPUT what they get back in one sentence. CONSTRAINT the one hard rule.

**If anything has to be fabricated, pick a different finding.** Every figure has
to trace to a row.

Then go to **[the handoff](#the-handoff)**.

### Two rules for Path 3

**Ten minutes, then commit.** Set a timer. Exploring is enjoyable and it is not
a deliverable.

**If nothing has grabbed you when the timer goes, take idea card 1 or 2** from
[`ideas/IDEA-CARDS.md`](../ideas/IDEA-CARDS.md). They use the smallest, cleanest
data in the Budget and you can be building within a minute. A shipped small
thing beats an interesting unshipped thing, every time.

---

<a id="the-handoff"></a>

## The handoff · all three paths

You have a brief. Paste this and you're building.

> Good, let's build that.
>
> **What I'm shipping:** one `index.html` plus one `data.js`, React and Babel
> from CDN with pinned versions, no build step, no backend, no login. It has to
> work on GitHub Pages **and** when opened as a local file, so use a `<script>`
> tag for the data, not `fetch()`. Everything stays in the browser.
>
> **How I want to work:** four steps, and I want to approve each one before you
> move on.
> 1. Describe the structure of the data we're using. Don't extract yet.
> 2. Get it into a clean data file I can download and open.
> 3. Reconcile it: find the column that should equal the sum of other columns,
>    check every row, show me any that don't. If most rows fail, your columns are
>    misaligned, fix it and re-run rather than telling me it's fine.
> 4. Only then build the UI, against the data file, never against the source
>    document.
>
> **Non-negotiable:** every figure on screen must trace back to a specific row
> and column of the source. If you can't trace a number, don't put it on screen.
>
> Start with step 1.

**Next:** open [`01-extract.md`](01-extract.md) for the paste that gets your
data out. **Unless you took Path 3**, in which case your data is already
extracted, so skip straight to [`02-verify.md`](02-verify.md).

Then: [`03-build.md`](03-build.md) → [`04-deploy.md`](04-deploy.md).

---

## Traps in this data, whichever path you took

**Baseline rows aren't initiatives.** `changes-to-appropriation.csv` has rows
literally called "2025-26 Budget" carrying billions. Those are starting totals,
not new spending. Sort by size and they'll dominate the top and mean nothing.

**Section headings look like data.** Many rows have a name and no figures. Drop
rows where every numeric column is empty.

**Negative isn't automatically a cut.** It can be a transfer to another agency, a
technical adjustment, or a Commonwealth grant ending. Read the item name before
you call anything a cut in your demo.

**Units.** Everything except `household-scenarios.csv` is in `$'000`. A "1,400"
is $1.4 million.

**Don't rank the First Nations or Women's statements.** Read them, make them
findable, build something that helps people use them. Don't build a scoreboard
over them.

---

## If you have time to dig deeper

Only if you're ahead, or you're doing this at home afterwards. Four more prompts
that produce better ideas than the fast paths do.

**What's missing, not what's there.** Absence is more interesting than presence
and almost nobody looks for it.

> Looking at this data, what's conspicuously absent? Categories with no funding,
> indicators dropped between years, agencies that report far less than others,
> projects with no completion date.
> For each gap: is it genuinely absent, or just not in the file I gave you? Be
> strict about that distinction.

*You'll find 16 infrastructure projects with a completion date of `TBD` and 12
marked `Ongoing`. "The things government won't commit to a date on" is a good app.*

**The scoreboard.** Turns 365 rows into one number, which is usually where a
question appears.

> Using `accountability-indicators.csv`: for every indicator where both the
> 2025-26 target and the 2025-26 estimated outcome are numbers, work out whether
> the outcome met or beat the target.
> Give me the overall count, a breakdown by agency sorted by hit rate, then the
> 10 biggest misses by percentage.
> Tell me explicitly how many rows you had to exclude and why.

*Roughly 290 rows are comparable, about a third missed target, across 18
agencies. That last instruction matters: about 75 rows can't be compared, and a
scoreboard that silently drops a fifth of the data is a scoreboard that lies.*

**Follow one thread.** Pick something you personally care about.

> I care about [public transport]. Trace it through everything I've attached:
> which agencies fund it, what changed since last year, what's being built, what
> they promised to deliver.
> Then tell me the one question about it this data answers well, and one it
> obviously can't.

*The "can't" half is the useful half. It stops you promising something in your
demo that your data can't back.*

**Kill your own idea.** Once something has caught you, spend one prompt trying to
destroy it.

> I'm thinking of building: [your idea in one sentence]. Argue against it.
> Is the data actually there, or am I assuming? What would I have to fabricate?
> Is this useful to someone, or does it just look clever? Could it be read as
> taking a political position? Can it be built in 45 minutes as one HTML page?

---

## If you're behind at 0:55

Whichever path you took, say this and keep moving:

> I'm short on time. Use the pre-extracted CSV I'm attaching instead
> (`data/extracted/household-scenarios.csv`). Skip to the UI and build it.
> Note: one household's published figures don't reconcile, by $899. Show the
> published figure and flag the gap in the UI rather than correcting it.

That's not failure, it's the designed shortcut. Taking it at 0:55 means you demo.
Refusing it at 0:55 often means you don't.
