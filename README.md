# LED Strip Simulator for WLED

See what a [WLED](https://github.com/wled/WLED) setup looks like before you touch the LEDs: split a strip or a 2D
matrix into segments, give each one an effect, a palette and colours, and copy the JSON straight to your WLED.

[![Six segments with Fire 2012, Scanner, Theater, Colorwaves, Meteor and Ripple](images/simulator.png)](https://djlex83.github.io/wled-strip-simulator/)

[![A 32 × 16 matrix with Octopus and Noise2D](images/matrix.png)](https://djlex83.github.io/wled-strip-simulator/)

**[Open the simulator](https://djlex83.github.io/wled-strip-simulator/)** – a single web page, nothing to install.

## What it does

- **Strip:** number of LEDs (up to 1500), RGB or RGBW, master brightness and how many LEDs go in one row.
- **2D matrix:** switch the layout to *Matrix (2D)* and set width and height (up to 128 each, 4096 LEDs). Segments
  become rectangles with Start X/Stop X and Start Y/Stop Y. 1D effects are expanded like in WLED: *Pixels* (the
  matrix as one long strip), *Bar* (rows from the bottom), *Arc* (quarter circles from a corner) or *Corner*
  (L shapes). The JSON carries `startY`, `stopY` and `m12`; the matrix size itself is set in WLED under
  *Config → 2D Configuration*.
- **Segments:** split the strip into equal parts or set start and stop yourself. Each segment has its own effect,
  sliders, checkboxes, colours, palette, brightness, *reverse* and on/off, labelled like in the WLED app.
- **JSON for WLED:** the page writes the state as JSON. Send it to `POST /json/state` on your WLED, or put it into a
  preset. Effects and palettes carry their WLED numbers.
- **Import:** paste the result of `http://<your-wled>/json/state` (or an entry of `presets.json`) to see your current
  setup.
- **Share:** the whole setup lives in the page address. *Copy link* gives you a link that opens exactly this strip,
  these segments and these settings, for example to send it to someone or to keep it as a bookmark.
- **Like the real thing:** effects run at 42 frames per second like WLED, and gamma 2.8 is applied to every pixel like
  in WLED 16. A screen cannot show the brightness of real LEDs, so take the colours as an impression.
- English and German.

## Effects

50 WLED effects, written in JavaScript after the WLED 16 source code. The number is the effect ID in WLED.

**For strips (and on a matrix as expanded 1D effects):**

| ID | Effect | ID | Effect | ID | Effect |
| --: | :-- | --: | :-- | --: | :-- |
| 0 | Solid | 15 | Running | 66 | Fire 2012 |
| 1 | Blink | 16 | Saw | 67 | Colorwaves |
| 2 | Breathe | 17 | Twinkle | 74 | Colortwinkles |
| 3 | Wipe | 18 | Dissolve | 76 | Meteor |
| 8 | Colorloop | 20 | Sparkle | 79 | Ripple |
| 9 | Rainbow | 23 | Strobe | 80 | Twinklefox ≈ |
| 10 | Scan | 40 | Scanner | 85 | Spots |
| 11 | Scan Dual | 41 | Lighthouse | 89 | Fireworks Starburst ≈ |
| 12 | Fade | 43 | Rain ≈ | 90 | Fireworks 1D ≈ |
| 13 | Theater | 46 | Gradient | 92 | Sinelon |
| 14 | Theater Rainbow | 57 | Lightning | 98 | Percent |
| | | 63 | Pride 2015 | 102 | Candle Multi |

**For 2D matrices:**

| ID | Effect | ID | Effect | ID | Effect |
| --: | :-- | --: | :-- | --: | :-- |
| 126 | Octopus | 153 | Matrix | 177 | Frizzles |
| 127 | Waving Cell | 154 | Metaballs | 178 | Plasma Ball |
| 146 | Noise2D | 162 | Pulser | 180 | Hiphotic |
| 150 | Squared Swirl | 173 | Tartan | 181 | Sindots |
| 152 | DNA | 176 | Lissajous | 183 | Black Hole |

≈ marks approximations: they look like the WLED effect but do not follow its code step by step. Effects with random
parts never repeat exactly, on the strip or here.

**Palettes:** Default, \* Colors Only, Party, Cloud, Lava, Ocean, Forest, Rainbow, Rainbow Bands, Sunset, Beech and
Fire, with the same colour values as WLED 16. *Default* means the effect's own default palette, like in WLED.

When you import a state with an effect or palette the simulator does not have, it shows that segment as *Solid* or
with the *Default* palette and tells you which numbers it skipped. A state with `startY`/`stopY` (or the matrix size
from `/json/info`) switches the simulator to the matrix layout. The *Pinwheel* expansion of WLED is not simulated.

## Running it locally

[`index.html`](index.html) is the whole simulator: one file with no build step and no external libraries. Open it in
a browser or serve the folder with any static web server.

## Licence

[EUPL-1.2](LICENSE), the same licence as WLED, because the effects follow the WLED source code. The colour maths
follows WLED's slimmed-down FastLED functions.

This is an independent project. It is not part of WLED and not endorsed by the WLED team.
