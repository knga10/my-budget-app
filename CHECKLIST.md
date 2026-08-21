# "Production ready" for today

Not enterprise-grade. This is the bar for something you'd put your name on and
send to a friend.

## Must have, before your 2 minutes

- [ ] **It's live.** A GitHub Pages URL, not localhost, not a file on your desktop
- [ ] **It opens on a phone.** You actually checked, on an actual phone
- [ ] **One user, one question, 30 seconds.** You can say the sentence out loud
- [ ] **Every number traces to a table.** Ask Claude to prove it (see `prompts/04-verify.md`)
- [ ] **Your data file is separate from your UI file.** `data.js` and `index.html`
- [ ] **The footer names the exact table and statement** your figures came from
- [ ] **A caveat.** Illustrative guide, not advice or an eligibility determination
- [ ] **No console errors.** Right click → Inspect → Console. It should be empty

## Should have

- [ ] **Any discrepancy you found is visible in the UI**, not quietly corrected
- [ ] **The year is labelled** on every figure. 2026-27 is not the same as the forward estimates
- [ ] **Colour isn't the only signal.** A dot, a label or a shape as well
- [ ] **Contrast is readable** in a bright room on a projector
- [ ] **CDN versions are pinned.** `react@18.3.1`, never `@latest`
- [ ] **No login, no backend, nothing stored off the user's browser**

## Nice to have

- [ ] Selection persists in `localStorage`
- [ ] A table view of the same data as any chart
- [ ] Keyboard navigable
- [ ] A README in your own repo saying what it is and where the data came from

## Deliberately not on this list

Tests, a build step, a framework, a domain name, analytics, a backend, a
database, auth. None of it earns its cost in two hours, and most of it never
will for a tool like this.
