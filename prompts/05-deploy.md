# 5. Deploy

**Do this at minute 20 of the 25-minute build sprint, not at the end.** If
something's broken you still have five minutes. If you deploy last, a broken
deploy means no demo.

## No git required

1. Go to your repo on github.com
2. Click **Add file** → **Upload files**
3. Drag in `index.html` and `data.js`
4. Scroll down, click **Commit changes**
5. Wait about 90 seconds
6. Open `https://YOUR-USERNAME.github.io/my-budget-app/`

## Check these two things on your phone

- The table doesn't overflow sideways
- The buttons are big enough to tap

**Only now** go back and adjust spacing and colours.

## If it 404s

- Wait another minute. First publish is slow.
- Check **Settings → Pages** says "Your site is live at ...".
- Check your file is called `index.html`, lowercase. GitHub Pages is
  case-sensitive even though your Mac isn't. This catches somebody every year.
- Check your links are relative (`./data.js`), not absolute (`/data.js`).
  Pages serves from `/your-repo-name/`, not from `/`.
