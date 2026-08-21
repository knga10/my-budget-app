# 0. The kickoff paste

**Paste this as your very first message.** It replaces three or four rounds of
context-setting, which matters on a free account where usage is finite and you
have 50 minutes of build time.

Fill in the two brackets, attach your file, send.

---

> I'm at a 2-hour workshop building a small civic web app from the 2026-27 ACT
> Budget. Here's my whole situation, so you don't have to ask.
>
> **What I'm building:** [one sentence. e.g. "a calculator that shows a Canberra
> household whether they're better or worse off next year"]
>
> **My data:** [e.g. "Table 3.3.2 of the Cost of Living Statement, 9 published
> household scenarios"], attached.
>
> **What I'm shipping:** one `index.html` plus one `data.js`, React and Babel
> from CDN with pinned versions, no build step, no backend, no login. It has to
> work on GitHub Pages and when opened as a local file, so use a `<script>` tag
> for the data, not `fetch()`. Everything stays in the browser.
>
> **How I want to work:** four steps, and I want to approve each one before you
> move on.
> 1. Describe the structure of my data. Don't extract yet.
> 2. Extract it to a CSV I can download.
> 3. Reconcile it: find the column that should equal the sum of other columns,
>    check every row, and show me a table of any that don't. If most rows fail,
>    your columns are misaligned, fix it and re-run rather than telling me it's fine.
> 4. Only then build the UI, against the data file, never against the source document.
>
> **Non-negotiable:** every figure on screen must trace back to a specific row
> and column of the source table. If you can't trace a number, don't put it on
> screen.
>
> Start with step 1.

---

## Why it's shaped like that

- **It states the constraints once**, so you don't re-litigate "no build step"
  four times.
- **It names the four steps and asks for approval between them**, which stops
  Claude racing to a finished app before the data is right.
- **It pre-loads the reconciliation check**, so the most important step happens
  by default instead of being remembered.
- **It says what to do when the check fails**, which is the difference between
  a self-correcting loop and a confident wrong answer.

## If you're behind at 1:05

Say this and keep moving:

> I'm short on time. Use the pre-extracted CSV I'm attaching instead
> (`data/extracted/household-scenarios.csv`). Skip to step 4 and build the UI.
> Note: one household's published figures don't reconcile, by $899. Show the
> published figure and flag the gap in the UI rather than correcting it.
