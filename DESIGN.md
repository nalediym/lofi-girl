# Design System — gifterm

## Product Context
- **What this is:** A Rust CLI tool that plays animated GIFs natively in kitty-protocol terminals
- **Who it's for:** Developers who live in the terminal and want it to feel alive — lofi vibes, pixel art, ambient animation
- **Space/industry:** Terminal tools, developer CLI utilities (peers: kitty, WezTerm, Ghostty, Charm, starship)
- **Project type:** CLI tool + landing page / docs site

## Aesthetic Direction
- **Direction:** Retro-Futuristic (lofi subset)
- **Decoration level:** Intentional — subtle grain texture, soft glow effects
- **Mood:** Warm, atmospheric, late-night-coding energy. Not harsh synthwave neon, more the soft amber glow of a terminal at 2am. The product plays GIFs; the brand should feel alive without being noisy.
- **Reference sites:** warp.dev (dark corporate polish), ghostty.org (brutally minimal ASCII), charm.sh (maximalist playful), starship.rs (clean docs). gifterm occupies a gap — warm/ambient/lofi — that none of these claim.

## Typography
- **Display/Hero:** Satoshi — geometric with just enough personality, modern without being generic. Loads from Fontshare.
- **Body:** DM Sans — clean, warm, excellent readability. Supports tabular-nums for data contexts.
- **UI/Labels:** DM Sans (same as body, medium weight)
- **Data/Tables:** DM Sans with `font-feature-settings: 'tnum'` — tabular figures for aligned numbers
- **Code:** JetBrains Mono — ligatures, excellent at small sizes, the developer standard
- **Loading:** Satoshi via `api.fontshare.com/v2/css`, DM Sans + JetBrains Mono via Google Fonts
- **Scale:**
  - `3xs`: 0.625rem (10px) — fine print, badges
  - `2xs`: 0.7rem (11.2px) — labels, metadata
  - `xs`: 0.8rem (12.8px) — captions, secondary UI
  - `sm`: 0.875rem (14px) — body small
  - `base`: 1rem (16px) — body
  - `md`: 1.125rem (18px) — body large
  - `lg`: 1.25rem (20px) — subheadings
  - `xl`: 1.75rem (28px) — section titles
  - `2xl`: 2.5rem (40px) — page titles
  - `3xl`: 3.5rem (56px) — hero display
  - `4xl`: clamp(3rem, 8vw, 5.5rem) — hero main

## Color
- **Approach:** Restrained — warm amber primary, teal secondary, used deliberately
- **Primary:** `#E8A849` — warm amber, the glow of a terminal cursor. For emphasis, CTAs, brand moments. Dark mode adjusted to `#C48A2A` in light mode for contrast.
- **Secondary:** `#5BB8B0` — soft teal, cool complement used sparingly. For info states, progress, secondary actions. Light mode: `#3D8A83`.
- **Neutrals:** Warm gray scale (not cool/blue grays):
  - 950: `#1A1816` (darkest background)
  - 900: `#211F1C` (raised surfaces, dark)
  - 850: `#2A2724` (overlay surfaces)
  - 800: `#343130` (subtle borders, dark)
  - 700: `#4A4643` (borders)
  - 600: `#6A6560` (disabled, tertiary text)
  - 500: `#8A8580` (placeholder, muted)
  - 400: `#A8A39C` (secondary text, dark mode)
  - 300: `#C4BFB8` (secondary text, light mode)
  - 200: `#DAD5CE` (borders, light mode)
  - 100: `#EDE8E1` (surfaces, light mode)
  - 50: `#F0EBE3` (background, light mode)
- **Semantic:** success `#7EC88B`, warning `#E8A849`, error `#D4574E`, info `#5BB8B0`
- **Dark mode:** Default. Dark mode uses neutral-950 as base bg, neutral-900 for raised surfaces. Light mode inverts to neutral-50 bg with white raised surfaces. Reduce primary/secondary saturation ~15% in light mode for comfortable contrast.

## CLI Output Styling
- **Prefix:** `gifterm` in dim/muted color — always present, quiet
- **Action verbs:** Colored by semantic meaning:
  - Teal (`info`): decoding, scaling, transmitting — active status
  - Green (`success`): cached, playing, done — completion
  - Yellow (`warning`): cache hit, narrow terminal — non-blocking issues
  - Red (`error`): not supported, file not found — failures
- **Details:** Default text color, no decoration
- **Hints:** Dimmed, appear under errors with additional context
- **Philosophy:** No emojis. No spinners. No progress bars. Quiet confidence. Each line is `prefix action detail`.
- **ANSI mapping:**
  - Primary (amber): `\x1b[38;2;232;168;73m` — prompts, emphasis
  - Secondary (teal): `\x1b[38;2;91;184;176m` — status, info
  - Success (green): `\x1b[38;2;126;200;139m` — completion
  - Warning (yellow): `\x1b[38;2;232;168;73m` — warnings (shares primary)
  - Error (red): `\x1b[38;2;212;87;78m` — errors
  - Dim: `\x1b[2m` — prefixes, hints

## Spacing
- **Base unit:** 8px
- **Density:** Comfortable — terminal tools shouldn't feel cramped
- **Scale:** 2xs(2px) xs(4px) sm(8px) md(16px) lg(24px) xl(32px) 2xl(48px) 3xl(64px)

## Layout
- **Approach:** Grid-disciplined — clean and readable. Let the aesthetic do the personality work, not layout chaos.
- **Grid:** Single column (CLI docs), 12-column grid for landing page. Breakpoints: sm(640px), md(768px), lg(1024px), xl(1280px)
- **Max content width:** 1120px
- **Border radius:** sm:4px, md:8px, lg:12px, full:9999px — use md as default, lg for cards/modals, full for pills/badges

## Motion
- **Approach:** Intentional — the product plays animations, so the brand should echo that. Subtle entrance fades, smooth state transitions. Nothing bouncy or playful.
- **Easing:** enter(cubic-bezier(0.16, 1, 0.3, 1)) exit(cubic-bezier(0.7, 0, 0.84, 0)) move(cubic-bezier(0.45, 0, 0.55, 1))
- **Duration:** micro(50-100ms) short(150-250ms) medium(250-400ms) long(400-700ms)

## Decoration
- **Film grain:** Subtle SVG noise overlay at 3% opacity, fixed position, pointer-events: none. Creates warmth without distraction.
- **Glow effects:** Radial gradient using primary-dim (`#E8A84933`) behind hero elements. Soft, atmospheric, not sharp.
- **No gradients on buttons.** No drop shadows. No blur effects. Decoration is environmental, not component-level.

## Decisions Log
| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-03-19 | Initial design system created | Created by /design-consultation based on competitive research of terminal tools space (warp, kitty, ghostty, charm, starship) |
| 2026-03-19 | Warm amber (#E8A849) as primary | Every terminal tool uses blue/purple. Amber claims the lofi/warm/alive identity gap. |
| 2026-03-19 | Satoshi for display typography | Geometric personality differentiates from monospace-everything terminal tools without being distracting |
| 2026-03-19 | Film grain + glow decoration | Matches the lofi/atmospheric brand promise. Most terminal sites are flat — this creates warmth. |
| 2026-03-19 | "Quiet confidence" CLI output philosophy | No emojis, no spinners, no progress bars. Clean structured output that respects terminal culture. |
