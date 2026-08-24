# Idea to Production-Ready Product

**ProductTank Canberra x Claude Community Australia**
A 2-hour workshop. Turn one slice of the 2026-27 ACT Budget into a live civic
app, using [Budget Buddy](https://knga10.github.io/civiccanberra) as the template.

You leave with a working app on your own GitHub Pages URL, and a repeatable
pattern for turning any messy pile of documents into a working tool.

---

## Start here

1. **[`SETUP.md`](SETUP.md)** : 15 minutes of pre-work. Please do this before you arrive.
2. **[`EXTRACTING-DATA.md`](EXTRACTING-DATA.md)** : four ways to get data out of these files. Three involve no code.
3. **[`ideas/IDEA-CARDS.md`](ideas/IDEA-CARDS.md)** : ten things you could build. Pick two.
4. **[`TIPS.md`](TIPS.md)** : which plan, which model, chat or Claude Code, and how to debug.

**On the day, open [`prompts/00-start-here.md`](prompts/00-start-here.md) first.**
It has three paths depending on whether you know the documents and whether you
know what you want to build. All three converge. Nobody is behind.

**You do not need to pay for anything, and you do not need to know how to code.**
A free Claude account is enough.

---

## What's in here

```
├── SETUP.md                   pre-work, 15 minutes
├── EXTRACTING-DATA.md         four routes to get data out, no Python needed
├── TIPS.md                    plan, model, tooling, and the four build stages
├── CHECKLIST.md               what "production ready" means today
│
├── data/
│   ├── MANIFEST.md            what's in all 13 statements, and the six table shapes
│   ├── source/                the official Treasury spreadsheet, 65 tables
│   ├── markdown/              all 13 statements as markdown, with heading anchors
│   └── extracted/             five pre-extracted CSVs, your safety net
│
├── index.html                 your app. This is what your live URL serves
├── data.js                    your data. Empty until you fill it
├── ANNOTATED.md               walkthrough of index.html, line by line
├── examples/                  a finished build, for reference
├── reference/budget-buddy-v1/ the app we tear down at 0:20
├── prompts/                   00-start-here, then extract, verify, build, deploy
└── ideas/IDEA-CARDS.md        ten starter ideas
```

---

## The pattern

Everything in this repo exists to get you through four steps:

> **Pick a slice → extract it to a data file → verify the data → build the UI on the file.**

Step three is the one people skip and the one that matters. There are 519 tables
in this Budget and some of them do not add up. Find that out before you demo,
not during.

---

## The day

| Time | | |
|---|---|---|
| 0:00 | Welcome, framing, pair up | 10 min |
| 0:10 | What's actually in the 13 files | 10 min |
| 0:20 | Budget Buddy teardown | 5 min |
| 0:25 | Pick your lane, scope your idea | 10 min |
| 0:35 | **Sprint 1: get the data out** | 20 min |
| 0:55 | **Data checkpoint** | 5 min |
| 1:00 | **Sprint 2: build and deploy** | 35 min |
| 1:35 | Show and tell, then wrap | 25 min |

Two hard gates: **a data file you can open by 0:55**, and **a live URL by 1:25**.
Polish comes after both.

---

## Sources and licence

All Budget content is from the
[2026-27 ACT Budget](https://www.treasury.act.gov.au/budget/budget-2026-27/budget-papers-and-statements),
published by ACT Treasury and reproduced here for a community workshop. Nothing
has been edited except format. Check the official papers before you quote a figure.

Anything you build is yours.
