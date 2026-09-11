# hannah — personal site

Single static page. No build step, no dependencies.

## Files

    index.html                  the whole site (markup + styles + projects)
    ink-signature-slate.png     signature, bottom right
    ink-living-slate.png        "living in -1", surfaces behind the name
    ink-technology.png          flip side of "inventing"
    ink-blind-spots.png         flip side of "surfacing"
    ink-culture.png             flip side of "steering"

## Adding projects

Open `index.html` and edit the `PROJECTS` object near the bottom — it's the only
thing you need to touch. Three keys: `inventing`, `surfacing`, `steering`.

```js
const PROJECTS = {
  inventing: [
    { title: 'evaluation infrastructure',
      date:  '2026 —',
      tag:   'software',                     // software | writing | leadership | research
      desc:  'One sentence on what it is.',
      href:  'https://github.com/you/repo' }
  ],
  ...
};
```

Add, remove, or reorder entries freely — the list renders from the array.

## Other things to change

- **Bio** — the `<p class="bio">` in the markup.
- **Social links** — the `<footer>`; replace `YOUR-HANDLE` and `you@example.com`.
- **Colors** — the `:root` block: `--ink`, `--paper`, `--accent`.

## Deploy (GitHub Pages)

```bash
git init
git add .
git commit -m "site"
git branch -M main
git remote add origin git@github.com:YOU/YOU.github.io.git
git push -u origin main
```

Then Settings → Pages → deploy from `main` / root.
