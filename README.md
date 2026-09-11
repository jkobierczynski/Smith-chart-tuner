# Smith Chart Tuner

An interactive, single-page simulation of an antenna tuner: drag the series
and shunt elements of an L-network (or hit Auto-Tune) and watch the effect
ripple through an analog SWR meter, a live Smith chart, and a pair of
forward/reflected waveform scopes — all driven by the same underlying
transmission-line math, not canned animations.

Open `index.html` in any modern browser. There is nothing to build or
install; the whole tool is one static HTML file.

## What it shows

- **SWR meter** — an analog cross-needle-style gauge reading VSWR from the
  reflection coefficient at the transmitter, with forward/reflected power
  bars (100 W assumed carrier).
- **Antenna & frequency** — a few illustrative antenna presets (a resonant
  dipole, a short mobile whip, an end-fed long wire, and a flat 50 Ω
  reference load) whose feedpoint impedance shifts with frequency using a
  simplified resonance model.
- **Antenna tuner (L-network)** — two tuning controls, a series reactance
  and a shunt susceptance, in either signal-path order (series-then-shunt
  or shunt-then-series). Each is labeled with the equivalent inductor or
  capacitor value at the current frequency. An **Auto-Tune** button solves
  the exact L-match analytically (flipping the signal-path order on its
  own if the one you've selected has no solution for the current load).
- **Smith chart** — a normalized (Z₀ = 50 Ω) impedance chart with true
  circular grid geometry. It plots the antenna's raw reflection
  coefficient, the trajectory each tuning element sweeps (series moves
  along a constant-resistance circle, shunt moves along a
  constant-conductance circle), and the impedance the transmitter actually
  sees.
- **Forward & reflected waves** — two oscilloscope-style panels comparing
  the sent and reflected sine waves, with their real amplitude ratio and
  phase, at the antenna (before the tuner) and at the transmitter (after
  it) — making it visible that the tuner only fixes what the transmitter
  sees, not the standing waves on the feedline itself.
- **Movable layout** — every panel can be dragged by its header into any
  order; the arrangement is remembered locally (via `localStorage`) and a
  "Reset layout" button restores the default.

## How it works

Everything is derived from a handful of closed-form transmission-line
relationships, computed live in plain JavaScript:

- Reflection coefficient: Γ = (Z − Z₀) / (Z + Z₀)
- VSWR: (1 + |Γ|) / (1 − |Γ|)
- The Smith chart grid (constant-resistance circles, constant-reactance
  arcs) is drawn from its exact center/radius in the Γ-plane, not
  approximated, so it stays perfectly round at any zoom level.
- The L-network auto-tune solver matches a complex load to a real Z₀
  analytically (the standard "Q-based" L-match formulas), rather than
  searching numerically.

Feedpoint impedances for the antenna presets are simplified, illustrative
curves for teaching purposes — not measured antenna data.

## Files

```
index.html   the entire application (HTML, CSS, and JavaScript — no build step)
LICENSE      GNU General Public License v3.0
README.md    this file
```

## Requirements

Any reasonably current desktop or mobile browser. An internet connection
is used only to load the IBM Plex Sans/Mono webfonts from Google Fonts;
without it the page still works fine and falls back to your system fonts.

## License

Licensed under the GNU General Public License v3.0 — see [LICENSE](LICENSE)
for the full text. In short: you're free to use, study, modify, and
redistribute this software, including commercially, as long as derivative
works are also distributed under the GPL-3.0 with source available.
