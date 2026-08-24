# 4. Deploy

**Deploy at 1:25, with ten minutes of the build sprint still to run.** Not at
the end. If something's broken you still have time to fix it. If you deploy
last, a broken deploy means no demo.

## No git required

1. Go to your repo on github.com
2. Click **Add file** → **Upload files**
3. Drag in `index.html` and `data.js`. **Drop them at the repo root**, the same
   place the existing ones are. Not in a subfolder
4. It will ask if you want to replace the existing files. Yes
5. Scroll down, click **Commit changes**
6. Wait about 90 seconds
7. Open `https://YOUR-USERNAME.github.io/my-budget-app/`

## Check these two things on your phone

- The table doesn't overflow sideways
- The buttons are big enough to tap

**Only now** go back and adjust spacing and colours.

## If it says "no data" after you just uploaded data.js

**Hard refresh. `Cmd+Shift+R` on Mac, `Ctrl+Shift+R` on Windows.**

This catches almost everyone, once. Your browser cached the empty `data.js`
from the pre-work, and your filename hasn't changed, so it happily serves you
the old one alongside your new `index.html`. The result looks exactly like your
data failed to load.

**Check it properly before you debug anything else:** open
`https://YOUR-USERNAME.github.io/my-budget-app/data.js` directly. If you can see
your own rows in it, the file is fine and it was only the cache.

## If it 404s

- Wait another minute. First publish is slow.
- Check **Settings → Pages** says "Your site is live at ...".
- Check your file is called `index.html`, lowercase. GitHub Pages is
  case-sensitive even though your Mac isn't. This catches somebody every year.
- Check your links are relative (`./data.js`), not absolute (`/data.js`).
  Pages serves from `/your-repo-name/`, not from `/`.
