# project cards

The project cards on the profile README are generated from this folder.

```
cards/
  projects.json   every project: name, one-liner, link, size, screenshot, colors
  shots/          source screenshots (any size; they're cropped to fit)
  fonts/          Geist, vendored so renders match on every machine
  png/            baked cards (2x). the README points here. don't hand-edit.
  og/             1280x640 social previews (node cards/build.mjs --og), uploaded in each repo's Settings → Social preview
  build.mjs       renders png/ and rewrites the README block
```

## add a project

1. Drop a screenshot in `shots/` (a real interface beats a logo).
2. Add an entry to the right section in `projects.json`:

   ```json
   {
     "id": "my-thing",
     "name": "My Thing",
     "line": "I needed to … (one line, the problem it solves)",
     "href": "https://github.com/codyhxyz/my-thing",
     "site": "mything.codyh.xyz",
     "status": "live",
     "size": "full",
     "shot": "my-thing.jpg",
     "focus": "70% 40%",
     "theme": { "bg": "#101418", "ink": "#eef2f6", "acc": "#5fb3ff" }
   }
   ```

3. `node cards/build.mjs` (or `node cards/build.mjs my-thing` to render just that one).

## fields

- `card`: set to `false` to list the project as a plain text bullet instead of a card (only `id`, `name`, `line`, `href` are used).
- `size`: `full` (880×240), `half` (430×240), or `row` (880×56, a slim name + one-liner strip for projects with no image yet). Two halves in a row share a line.
- `status`: `live` or `dev`. Bookkeeping only; nothing is drawn on the card.
- `href`: optional. Without it the card isn't a link (fine for unreleased things).
- `site`: optional. Shown on full cards in place of the repo URL.
- `shot`: optional. Use `size: "row"` when there's no image yet. `term: "…"` shows terminal output instead (for CLI tools), and `shelf: ["a", "b"]` shows a row of pills.
- `focus`: CSS `object-position` for the crop. `100% 80%` = show the bottom-right of the screenshot.
- `theme`: card background, text, and accent colors. Pick them from the screenshot.

## tips

- `node cards/build.mjs --preview` writes `.render.html`. Open it to see every card at once while tuning `focus` and colors.
- `node cards/build.mjs --og` also renders `og/<id>.png` for every non-row card. If the project's website has its own og:image, prefer that.
- Needs Google Chrome. Set `CHROME=/path/to/chrome` if it isn't in `/Applications`.
- The README block between the `cards:start` / `cards:end` markers is overwritten on every build. Edit headings and notes in `projects.json`.
