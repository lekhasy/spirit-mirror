# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Build to ./dist/ for production
npm run preview   # Preview production build locally
```

## Architecture

### Layout Pattern
- **Layout.astro**: Base HTML shell with fixed header (72px height), CSS custom properties for theming, and global CSS imports
- **PaddingLayout.astro**: Wrapper that applies 72px top padding to account for fixed header
- Country pages use Layout directly (not PaddingLayout) with their own padding

### Homepage (index.astro)
- Contains server-side `countries` array embedded in DOM via `data-countries` attribute for client-side JavaScript access
- Client-side script in `<script type="module">` handles carousel rotation (5s intervals), search functionality, and dynamic button styling
- Carousel randomizes country order on load, cycles through slides with crossfade transition
- Search panel shows 3 random suggestions on focus when empty, filters by name on input

### Styling System
- Global CSS in `src/styles/global.css` handles all shared styles including responsive breakpoint at 720px
- CSS variables defined in Layout.astro: `--accent-1`, `--accent-2`, `--accent-3`, `--bg` (gradient), `--glass`
- Country pages use inline gradient backgrounds (typically 2-color) matching cultural aesthetics
- Glassmorphism effects with backdrop filters and semi-transparent backgrounds throughout

### Country Data Structure
Each country entry requires:
```javascript
{
  name: string,
  path: string,
  image: string (URL),
  description: string,
  flagColors: string[] (hex colors for button theming)
}
```

The homepage client script uses `flagColors[0]` to determine button text contrast (light/dark) via brightness calculation.

### Key Implementation Details
- No bundling for client JS—scripts run directly in browser
- Mix of external image URLs (Unsplash) and local files in `/public/`
- TypeScript strict mode enabled
- No testing framework configured
