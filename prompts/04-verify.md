# 4. Verify, before you demo

## The reconciliation check

Every good table has a number that should equal the sum of other numbers.

> For every row of this data, check whether [the total column] equals
> [the components added up]. Show me all rows with the calculated value, the
> published value, and the difference. Flag anything off by more than $2.

| Result | Meaning | Do this |
|---|---|---|
| All rows reconcile | Extraction is correct | Go build |
| One or two off, rest perfect | Likely an error in the published table | **Flag it in the app, don't fix it** |
| Most rows off | Your columns are shifted | Go back and try another route |

## The traceability check

Last prompt before you demo. Always.

> List every dollar figure that appears in my index.html and tell me which row
> and column of the source table each one came from. Flag any figure you can't
> trace.

**If Claude can't trace a number, neither can you**, and you're about to say it
out loud to a room.

## When something's broken

Don't say "it's broken". Say:

> [What I expected]. [What actually happens]. Here's the relevant code: [paste]

Three ingredients: expected, actual, code. That turns a five-message guessing
loop into one answer.

Blank white page? Right click → Inspect → Console, and paste the red text.
That's usually the whole answer.

## Test the edges

- Which option has the biggest number? The smallest? A zero? A negative?
- Click every one of them before you demo.
- Open it **on your phone**, not just the laptop.
