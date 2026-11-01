# Sources

Catalogs change constantly — always browse them live; use the examples below only to orient yourself.

## 21st.dev — components (`https://21st.dev/community/components`)

shadcn/ui-compatible React + Tailwind components and full sections.

- Listing sections: `/community/components/featured`, `/community/components/newest`
- Category pages: `/community/components/s/{slug}` — e.g. `hero`, `button`, `ai-chat`, `pricing-section`, `modal`, `navbar`, `footer`, `features`, `testimonials`, `call-to-action`, `sign-in`, `card`, `table`, `tabs`, `input`, `sidebar`, `chart`, `background`, `text`. Guess the slug, and if it 404s go back to the components page and read the category chips.
- Extra galleries: `/community/gradients`, `/community/shaders`, `/community/ascii`, `/community/libraries`
- Component detail: `/@{author}/components/{slug}` — e.g. `/@jahed/components/spotlight-card`. Its "About" text describes the look and motion precisely (e.g. "frosted translucent track, gradient rim glow, spring-animated sliding thumb") — use it, plus a screenshot, as the spec when replicating.
- WebFetch on a category page returns the full list of names and URLs (≈60 per page) — fast way to gather candidates.
- Install:
  ```bash
  npx shadcn@latest add "https://21st.dev/r/{author}/{slug}?api_key=$API_KEY_21ST"
  ```
  Requires a 21st.dev API key (free tier has a daily install limit). If the user has no key or hits the limit: copy the code if the detail page shows it publicly; otherwise replicate the component from its public preview.
- Preview images come from `cdn.21st.dev` — you can embed them in comparison pages.

## 21st.dev — templates (`https://21st.dev/community/templates`)

Full React / Next.js websites.

- Filters: `/community/templates/free`, `/paid`, `/included` (in 21st plan), `/verified`
- Detail: `/@{creator}/templates/{slug}` — e.g. `/@larsen66/templates/glass-portfolio`, `/@coreui/templates/coreui-free-react-admin-template`
- Access varies: open source, "with plan", or paid ($39–$119+). Open source → clone it. Anything else → replicate it from the public detail page, screenshots and live demo (see "Replicating a style" in SKILL.md). Never buy one, and never fetch code from behind the paywall.
- **Gathering candidates (tested)**: in the built-in browser on `/community/templates`, scroll to the bottom a few times (it lazy-loads), then collect `a[href*="/templates/"]` hrefs + text (~50 templates). Then `fetch()` each shortlisted detail page and parse it with `DOMParser`: `meta[property="og:image"]` = official hero preview (on `cdn.21st.dev`), `meta[name="description"]` = full feature list and stack, and the anchor whose text is "Preview"/"Open preview" = the live demo URL. Don't regex the raw HTML for demo URLs — it contains other templates' links.
- **Preview images**: artifact CSP blocks external images, so download the og:image through `https://cdn.21st.dev/cdn-cgi/image/width=1200,format=jpeg,quality=80/{path}` with curl into the scratchpad and publish them as artifact `files`. Prefer these official previews over screenshots of live demos: demos often have loading screens, WebGL heroes that don't render in the pane, and reveal animations, so screenshots come out blank or partial.
- The listing has no topic categories — infer type (SaaS, portfolio, agency, dashboard, restaurant, store, health/clinic…) from names and detail pages. Open detail pages in the browser to see screenshots, page list and live demo link.

## 21st.dev — themes (`https://21st.dev/community/themes`)

shadcn/ui themes (CSS variable sets). Also: `/community/themes` sections "Websites" and "Presets".

- Detail: `/@{author}/themes/{slug}` — e.g. `/@serafimcloud/themes/vercel`, `modern-minimal`, `zen-linen`, `claude`, `sage-garden`, `elegant-luxury`, `supabase`, `vintage-paper`, `graphite-mono`, `catppuccin`, `amber-slate`, `solar-dusk`, `lime-frost`
- **Getting the tokens (tested, fastest)**: open any 21st.dev page in the built-in browser, then with `javascript_tool` `fetch('/@{author}/themes/{slug}')` for each candidate, unescape the text (`.replace(/\\"/g,'"')`) and slice from `':root {'` to `'@theme inline'` — that is the theme's full CSS (`:root` + `.dark`, colors, `--radius`, `--font-sans/serif/mono`, shadows). One script can pull 10–15 themes at once. The "Copy CSS" button only writes to the clipboard, so don't rely on it.
- Fallback: the detail page renders client-side, so WebFetch returns almost nothing. Open it in the built-in browser and read the code/CSS tab (`get_page_text`, or `javascript_tool` to read `getComputedStyle(document.documentElement)` for `--background`, `--foreground`, `--primary`, `--primary-foreground`, `--secondary`, `--muted`, `--accent`, `--destructive`, `--border`, `--input`, `--ring`, `--card`, `--popover`, `--chart-1..5`, `--sidebar-*`, `--radius`, `--font-sans`, `--font-serif`, `--font-mono`, shadows). Capture both light and dark values.
- If the detail page offers a shadcn install command or registry URL, prefer it for applying the theme.

## React Bits (`https://reactbits.dev`)

Animated, expressive React components. Best for: hero text effects, animated backgrounds, cursor effects, galleries, playful micro-interactions.

- Categories and URL pattern `/{category}/{kebab-name}`:
  - `/text-animations/` — Split Text, Blur Text, Shiny Text, Gradient Text, Decrypted Text, Rotating Text, Scroll Reveal, Text Type, Count Up, Glitch Text, Scroll Velocity…
  - `/animations/` — Animated Content, Fade Content, Magnet, Click Spark, Glare Hover, Logo Loop, Star Border, Electric Border, Target Cursor, Splash Cursor, Pixel Transition, Gradual Blur…
  - `/components/` — Magic Bento, Spotlight Card, Tilted Card, Card Swap, Dock, Pill Nav, Card Nav, Staggered Menu, Gooey Nav, Bubble Menu, Masonry, Circular Gallery, Dome Gallery, Carousel, Stepper, Animated List, Scroll Stack, Profile Card, Glass Surface, Counter, Elastic Slider, Folder…
  - `/micro/` — Hold Button, Squish Switch, Spring Check, Jelly Radio, Swipe Toast, Peek Rating, Prompt Bar, Glide Select, Slide Commit, Lattice Loader, Pulse Heart, Warm Tooltip…
  - `/backgrounds/` — Aurora, Silk, Particles, Beams, Waves, Dot Grid, Galaxy, Orb, Iridescence, Light Rays, Grainient, Ripple Grid, Hyperspeed, Threads, Dark Veil, Liquid Ether…
- Install (variant suffix = language `JS|TS` + styling `CSS|TW`):
  ```bash
  npx shadcn@latest add @react-bits/SplitText-TS-TW
  ```
  Component name is PascalCase (`BlurText`, `MagicBento`, `Aurora`). Or copy manually from the Code tab and install the listed dependencies (often `motion`, `gsap`, `ogl`, `three`).
- Many backgrounds are WebGL — heavy on mobile; mention it.

## Uiverse (`https://uiverse.io/elements`)

Community HTML/CSS (and Tailwind) UI elements. Best for: small polished pieces — buttons, toggles, checkboxes, loaders, inputs, cards, tooltips, radio buttons, forms, patterns. Works in any stack.

- **WebFetch gets 403 here — use the built-in browser.**
- Search (works in the browser): `https://uiverse.io/elements?search={term}`. List result links with `javascript_tool` (hrefs matching `/{user}/{slug}`), and read an element's code from its detail page via `document.querySelectorAll('.cm-content')`. Many results are off-brief (glitch, neon, 3D); filter hard.
- Category pages: `https://uiverse.io/{category}` — `buttons`, `checkboxes`, `toggle-switches`, `cards`, `loaders`, `inputs`, `radio-buttons`, `forms`, `patterns`, `tooltips`. Tag search: `https://uiverse.io/elements?search={term}` or the tags on each page (e.g. `neumorphism`, `glassmorphism`, `3d`, `minimalist`, `gradient`, `animated`).
- Element detail: `https://uiverse.io/{username}/{element-slug}` — the code panel offers HTML + CSS or Tailwind, and an export to React/JSX.
- Licence: MIT. Keep attribution.
- When adapting, replace hardcoded colors with the project's CSS variables.
