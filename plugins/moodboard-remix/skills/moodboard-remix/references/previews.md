# Building previews

Every round ends with a visual comparison page. Publish it as an Artifact (load `artifact-design` first) unless the user wants to stay local, in which case write an HTML file in the project and open it in the built-in browser.

General rules for the comparison page:
- Same viewport, same content, same order for every option so differences are about style, not content.
- Every option shows exactly the same set of screens, no more and no fewer. Never add an extra shot to one option (e.g. a dark-mode capture only on the recommended one): it breaks the side-by-side comparison. If a variant matters (dark mode, mobile), capture it for every option and expose it as another value of the global view switcher.
- Each option card: preview (screenshot or live render), name, source + link, author, key dependencies, size of the change in the user's project, one line on fit with the brief. No price, free/paid badge, or "install/copy/replicate" label — how a piece is obtained is never shown.
- The recommended option gets a clear "Recommended" badge and a short why.
- Number options (T1–T4, C1–C5, S1–S5) so the user can answer "C3 for pricing, S2".

## Getting preview images

- **Screenshots**: open the item in the built-in browser (`navigate`), wait for animations, `computer` → `screenshot` (or `zoom` on the demo region). To embed them in an artifact, save the page's own preview image instead: 21st.dev previews are on `cdn.21st.dev` and can be referenced directly by URL; for others, describe the look and link out if you can't get an image.
- **Live renders**: for Uiverse elements (plain HTML/CSS) you can paste the code straight into the comparison page — that's the most faithful preview. Scope each element's CSS under a wrapper class to avoid clashes.

## Templates mode

Open with a "Today" strip: a screenshot of the user's current site plus its list of sections. Then 4 cards in a 2×2 grid (1 column on mobile), each with: the template's official hero preview (same kind of image for all four), the route it represents (safe / bold / wildcard / editorial…), a **section map** — each of the user's real sections → the template section it would become — what you'd change (accent, font, heavy parts to drop), pros/cons against the brief, and links to the template and its live demo. Close with one paragraph on why the recommended one wins.

If the user's stack differs from the templates' (e.g. static HTML vs Next.js), ask in Step 3 whether to keep the stack; if they keep it, every template is applied by rebuilding its style in their stack — don't call that out on the cards.

## Components mode

**Prefer live, interactive rebuilds over screenshots.** Components are about interaction (sliding thumbs, hovers, springs), which a still image can't show. For each candidate, rebuild it in the comparison page in plain HTML/CSS (small JS only if needed) using:
- the project's real tokens (copy its CSS variables, fonts, radius, field height), with a light/dark switcher if the project has both;
- the project's **real markup** for that control, so the rebuild doubles as the implementation and applying it is a CSS swap (e.g. a thumb drawn with `::before` and moved with `:has(input:checked)` needs no HTML change);
- the surrounding context (e.g. the neighbouring form fields), so the user judges fit, not the component in isolation;
- a first "Today" row with the current control, and `prefers-reduced-motion` fallbacks.
This matters most when the project isn't React: React Bits and 21st.dev pieces are React, so they get rebuilt from their public demo anyway (don't mention that on the card). Per card, say how big the change is ("≈12 lines of CSS, no JS, no HTML changes").
CSS gotcha: `!important` inside `@keyframes` invalidates the declaration — animate independent `scale`/`translate` properties instead of fighting `transform`.

One section per feature. Each section: a row of 5 cards (horizontally scrollable on mobile), recommended one first and highlighted. Below the row, one line on how the recommended pick fits with the picks for the other features.

## Themes mode — preview on the user's own UI

Pick the most faithful method available:

### A. Live app (best)

1. Start the app (`preview_start` with the project's launch config) and open the 2–3 most representative screens.
2. For each theme, inject its tokens with `javascript_tool`:
   ```js
   (() => {
     const id = 'theme-preview';
     document.getElementById(id)?.remove();
     const s = document.createElement('style');
     s.id = id;
     s.textContent = `:root{ /* light tokens */ } .dark{ /* dark tokens */ }`;
     document.head.appendChild(s);
   })()
   ```
   If the theme changes fonts, also inject the Google Fonts `<link>`. For Tailwind v4 projects that map tokens via `@theme inline`, overriding the `--background`/`--primary`… variables is enough; for projects with hardcoded colors, note in the results which parts didn't change — that's useful feedback too.
   The project's tokens rarely share shadcn names: map them by role (background, surface, border, text, muted text, accent, accent text, error/success, data-viz colors → chart-1..5). Put the mapping in a reusable `applyTheme(slug, mode)` function on `window`, and fill the app with realistic sample data first so result screens are populated. If the page has `scroll-behavior: smooth`, scroll with `scrollTo({top, behavior: 'instant'})`, wait for `document.fonts.ready` plus ~500 ms, then screenshot. Set a fixed viewport (e.g. 1100×820) so all shots match.
3. Screenshot each screen per theme. Screenshots are saved under the session's `tool-results` folder (the path is in the tool output); copy them into the scratchpad and publish them as artifact `files`. (and dark mode if the product uses it). Remove the injected style at the end. Nothing is written to the project in this step.
4. Comparison page: 5 columns (or a tab switcher) with the same screens, plus a token table (primary, background, accent, radius, fonts) per theme.

### B. App exists but can't run

Recreate the key screen in a single static HTML page using the project's real structure and copy (read the components to get layout, labels and data). Define every color as a CSS variable, then add a switcher that swaps the 5 themes' token sets on `:root`. Show all 5 side by side in iframes or scaled-down containers, plus the switcher for a full-size look.

### C. Nothing built yet

Build a representative mock screen for the product type from the brief (e.g. landing hero + feature cards + pricing for SaaS; dashboard with sidebar, KPI cards and a table for internal tools) and apply method B.

Always include both light and dark variants when the theme defines them, and check text contrast (WCAG AA) on each — flag any theme that fails.
