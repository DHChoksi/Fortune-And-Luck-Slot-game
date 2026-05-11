# Imperial Fortune - Slot Game Prototype

A playable HTML5 prototype of the Imperial Fortune slot game built for the AGS Game Innovation Fellowship candidate exercise.

## How to Play

1. Open `index.html` in any modern browser (Chrome, Firefox, Safari, Edge).
2. Press **SPIN** or hit **spacebar** to play one spin.
3. Press **AUTO 25** to play 25 spins automatically (hit AUTO again to cancel).
4. Press **PAYS** to view the paytable.
5. Adjust the **bet size** ($1, $3, $5) from the dropdown.

## What You'll See

- **Slot reels (left)**: 3 reels, 22 stops each, displayed as a 3×3 grid with the middle row paying.
- **Fortune Wheel (right)**: Always-visible roulette-style wheel that spins in parallel with every slot spin.
- **Stats bar (bottom-right)**: Live tracking of spin count, total bet, total won, and realized RTP. After 100+ spins this should converge near the theoretical 90.24%.

## What to Watch For

- **Most spins (~99%)**: just normal slot rhythm — wheel lands on a number, no match
- **About 1 in 73 spins**: 1-match free spin (slot AND wheel re-spin for free)
- **About 1 in 1,520 spins**: 2-match cash bonus (popup celebration)
- **About 1 in 95,800 spins**: 3-match jackpot (full coin shower + jackpot popup)

The "near-miss" tension is built in: every spin where the wheel lands on a Dragon and there are zero Dragons on the payline (or vice versa), the player feels "so close."

## Files

```
ImperialFortune_HTML/
├── index.html    — the entire game (single file: HTML + CSS + JS)
├── README.md     — this file
└── assets/
    ├── Background.png       — starry purple game background
    ├── Lantern.png          — low-tier symbol
    ├── Gold_Coin.png        — mid-low-tier symbol
    ├── Jade.png             — mid-high-tier symbol
    ├── Dragon.png           — high-tier symbol (special, triggers wheel match)
    ├── Treasure_Chest.png   — top-tier symbol (special, triggers wheel match)
    └── Fortune_Wheel.png    — the parallel-spinning fortune wheel
```

## Math (validated)

- Reel composition: 8 Lantern, 8 Gold Coin, 4 Jade, 1 Dragon, 1 Treasure (per reel × 3 reels)
- Paytable: 8× / 8× / 12× / 100× / 350× of bet for 3-of-a-kind
- Wheel: 36 segments — 2 Dragons (opposite) + 2 Treasures (opposite) + 32 numbers
- Total RTP: **89.997%**

## Architecture Note

The code follows a **math-first, animation-second** pattern. When you press SPIN:

1. `runSpin()` returns the full result instantly (which 3 stops, what the wheel hit, what the player won)
2. Animations play to *reveal* a result that's already decided
3. The visible outcome matches the predetermined math exactly

This is how real slot machines work and means the same `runSpin()` function can drive a 100,000-spin headless simulation for the math-to-emotion visualization deliverable, without any rendering overhead.

## Browser Compatibility

Tested and works in Chrome 90+, Firefox 90+, Safari 14+, Edge 90+. Requires:
- ES6 (let, const, arrow functions, async/await, Promise)
- CSS3 (grid, custom properties, transforms, transitions)
- No external JS libraries used

## Known Limitations (intentional, per scope of brief)

- No sound effects (the brief explicitly says polish isn't required)
- No save/load (refresh the page = $100 fresh start, useful for testing)
- Single bet size lock recommended for math accuracy (other sizes use the same RTP, multiplied)

---

**Built by:** Dhruvi (Starlight) Choksi - May 2026
**For:** AGS Game Innovation Fellowship candidate exercise
