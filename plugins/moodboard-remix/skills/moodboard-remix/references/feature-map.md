# Feature → where to look

Use this to break a functionality into features and find candidates on each source. "21st" = `21st.dev/community/components/s/{slug}`; "RB" = `reactbits.dev/{path}`; "UV" = `uiverse.io/{category}`.

| Feature | 21st.dev | React Bits | Uiverse | Notes |
|---|---|---|---|---|
| Hero / above the fold | `hero` | text-animations/* + backgrounds/* | — | Combine a calm 21st hero with one RB text effect or background, not both loud. |
| Navigation bar | `navbar`, `header` | components/pill-nav, card-nav, gooey-nav, staggered-menu, bubble-menu | — | Mobile menu behaviour matters more than desktop flair. |
| Dock / app launcher | `dock` | components/dock | — | |
| Sidebar (app) | `sidebar` | micro/line-sidebar | — | Prefer shadcn sidebar for dashboards. |
| Feature grid / bento | `features`, `bento-grid` | components/magic-bento, spotlight-card | cards | |
| Pricing | `pricing-section` | animations/star-border (highlight plan) | cards, toggle-switches (monthly/yearly) | |
| Testimonials / social proof | `testimonials` | animations/logo-loop, components/card-swap | cards | |
| Logo cloud | `clients`, `logos` | animations/logo-loop | — | |
| Call to action | `call-to-action` | animations/magnet, click-spark | buttons | |
| Buttons | `button` | animations/star-border, micro/hold-button, sling-button, fuse-button | buttons | Uiverse has the widest choice. |
| Forms / sign-in / sign-up | `sign-in`, `sign-up`, `form`, `input` | micro/curved-input, scrub-field | forms, inputs, checkboxes | Check labels and error states. |
| Toggles, checkboxes, radios | `toggle`, `checkbox`, `radio-group` | micro/squish-switch, spring-check, jelly-radio | toggle-switches, checkboxes, radio-buttons | |
| Select / dropdown | `select`, `dropdown-menu` | micro/glide-select | — | Accessibility: prefer Radix-based. |
| Modal / dialog | `modal` | — | — | |
| Toast / notification | `toast` | micro/swipe-toast | — | |
| Tooltip | `tooltip` | micro/warm-tooltip | tooltips | |
| Loading states | `loader`, `skeleton` | micro/lattice-loader | loaders | |
| Stepper / onboarding | `stepper`, `onboarding` | components/stepper | — | |
| Tabs / segmented | `tabs`, `segmented-control` | micro/rubber-segment | radio-buttons | |
| Tables / data | `table`, `data-table` | — | — | shadcn data-table for real data. |
| Charts / KPIs | `chart`, `stats` | text-animations/count-up | — | |
| AI chat / prompt input | `ai-chat`, `prompt-input` | micro/prompt-bar, voice-pill | inputs | |
| Gallery / portfolio | `gallery`, `carousel` | components/masonry, circular-gallery, dome-gallery, carousel, tilted-card | cards | |
| Profile / team | `team`, `profile` | components/profile-card, lanyard | cards | |
| FAQ | `faq`, `accordion` | components/accordion-gallery | — | |
| Footer | `footer` | — | — | |
| Backgrounds / texture | `background`, `/community/shaders`, `/community/gradients` | backgrounds/* | patterns | WebGL is costly on mobile. |
| Cursor / delight effects | — | animations/*-cursor, click-spark, splash-cursor | — | Only with "Showpiece" motion level. |
| Rating / feedback | `rating` | micro/peek-rating, pulse-heart | — | |
| Empty / 404 states | `empty-state`, `404` | text-animations/fuzzy-text, glitch-text | — | |

If a slug doesn't exist, search the source for the feature name and closest synonyms.

## Motion level → which sources to lean on

- **Subtle**: 21st.dev shadcn blocks + Uiverse minimal elements; React Bits limited to fade-content, animated-content, count-up.
- **Noticeable**: add React Bits text animations, scroll reveals, spotlight/tilted cards.
- **Showpiece**: React Bits backgrounds, cursors, 3D galleries; 21st.dev shaders. Always add `prefers-reduced-motion` fallbacks.
