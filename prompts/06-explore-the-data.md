# 6. Explore first, decide later

**For people who don't want an idea card.** You'd rather poke around the Budget,
find something that surprises you, and build a tool around *that*.

Good instinct. It usually produces better demos, because you're building
something you actually became curious about. It also has a failure mode: you can
burn 40 minutes browsing and never build anything.

**So: 10 minutes of exploring, hard stop, then commit to one question.** Set a
timer. The prompts below are designed to get you to a decision fast.

---

## Start here: explore the pre-extracted CSVs, not the documents

The four CSVs in `data/extracted/` are already parsed, which makes them the
cheapest thing to explore. Attach one and start asking. No extraction step, no
waiting.

| File | Rows | What's in it |
|---|---:|---|
| `accountability-indicators.csv` | 365 | What 18 agencies promised to deliver, and what they actually did |
| `changes-to-appropriation.csv` | 1,081 | Every funding change since the last Budget |
| `infrastructure-program.csv` | 254 | Projects, dollar values, and physical completion dates |
| `household-scenarios.csv` | 18 | 9 households, before and after |

Attach two or three at once. They're small.

---

## Prompt 1: the surprise sweep

**Use this first.** It's the highest hit rate for finding something worth building.

> I've attached some data extracted from the 2026-27 ACT Budget.
> I don't have a question yet. I want you to help me find one.
>
> Give me the 10 most surprising or counter-intuitive things in this data.
> For each one: the finding in one sentence, the specific rows it comes from,
> and how confident you are that it's real rather than an artefact of how the
> data was extracted.
>
> Rank them by how much a Canberra resident would care, not by how big the
> numbers are.

That last line matters. Without it you get "the biggest number is big", which
is not interesting. With it you get things people would actually click on.

**Follow up on anything that catches you:**

> Tell me more about #3. Show me every row it's based on, and tell me what I'd
> need to check before I trusted it.

---

## Prompt 2: what's missing, not what's there

Absence is more interesting than presence, and almost nobody looks for it.

> Looking at this data, what's conspicuously absent?
> Categories with no funding, indicators that were dropped between years,
> agencies that report far less than others, projects with no completion date.
>
> For each gap: is it genuinely absent, or is it just not in the file I gave you?
> Be strict about that distinction.

**What you'll find:** 16 of the infrastructure projects have a completion date
of `TBD` and 12 say `Ongoing`. 75 of the 365 accountability indicators can't be
compared year to year at all. Those gaps are a real story, and "the things
government won't commit to a date on" is a genuinely good app.

---

## Prompt 3: the scoreboard

Turns 365 rows into one number, which is usually where a question appears.

> Using `accountability-indicators.csv`: for every indicator where both the
> 2025-26 target and the 2025-26 estimated outcome are numbers, work out whether
> the outcome met or beat the target.
>
> Give me: the overall count, then a breakdown by agency, sorted by hit rate.
> Then show me the 10 biggest misses by percentage.
>
> Tell me explicitly how many rows you had to exclude and why.

**What you'll find:** roughly 290 comparable rows, about a third of which missed
target, spread across 18 agencies. That last instruction matters: about 75 rows
can't be compared, and a scoreboard that silently drops a fifth of the data is a
scoreboard that lies.

---

## Prompt 4: follow one thread all the way through

Pick a thing you personally care about. Buses, schools, your suburb, housing,
the arts. Then:

> I care about [public transport]. Trace it through everything I've attached:
> which agencies fund it, what changed since last year, what's being built,
> and what they promised to deliver.
>
> Then tell me the one question about [public transport] that this data can
> answer well, and one it obviously can't. I want to know the edges.

The "one it can't answer" half is the useful half. It stops you promising
something in your demo that your data can't back.

---

## Prompt 5: find me a table shaped like a product

Sometimes the shape of the data suggests the app.

> Look across everything I've attached. Which single table or slice would make
> the best small interactive tool for a member of the public, and why?
>
> Judge it on: does it have a natural "pick one" dimension, does it have a
> before and after, does it have a number a person would recognise as being
> about them, and is it small enough to build in 45 minutes?
>
> Give me your top three with the reasoning, then recommend one.

---

## Prompt 6: pressure-test your idea before you commit

Once something has caught your interest, spend one prompt trying to kill it.

> I'm thinking of building: [your idea in one sentence].
>
> Argue against it. Specifically:
> - Is the data actually there, or am I assuming?
> - What would I have to fabricate or estimate to make this work?
> - Is this genuinely useful to someone, or does it just look clever?
> - Could it be read as taking a political position?
> - Can it realistically be built in 45 minutes as a single HTML page?
>
> Then, if it survives, write me the four-line brief: WHO, INPUT, OUTPUT,
> CONSTRAINT.

**If the answer to "what would I have to fabricate" is anything at all, change
the idea.** Every figure has to trace to a row.

---

## Traps in exploring this particular data

**The baseline rows aren't initiatives.** `changes-to-appropriation.csv` has
rows literally called "2025-26 Budget" and "2026-27 Budget" carrying figures in
the billions. Those are the starting totals, not new spending. If you sort by
size, they'll dominate the top and mean nothing. Filter them out and say so.

**Section headings look like data.** Many rows have a name and no figures,
because they're subheadings inside the original table. Drop rows where every
numeric column is empty.

**Negative isn't automatically a cut.** A negative can be a transfer to another
agency, a technical adjustment, or a Commonwealth grant ending. Read the item
name before you call anything a cut in your demo.

**Units.** Everything except `household-scenarios.csv` is in `$'000`. A "1,400"
is $1.4 million.

**Don't rank the First Nations or Women's statements.** Explore them, read them,
build something that makes them findable. Don't build a scoreboard over them.

---

## The 10-minute rule

When your timer goes, write one sentence:

> **[who] can [do what] in 30 seconds.**

If you can't finish it, take an idea card and start building. Exploring is
enjoyable and it is not a deliverable. A shipped small thing beats an
interesting unshipped thing every time.
