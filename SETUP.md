# SETUP — Atharva Hegdekar · GitHub profile README

The README and its three SVG assets are ready to publish. You need to create the repository, upload the files, and replace four placeholders.

---

## 1. Files

```
README.md            the profile README (text unchanged in this revision)
assets/header.svg    cosmic header banner — 1600 × 500, ~112 KB
assets/typing.svg    one-line typewriter that cycles three sentences — 900 × 46
assets/divider.svg   gradient divider with drifting particles — 1600 × 72
SETUP.md             this file
```

All three SVGs are hand-written and self-contained: no JavaScript, no external fonts, no linked stylesheets. The header is a layered scene — nebula fields, three depths of starfield, a spiral galaxy, a ringed planet, a textured asteroid with craters, an orbit with a travelling moon, drifting rocks, and occasional shooting stars. Every element animates with SMIL, which runs inside an `<img>` tag.

---

## 2. Publish it

**1. Create the repository**

1. Go to `https://github.com/new`
2. Repository name: **exactly your GitHub username**. This is the only way GitHub treats a repo as your profile README.
3. Visibility: **Public** — a private repo will not appear on your profile.
4. Tick **Add a README file**, then create the repository.

**2. Upload the files**

In the repo: **Add file → Upload files**, then drag in `README.md` and the whole `assets` folder. Commit message: `Update profile README`.

Keep the folder named `assets` and the files named `header.svg`, `typing.svg`, `divider.svg`, all lowercase. The README references them by relative path, so any rename breaks the images.

If the assets are already in the repo from an earlier version, open each file, click the pencil icon, and paste the new contents — or upload over them, which creates a new commit.

With the Git CLI:

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME.git
cd YOUR_GITHUB_USERNAME
cp -r /path/to/kit/README.md /path/to/kit/assets .
git add README.md assets
git commit -m "Update profile README and cosmic assets"
git push
```

**3. Check it**

Open `https://github.com/YOUR_GITHUB_USERNAME`. The banner appears above your pinned repositories. Give it a few seconds on first load — GitHub's image proxy caches assets the first time it sees them.

---

## 3. Placeholders

| Placeholder | Where | Replace with |
| :-- | :-- | :-- |
| `YOUR_GITHUB_USERNAME` | 4 — stats card and the comment block | Your username, no `@` |
| `YOUR_LINKEDIN` | 3 — contact row and comment | Your LinkedIn handle, e.g. `atharva-hegdekar` |
| `YOUR_X` | 3 — contact row and comment | Your X handle, no `@` |
| `YOUR_ZOONIVERSE` | 3 — contact row and comment | Your Zooniverse username |
| `hegdekaratharva049@gmail.com` | 2 — About and contact | Already your address; change only if you want another one |

Find-and-replace all four at once; the counts include the comment block at the top of the file, so replacing every occurrence is safe.

If a link is not ready yet, delete its whole row from the contact table rather than leaving a dead `YOUR_` link in place.

---

## 4. Editing the visuals

**Header text** — four lines near the bottom of `assets/header.svg`. They sit at these coordinates inside a 1600 × 500 canvas:

| Line | Current text | `y` position |
| :-- | :-- | :-- |
| Location label | `INDIA · UTC+5:30` | 186 |
| Name | `ATHARVA HEGDEKAR` | 256 |
| Tagline | `PHYSICS · COMPUTING · AEROSPACE · AI` | 300 |
| Small line | `projects · notes · experiments` | 332 |

Edit the text between `<text ...>` and `</text>`. If a replacement is much longer, reduce `letter-spacing` on that line (`9` for the name, `3.8` for the tagline) so it doesn't reach the asteroid at x ≈ 1110.

**The asteroid** is drawn by a generated outline path with craters and surface speckle, centred at `cx=1214, cy=292`. To move or resize it, change `ax`, `ay` and `AR` in the generator (`gen_visuals.py`, function `header`); editing the SVG by hand means recalculating the crater positions too.

**Colour balance** — the five nebula patches are `<ellipse>` elements filled with the `violet`, `magenta`, `cyan`, `indigo` and `gold` gradients, each with an opacity animation. Raising or lowering that opacity is the fastest way to make the banner warmer, cooler or calmer.

**Typewriter lines** — the three sentences live in `assets/typing.svg`, one per `<text>` element. Keep them under about 66 characters; anything longer runs to the edge of the banner.

**Divider** — one `<line>` with the `dl` gradient, plus 40 drifting particles. If you want it quieter, lower the particle count in the generator (`range(40)`).

**Stats card** — a single image URL in the GitHub section. Delete that section if you would rather not show it while the account is new; nothing else depends on it.

---

## 5. What animates, and what depends on outside services

| Element | Animation | Renders on GitHub? | Depends on |
| :-- | :-- | :-- | :-- |
| Nebula fields | Opacity drift, 26–46 s cycles | Yes | Nothing |
| Starfield, 3 depths | Twinkle at staggered speeds; diffraction spikes on bright stars | Yes | Nothing |
| Spiral galaxy | Slow rotation, 150 s per turn | Yes | Nothing |
| Ringed planet | Vertical float, 19 s | Yes | Nothing |
| Asteroid | Tumble ±2.4°, 48 s | Yes | Nothing |
| Orbit moon | Path travel, 26 s | Yes | Nothing |
| Small rocks | Parallax drift, 38–54 s | Yes | Nothing |
| Shooting stars | Path travel with a short opacity flash, every 9–14 s | Yes | Nothing |
| Typewriter | Clip reveal plus blinking cursor | Yes | Nothing |
| Divider | Particle twinkle, drifting comet | Yes | Nothing |
| Tools icon strip | Static image | Yes | skillicons.dev |
| Stats card | Static image, live data | Yes | github-readme-stats |

GitHub strips `<script>`, blocks external stylesheets, and does not run JavaScript in Markdown. An SVG referenced with `<img src="...">` is rendered by the browser's SVG engine instead, which does support SMIL. That is why every animated element is a file in `assets/` rather than inline Markdown.

The motion is deliberately slow — nothing in the banner loops faster than a few seconds, so it reads as atmosphere rather than distraction. If you ever want a fully static page, delete the `typing.svg` line; the header and divider stay legible as stills.

---

## 6. Troubleshooting

| Symptom | Cause | Fix |
| :-- | :-- | :-- |
| Banner shows but nothing moves | Repo is private, or the image was cached as a still | Make the repo public; hard-refresh with Ctrl/Cmd+Shift+R |
| Broken image icon | Folder or file name mismatch | Paths are case-sensitive: `assets/header.svg` |
| Banner looks flat or washed out | The viewer's browser is rendering an older cached copy | Add `?v=2` to the image path in the README to bust the cache |
| Divider invisible | The gradient failed to load | Confirm the file uploaded intact; the gradient is defined inside the same SVG |
| Stats card says "Something went wrong" | The public stats server is rate-limited | Reload in a minute, or deploy your own copy of github-readme-stats on Vercel |
| Stats card shows zeros | New account with few public commits | Expected; it fills in as you push |
| Header text overlaps the asteroid | Replacement text is longer than the original | Lower the `letter-spacing` on that line |
| Animation stutters on an old laptop | 263 SMIL animations on one canvas | Reduce the star count in `starfield(...)` calls in the generator |

---

## 7. Before you publish

- Every project row states its real status — complete, ongoing, in progress, or still reading. Update a row when the status changes rather than when you want it to have changed.
- No publications, certifications, internships or affiliations are claimed anywhere on the page.
- The Zooniverse section describes participation in a NASA Partner citizen-science project, which is accurate; it does not imply any affiliation with NASA.
- The only numbers on the page come from the GitHub API.
- Replace all four placeholders, then open the profile in a private browser window to check it as a visitor would see it.
