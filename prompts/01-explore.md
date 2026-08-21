# 1. Explore, before you extract anything

**Don't ask for the data on your first message.** You don't know the shape yet,
so you can't tell whether the answer is right.

Attach your statement (or the `.md` from `data/markdown/`) and paste this:

> I've attached a statement from the 2026-27 ACT Budget.
> Don't extract anything yet.
>
> 1. List every table in this document with its table number, its caption, and
>    its row and column count.
> 2. For the three biggest tables, show me the first four rows exactly as they
>    appear, including blank cells.
> 3. Tell me which table you'd pick if I wanted to build a tool that answers one
>    question for one Canberra resident, and why.

Pick your table off that list. Then confirm its shape:

> I want Table [N]. Describe its structure in plain English: what are the header
> rows, how are the rows grouped, and are there any merged cells?

**If that description doesn't match what you see in the document, stop and fix
the misunderstanding now.** It costs 30 seconds here and 15 minutes later.
