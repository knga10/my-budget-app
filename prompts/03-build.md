# 3. Build

## First, write the brief. Four lines, on paper.

> **WHO** the one person this is for
> **INPUT** what they pick or tell it
> **OUTPUT** what they get back, in one sentence
> **CONSTRAINT** the one hard rule

If you can't finish *"[who] can [do what] in 30 seconds"*, you're building a
dashboard nobody wants. Fix the brief before you write a build prompt.

## Then the build prompt

> Build a single `index.html` that reads the data I just extracted.
>
> Put the data in a separate `data.js` that sets `window.DATA = [...]`, loaded
> with a script tag. Not fetch(): I need it to work when opened as a local file
> AND on GitHub Pages, and I want the data file separate from the UI file.
>
> React and Babel from CDN, pinned versions, no build step, must work on
> GitHub Pages.
>
> Screens:
> 1. [pick one thing, from a list]
> 2. Three stat tiles: [name them]
> 3. [a comparison, chart or table]
> 4. A full table of every line item
>
> Use `#B85042` for [one series] and `#0F7BA8` for [the other]. Keep a legend
> visible and put a coloured dot next to each table row, so identity is never
> colour alone.
>
> Where the source publishes a figure directly, use the published figure rather
> than recomputing it, so every number on screen traces to a cell.
>
> Footer: name the exact table and statement every figure came from, link to
> treasury.act.gov.au, an illustrative-guide-not-advice caveat, and a note that
> the selection stays in the browser.

## Tips

- **Ask for screens 1 and 2 only first.** Something running in six minutes beats
  something half-built in twenty.
- **Say what not to build:** no login, no analytics, no backend, nothing stored
  outside the browser.
- **Start from `template/index.html`.** It already has the pinned CDN versions,
  the `data.js` pattern, the citation footer, and the `display:block` fix for bars.
