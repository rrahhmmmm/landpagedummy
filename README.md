# Rawa Sentosa Group — Landing Page

Single-page landing site for **Rawa Sentosa Group**, a vertically-integrated hospitality, wellness, and property operator. Everything (HTML, CSS, JS) lives in one file: `index.html`.

> _Building Spaces. Creating Experiences._

---

## Tech Stack

All third-party libraries are vendored locally under `assets/libs/` — no CDN, no build step.

| Library | Purpose |
| --- | --- |
| Tailwind (JIT runtime) | Utility-class styling |
| GSAP + ScrollTrigger + ScrollToPlugin | Scroll-driven animations, intro timeline, magnetic buttons |
| Three.js | 3D timeline on the Track Record section (desktop only) |
| Lucide | Inline SVG icons |
| Custom fonts (Fraunces, Cormorant Garamond, MuseoModerno) | Self-hosted `woff2` via `assets/fonts/fonts.css` |

---

## Project Structure

```
.
├── index.html              # entire site — markup, inline <style>, inline <script>
├── bgrawa_fix.mp4          # hero video background
├── assets/
│   ├── libs/               # vendored JS libraries
│   ├── fonts/              # self-hosted woff2 + fonts.css
│   └── img/                # founders, hero poster, generic photos
│       └── trackrecord/    # per-project image sets for the timeline
│           ├── urban/
│           ├── jemari/
│           ├── pola/
│           └── amarta/
├── .gitattributes          # disables LFS for *.mp4 (GitHub Pages compat)
└── .gitignore
```

---

## Running Locally

The hero video and Three.js texture loading require an HTTP origin (they will not work from `file://`). Serve the folder with any static server:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Any of these also work: `npx serve`, `php -S localhost:8000`, the VS Code "Live Server" extension.

---

## Page Sections

| # | Section | What it does |
| --- | --- | --- |
| Intro | Overlay animation | "RAWA" + sub-text reveal, scales into the hero ghost wordmark |
| 1 | Hero | Looping video background, headline, sub-copy, CTA |
| 2 | Practice | Six service pillars as click-to-expand accordions |
| 2b | Foundation | Four founders on a scroll-driven 3D carousel |
| 3 | Track Record | Three.js 3D timeline (desktop) / 2D fallback timeline (mobile, `≤ 767px`) + featured case |
| 4 | Contact | Email CTA, presence list, animated sparkles, footer |

Side-dot navigation and a top nav both update active state via `ScrollTrigger`.

---

## Customizing Content

Common edits, all inside `index.html`:

- **Hero headline / sub-copy** — search for `id="heroText"`.
- **Service pillars (6 items)** — search for `class="pillar"`; each block has a number, title, summary, and expand panel.
- **Founders** — search for `class="founder-card"`; swap the `<img src>` (files in `assets/img/`), name, role, and quote.
- **Track Record entries** — both the Three.js (`timelineData` array in the script) and the 2D fallback (`class="tl2d-node"` blocks in the markup) need to be updated together so desktop and mobile match. Each entry references a slideshow folder under `assets/img/trackrecord/<slug>/`.
- **Featured case (Wellness Cinere)** — search for `<!-- Featured Case -->` region around the bottom of the Track Record section.
- **Presence list / contact email** — search for `id="contact"`.
- **Colors** — CSS custom properties at the top of the inline `<style>` block (`--navy`, `--gold`, `--cream`, etc.).

---

## Deployment — GitHub Pages

This site is built to deploy as-is on GitHub Pages. Notes:

- `*.mp4` is explicitly excluded from Git LFS (see `.gitattributes`) because GitHub Pages does not serve LFS-backed files. The hero video must be a regular Git-tracked blob.
- No build step. Pushing to the configured Pages branch is enough.
- All asset paths are relative, so the site works at both a user-site root (`username.github.io/`) and a project subpath (`username.github.io/repo/`).

---

## Browser Support

- **Desktop**: Chromium, Firefox, Safari (latest two majors). Three.js timeline + custom cursor are desktop-only.
- **Mobile (`≤ 767px`)**: 3D timeline is replaced by a 2D fallback, custom cursor disabled, magnetic buttons disabled.

---

## License

Proprietary — © Rawa Sentosa Group. All rights reserved.
