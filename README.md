# hannah — personal site

Single static page. No build step, no dependencies.

## Files

    index.html                  the whole site (markup + styles + projects)
    favicon.png / favicon-32.png / apple-touch-icon.png
    ink-signature-slate.png     signature, top left
    ink-living-slate.png        "living in -1" — retired, kept for reference
    ink-technology.png          flip side of "inventing"
    ink-blind-spots.png         flip side of "surfacing"
    ink-culture.png             flip side of "steering"

## Adding projects

Open `index.html` and edit the `PROJECTS` object near the bottom — it's the only
thing you need to touch. Three keys: `inventing`, `surfacing`, `steering`, each a
flat array.

```js
const PROJECTS = {
  inventing: [
    { title: 'Questable',
      date:  '2022',                       // "2025 —" marks something ongoing
      tag:   'software',                   // or an array: ['founding','0–1']
      role:  'Co-Founder & Advisor',       // optional, italic line under the title
      desc:  'One sentence on what it is.',// optional
      href:  'https://github.com/you/repo' }
  ],
  ...
};
```

Only `title` is required.

- **`href` is optional and the title *is* the link.** Leave the key out and the
  title renders as plain text with no dead link — add it later and the link
  appears. Five projects are intentionally unlinked this way.
- **Order doesn't matter.** Each tab is sorted newest → oldest at render time,
  with ongoing (`"2025 —"`) items first. Drop a new project anywhere in the array.
- **Dates live on the timeline rail**, not in the card. A repeated year is shown
  once and the following projects just get an unlabelled node.
- **Tags render in the casing you type** — no uppercase transform, so `HCI` and
  `neuroAI` survive intact.

## Colours

All in the `:root` block. One value per *role*, so hierarchy comes from colour
rather than from stacking transparency on one ink.

| property        | value     | role                                          |
|-----------------|-----------|-----------------------------------------------|
| `--paper`       | `#f5f8fa` | near-white background, faint cool cast         |
| `--ink`         | `#0d1b26` | primary text: name, bio, project titles        |
| `--ink-2`       | `#3f5462` | secondary: descriptions, footer links          |
| `--ink-3`       | `#5c6f7c` | tertiary: years, roles, separators             |
| `--rule`        | `#ccd9e1` | hairlines and the timeline rail                |
| `--accent`      | `#1453f0` | anything interactive: tabs, links, tags        |
| `--accent-deep` | `#0a2a7a` | reserved deeper blue                           |
| `--accent-line` | `#9db6f5` | tag pill outline                               |

Body text is 7.4:1 against the paper and the accent 5.6:1, so retuning these is
safe as long as you keep that kind of separation. `.grain` and `.wash` sit
behind the content at low opacity — raise them and the type starts to flatten.

## The project gallery

One horizontal row you scroll sideways; the mouse wheel is translated to
horizontal in JS. Cards dissolve into a `mask-image` fade at whichever edge
still has content, with a small chevron on that side.

Each tab deforms the *same* timeline rail rather than having its own motif, and
each has its own card entrance. Both are tuned deliberately quiet — search the
stylesheet for `one rail, three states` and `one grammar, three dialects`.

| tab       | rail                                   | entrance                          |
|-----------|----------------------------------------|-----------------------------------|
| inventing | ruler ticks, majors on the nodes       | `scale(.988)` settle              |
| surfacing | plain waterline                        | rises 8px, `blur(2px)` resolving  |
| steering  | plain; the row sits under perspective  | 9px lateral, `1.1deg` correction  |

Constant across all three: the easing, the ~.26s duration, the 22ms per-card
stagger, and the resting state. Only the vector of arrival changes. Steering
additionally turns each card through ±13° as it scrolls past, via a scroll-driven
CSS animation. All of it collapses under `prefers-reduced-motion: reduce`.

## Other things to change

- **Bio** — `<span class="lead">` in the markup; the three tab words continue it.
- **Social links** — the `<footer>`.
- **The name-reveal phrase** — currently live text set in Caveat as a stand-in.
  The stylesheet marks the spot to swap in real handwriting artwork.

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
