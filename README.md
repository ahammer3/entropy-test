# Just Make It Random

An interactive explainer on why *"just make it random"* is one of the hardest things a computer actually does — told through a single six-sided die.

> **Live demo:** https://&lt;you&gt;.github.io/&lt;repo&gt;/ &nbsp;·&nbsp; *(update after enabling GitHub Pages)*

Broken randomness doesn't announce itself: it passes the eye test, hides its structure, reuses a guessable seed, and leaks through a rounding error — all while looking perfectly fine. This page lets you *see* each of those failures happen, live, in your browser.

## The five experiments

1. **The eye test** — two live dice streams, one from the OS's cryptographic randomness, one from a throwaway generator. You can't tell them apart by watching.
2. **The hidden lattice** — plot each roll against the next and the "hasty" generator's numbers collapse onto a handful of invisible lines.
3. **The seed is the secret** — a device leaks a few rolls; watch an attacker brute-force its seed and then *predict rolls it hasn't made yet*.
4. **Modulo bias** — even perfect randomness gets skewed by the one-line shortcut `value % 6`.
5. **You try** — tap "randomly" and a dead-simple predictor beats the 1-in-6 baseline. Humans are the worst RNG of all.

## Running it

It's a single, fully self-contained HTML file — no build step, no dependencies, no external assets. Everything runs client-side.

- **Just open it:** double-click `index.html`, or
- **Serve it locally** (recommended, so `crypto.getRandomValues` has a secure context):

  ```bash
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```

## Deploying

Push to GitHub and enable **Settings → Pages → Deploy from a branch → `main` / root**. Since the file is named `index.html`, it loads at the site root automatically.

## How it works

- **True randomness** comes from [`crypto.getRandomValues`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/getRandomValues) (a CSPRNG), with a `Math.random` fallback for non-secure contexts.
- **The "hasty" generator** is a linear congruential generator, `x = (25·x + 13) mod 65536` — full-period, but every consecutive pair lands on one of 25 lines.
- **The brute-force demo** uses a small, seedable PRNG (mulberry32) so the whole seed space is searchable in the browser.
- No frameworks. Vanilla JS, canvas, and CSS custom properties for light/dark theming.

## License

MIT — do whatever you like with it.
