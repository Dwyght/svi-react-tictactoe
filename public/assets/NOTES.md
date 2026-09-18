# Asset migration notes

All images/video below were copied as-is (no transformation) from
`svi-js-tic-tac-toe/src/assets/images/` into `public/assets/`, organized by
the domain that actually uses them (checked against real usage in the old
`.js`/`.css` files, not guessed):

- `app/` — `background.mp4`, `splash_art.png`, `splash_text.png` (used by
  `SplashScreen.js`), `loading-sushis/*` (used by `ConveyorBelt.js`)
- `home/` — `banner.png` (used by `pages/Home.js`)
- `game/` — `victory.png`, `defeat.png`, `draw.png`, `spectator.png` (used by
  `ResultModal.js`), `plate.png` (used by `css/components/board.css`),
  `emote/*.png` (used via `config/constants.js`), `x-sushis/*.png`,
  `o-sushis/*.png` (used via `config/constants.js`)
- `favicon.png` — moved to `public/favicon.png` (project root), per Vite
  convention for the site favicon

## Not migrated: `coin.png`, `mushroom.png`

These two files exist in the old app's `src/assets/images/` folder but are
**not referenced anywhere** in its `.js` or `.css` files — they're dead
assets. They were intentionally left out of this structure rather than
copied over uninspected. If they're actually used somewhere (e.g. a page not
covered here, or referenced dynamically), pull them back in under whichever
domain folder uses them.
