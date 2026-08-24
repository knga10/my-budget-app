# What's in index.html

A walkthrough, so you can change it with confidence instead of guessing.

## The two files, and why they're two

`data.js` sets one global, `window.DATA`. `index.html` reads it.

They're separate because **the data file is the product** and the UI is
scaffolding. Keeping them apart means you can open the CSV, check it, hand it to
someone else, or point a different UI at it.

They're loaded with a plain `<script src="data.js">` rather than `fetch()`
because `fetch()` fails when you open an HTML file directly from your desktop
(the browser blocks it). The script tag works both locally and on GitHub Pages.
This detail costs people ten minutes every single time.

## The `<head>`

**Pinned CDN versions.** `react@18.3.1`, not `@latest`. An unpinned library
shipped a breaking change once and silently broke the live Budget Buddy site.

**Babel standalone** compiles JSX in the browser, so there's no build step, no
`npm install`, no `node_modules`. On venue wifi with twenty people, this matters.

## The CSS

`--accent-a` (`#B85042`) and `--accent-b` (`#0F7BA8`) are a **validated pair**:
distinguishable under the common forms of colour blindness, and both have enough
contrast against the background. If you swap them for your own colours, check
contrast before you demo.

The `.track` and `.bar` rules set `display:block` on purpose. Generated bar-chart
code usually uses `<span>` elements, which are inline by default, and inline
elements ignore `width` and `height`. Your bars then render as nothing at all.
This is the most common invisible bug in this kind of build.

## The JSX, section by section

1. **Empty state.** While `window.DATA` is `[]`, the page says "Hello, Budget".
   That's how you confirm your GitHub Pages setup worked before the workshop.
2. **Pick one.** Buttons with `aria-pressed`, so keyboards and screen readers
   work. Selection saved in `localStorage`.
3. **Headline numbers.** Stat tiles. `ADD YOUR OTHER STAT TILES HERE`.
4. **The detail.** Empty. Your table or chart goes here.
5. **The footer.** Citation, caveat, privacy note. **Don't delete this.** It's
   the difference between a toy and something a person can trust. Replace the
   `[NAME THE EXACT TABLE AND STATEMENT]` placeholder with your real source.

## Safe to delete

The empty state once you have data, and the example stat tile.

## Not safe to delete

The pinned versions, the `display:block` rules, the `data.js` script tag, and
the footer.
