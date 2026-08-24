# Tips and tricks

How to get from a 100-page Word document to a working app without burning your
two hours. Every section has a **Start here** (novice) and a **Go further**
(intermediate) track. Do the novice track even if you're experienced, it's fast.

---

## Before anything: plan, model, and where to work

### Do I need Pro?

**No. The whole workshop runs on a free account.** The two things you need,
file uploads and code execution, are on every plan.

| | Free | Pro ($20/mo, $17/mo billed annually) |
|---|---|---|
| Upload a .docx and ask questions about it | Yes | Yes |
| Run Python on it and download a CSV | Yes | Yes |
| Build and preview HTML in the chat | Yes | Yes |
| Models | Haiku 4.5, Sonnet 5 | adds Opus 5 and Fable 5 |
| Usage per session | baseline | at least 5x |
| **Projects** (persistent uploaded files across chats) | **No** | Yes |
| **Claude Code** (terminal) | **No** | Yes |
| Cowork | No | Yes |

**What you actually lose on free:** Projects and Claude Code, plus you'll hit
usage limits sooner. Neither is fatal today. You just attach the .docx to a
normal chat instead of parking it in a Project.

**One free-account habit that matters:** you have no Projects, so a chat is
your only memory. Do all four stages in **one long chat**. If you start a fresh
one, you have to re-upload and re-explain, and that's how people run out of
usage at minute 80.

### Which model?

| Model | Use it for | Plan |
|---|---|---|
| **Sonnet 5** | **Your default today.** Writing the parser, building the HTML, debugging | Free |
| Haiku 4.5 | Quick lookups, "what's in this file", renaming columns | Free |
| Opus 5 | When Sonnet has failed the same bug twice and you need it to actually think | Pro |
| Fable 5 | Reading dense source material end to end, the hardest extraction jobs | Pro |

**Practical rule:** start on Sonnet and stay there. It's the recommended model
for coding, it's fast enough to iterate against, and fast iteration beats a
smarter slower answer when you're on a clock. If you're on Pro and you're
stuck on the same error for a third time, switch to Opus for that one message,
then switch back.

Don't burn Opus or Fable on the build. Burn it on the stuck moment.

### Claude Code or chat?

**Use chat today. Both novice and intermediate.**

The honest comparison:

| | Chat (claude.ai or Desktop) | Claude Code (terminal) |
|---|---|---|
| Setup cost | zero | Node install, terminal, Pro plan |
| Sees your uploaded .docx | yes, drag and drop | yes, it's a file on disk |
| Runs the extraction script | yes, in its own sandbox | yes, on your machine |
| Fixes its own script after an error | you paste the error back | **it reads the error and retries by itself** |
| Previews your HTML | yes, renders inline | no, you open the file yourself |
| Right for | 2 files, 2 hours | 20 files, a repo, git |

Claude Code is genuinely better at the extract-verify-fix loop, because it runs
the script, reads the traceback, and fixes it without you in the middle. That
is a real advantage and it is **not worth a 20 minute install today**. Today's
deliverable is two files uploaded through a web form.

**If you already have Claude Code installed and you're on Pro, use it.** You'll
be about 10 minutes faster in Stage 2. Everyone else: chat.

Take Claude Code home. It's the right tool for version 2 of whatever you build.

---

## Stage 1: Analyse before you extract

The mistake everyone makes is asking for the data on the first message. You
don't yet know what shape it is, so you can't tell whether the answer is right.

### Start here

Attach the .docx and ask this, exactly. Do not ask for data yet.

> I've attached a statement from the 2026-27 ACT Budget.
> Don't extract anything yet.
>
> 1. List every table in this document with its table number, its caption, and
>    its row and column count.
> 2. For the three biggest tables, show me the first four rows exactly as they
>    appear, including blank cells.
> 3. Tell me which table you'd pick if I wanted to build a tool that answers
>    one question for one Canberra resident, and why.

You now have a map. Pick your table off that list.

**Then confirm the shape before you spend a prompt on code:**

> I want Table 3.3.2. Describe its structure in plain English: what are the
> header rows, how are the rows grouped, and are there any merged cells?

If that description doesn't match what you see when you scroll to the table in
Word, stop. Fix the misunderstanding now. It costs 30 seconds here and 15
minutes later.

### Go further

- **Ask what's missing.** "Which columns in this table are derived from other
  columns? Which ones are totals?" Derived columns are your free correctness
  check in Stage 4.
- **Ask what could go wrong.** "If I asked you to parse this table with
  python-docx, what would break?" Claude will usually name the merged cells
  itself, and now it's in the conversation, so the next prompt inherits it.
- **Scan across statements.** The 519 tables in this Budget come in only six
  shapes. If your table is a "Changes to Appropriation" or "Accountability
  Indicators" table, there are 50-odd more just like it. Ask: "does this same
  table shape appear in the other statements?" One parser, many files.

---

## Stage 2: Get the data out

**The target by 0:55 is a file you can open.** Not a UI. A CSV or a JSON.

**You do not need to know Python for this.** Full routes are in
[`EXTRACTING-DATA.md`](EXTRACTING-DATA.md). The short version:

| Route | When | Code? |
|---|---|---|
| **1. The official spreadsheet** | Your table is in the Budget Outlook, chapters 1 to 4 | None |
| **2. Copy and paste from Word** | One or two tables from any statement | None |
| **3. Attach the file and ask** | No Word, or it's prose not tables | None |
| **4. Let Claude write and run a script** | Many tables, or one shape across many files | Claude's, not yours |

### Start here

**Check Route 1 first.** ACT Treasury publishes a spreadsheet of 65 Budget
tables that almost nobody opens. If your table is in there, your extraction step
is over before it started. **Table 3.3.2, the household scenarios, is in there**,
on the sheet called `Chapter 3.3`.

**If it's not, use Route 2.** Open the .docx in Word, click the handle at the
table's top-left to select the whole table, copy, and paste it straight into the
chat. Table 3.3.2 is only 2,494 characters pasted. Word's clipboard resolves
merged cells correctly on its own, which is the single nastiest problem in these
files, gone for free.

Then:

> That's Table 3.3.2 from the 2026-27 ACT Budget Cost of Living Statement,
> pasted out of Word.
>
> The first two lines are headers. After that the rows come in groups of three:
> a household name on its own line, then its 2025-26 figures, then its 2026-27
> figures.
>
> Turn it into a CSV with one row per household per year. Carry the household
> name down into its own column, and split the suburb out of it. Strip the
> dollar signs and commas. Treat blank cells as empty, not zero.

**Then download the CSV and open it in Excel or Numbers.** Actually open it.
Looking at five rows in the chat is not the same as seeing the file.

### Describe the outcome and the test, not the fix

If you do use Route 4, don't try to give Claude library instructions you'd have
to look up. Give it the check instead, and let it correct itself:

> This table has merged cells and money formatted like `$29,900`, so I expect
> the first attempt to have problems. Before you show me anything:
> extract it, then check that for every row
> `disposable income - (all the taxes) + (all the concessions)` equals the
> published `net disposable income`. If most rows don't reconcile, your columns
> are misaligned. Work out why, fix it, run it again. Only then show me the
> result, with the reconciliation table so I can see it passed.

**You don't need to know the fix. You need to know the check.** That habit
transfers to every messy document you'll ever be handed.

### Go further

- **Give it a schema up front.** Naming your columns in the prompt beats
  renaming them after. `id, suburb, household, year, disposable_income, ...`
- **Ask for JSON too, in the shape your UI wants.** A flat CSV is right for
  checking. A nested object keyed by household is right for rendering. Ask for
  both, they're the same prompt.
- **Keep the raw column order.** If you tell it to reorder or prettify columns
  in the same step as extracting, you lose the ability to diff against the
  source table by eye.
- **Write the parser to be reusable.** "Make the table number and output
  filename command-line arguments" turns 20 minutes of work into a tool you can
  point at Statement C after lunch.

### Two traps specific to these files

1. **Units.** Statements A to H are in `$'000`. The Wellbeing and Housing
   statements quote `$ million` in prose. Put a `unit` column in your data file
   so this can never silently bite you.
2. **Forward estimates.** Most tables show 2026-27 plus 2027-28, 2028-29 and
   2029-30 estimates. Never add all four together and call it "the Budget".
   Label the year on every figure you display.

---

## Stage 3: Structure the prompt

### Start here: the four-line brief

Before you ask for a build, write this out. It fits on an index card.

> **WHO** the one person this is for
> **INPUT** what they tell it, or pick
> **OUTPUT** what they get back, in one sentence
> **CONSTRAINT** the one hard rule

Worked example:

> **WHO** a Canberra pensioner who saw a Budget headline and wants to know if
> they're better or worse off.
> **INPUT** which of the nine published household scenarios is closest to them.
> **OUTPUT** their net disposable income change, broken into the taxes and
> concessions that caused it.
> **CONSTRAINT** one index.html plus one data file, no backend, no build step.

Then the build prompt. Four things it must contain:

1. **Point it at the data file, never the source document.** "Use the CSV I
   just made" not "use the Budget statement".
2. **Name the screens as a numbered list.** Vague requests produce vague apps.
3. **State the deploy target.** "Single index.html, React and Babel from CDN
   with pinned versions, no build step, must work on GitHub Pages."
4. **Ask for the citation.** "Footer must name the exact table and statement
   every figure came from, and link to treasury.act.gov.au."

### Go further

- **Constrain the file layout explicitly.** Say: "put the data in a separate
  `data.js` that sets `window.HOUSEHOLDS = [...]`, loaded with a script tag.
  Not `fetch()`." `fetch()` fails when you open the file locally, and someone
  in the room will lose ten minutes to that.
- **Pin your CDN versions.** `react@18.3.1`, not `react@latest`. An unpinned
  library shipped a breaking change and silently broke the live Budget Buddy
  site once already.
- **Ask for one screen, then extend.** "Build screens 1 and 2 only" gets you
  something running in 6 minutes. You can always add screen 3.
- **Give it your colours and let it handle contrast.** "Use `#B85042` for costs
  and `#0F7BA8` for relief, keep a legend visible, and put a coloured dot next
  to each table row so identity is never colour alone." Accessible by
  construction beats a retrofit.
- **Say what NOT to build.** "No login, no analytics, no backend, nothing
  stored outside the browser." This prevents helpful scope creep.

---

## Stage 4: Debug and test

This is the stage people skip, and it's the one that separates a demo from
something you'd put your name on.

### Start here: the reconciliation check

Every good table has a number that should equal the sum of other numbers. Find
it and check it.

> For every row in this CSV, check whether
> `disposable_income - (sum of the 5 tax columns) + (sum of the 5 concession
> columns)` equals `net_disposable_income`.
> Print all 18 rows with the calculated value, the published value, and the
> difference. Flag anything off by more than $2.

Three possible outcomes, and you need to know which one you're in:

| Result | What it means | What to do |
|---|---|---|
| All rows reconcile | Your extraction is correct | Move on, confidently |
| Most reconcile, one or two don't | Probably an error in the published table | **Flag it in the UI, don't fix it** |
| Nothing reconciles | Your columns are shifted | Go back to Stage 2 |

The middle case actually happened when we tested this: 17 of 18 rows
reconciled to the dollar and one was out by $899. That's a finding, not a bug.
Show the published figure, show the gap, tell people to check the source.

### Start here: the traceability check

Last prompt before you demo, always:

> List every dollar figure that appears in my index.html and tell me which row
> and column of the source table each one came from. Flag any figure you can't
> trace.

If Claude can't trace a number, neither can you, and you're about to say it out
loud to a room.

### Start here: when something doesn't work

Don't say "it's broken". Say:

> The bar rows render their labels and dollar values but the coloured bars are
> invisible. Here's the CSS and the JSX for that component. [paste both]

Three ingredients: **what you expected, what you got, the relevant code.** That
turns a 5-message guessing loop into one answer. (The real fix for that one:
the bars were `<span>` elements, which are inline by default, so width and
height don't apply.)

If you're getting a blank white page, open the browser console (right click →
Inspect → Console) and paste the red text. That's usually the whole answer.

### Go further

- **Test the edges before you demo.** Which household has the biggest number?
  The smallest? A zero? A negative? Click all of them. In our test, one
  household had a $48,358 conveyance duty fully cancelled by a $48,358
  concession, and it looked broken until we read it properly.
- **Test on your phone, not the laptop.** Open your live GitHub Pages URL on
  your phone before you polish anything. Tables overflow sideways and buttons
  get too small, and you won't see either at 1440px.
- **Deploy at 1:25, not at the end of the sprint.** Upload to GitHub, wait 90
  seconds, load the URL. If something's broken you still have five minutes.
  If you deploy last, a broken deploy means no demo.
- **Ask Claude to critique it.** "You're a Canberra resident with no budget
  knowledge who has 30 seconds. What's confusing about this screen?" It's
  better at this than you'd expect and it's free.
- **Watch for the wrong kind of confidence.** If Claude produces a number that
  isn't in your data file, it invented it. Data file in, data file out, always.

---

## The one-page cheat sheet

**Setup**
- Free account is enough. Sonnet 5 is your model. Work in chat, one long chat.

**The loop**
1. Map the tables. Don't extract yet.
2. Confirm the table's shape in plain English before extracting anything.
3. Extract: official spreadsheet first, else copy-paste from Word, else ask,
   else let Claude run a script. No Python needed.
4. **Download and open the file.**
5. Reconcile: does the total equal the sum of its parts?
6. Write the four-line brief: WHO, INPUT, OUTPUT, CONSTRAINT.
7. Build against the data file, never the source document.
8. Deploy. Then polish.
9. Trace every number back to a table cell before you demo.

**Say this, not that**
- "Don't extract yet, describe the structure" > "give me the data"
- "Here's what I expected, what I got, and the code" > "it's broken"
- "Use the CSV I just made" > "use the Budget statement"
- "Build screens 1 and 2 only" > "build the app"

**Three things that will cost you ten minutes each if nobody warned you**
- Merged cells silently shifting your columns (copy-paste from Word avoids this entirely)
- `fetch()` failing when you open the HTML as a local file
- Bars, icons or dividers not showing because a `<span>` is inline by default

---

## Sources

- [Plans and pricing](https://claude.com/pricing): what Free vs Pro includes
- [Choose a Claude plan](https://support.claude.com/en/articles/11049762-choose-a-claude-plan)
- [Use Claude Code with your Pro or Max plan](https://support.claude.com/en/articles/11145838-use-claude-code-with-your-pro-or-max-plan)
- [Create and edit files with Claude](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude): code execution is on all plans
- [Upload files to Claude](https://support.claude.com/en/articles/8241126-upload-files-to-claude): 20 files per chat, .docx supported
- [Choosing the right Claude model](https://claude.com/resources/tutorials/choosing-the-right-claude-model)
- [Models overview](https://platform.claude.com/docs/en/about-claude/models/overview)
