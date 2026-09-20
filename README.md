# var-colors

**var-colors** is a Sass-based utility designed to create color palettes in the **OKLCH** color space. It allows you to use a palette of preset colors and their shades, and also allows you to flexibly customize a custom palette option.

## Features

- 25 calibrated **preset colors**.
- Up to **977 shades** of preset colors.
- Saturation stabilization for **dynamic temization**.
- **Flexible configuration** settings for preset and custom colors
- Gamut selection: `srgb`, `display-p3`, `rec2020`.
- Generation via `@use` or mixin `@include var-colors.generate($config)`.

## Installation

```bash
npm install var-colors
```

## Usage

After installation, you can import the SCSS file into your project

```scss
@use var-colors;
```

In `:root`, **154 shades** of eight colors will appear (`grey`, `red`, `orange`, `yellow`, `green`, `cyan`, `blue`, `violet`) with a step of 50, plus `--white` and `--black`. This is enough for 95% of projects. If the specified shades are not enough for you, you can use a flexible configuration system to create your own palette

In CSS:

```css
background: var(--blue-050);
color: var(--blue-900);
```

## Configuration

The settings are defined **before** importing the package — either as separate variables or as a single map `$config`.

The configuration allows you to set:

- Your set of preset colors (out of 25 preset colors);
- Lightness levels step (`$levels-step`) from 25 to 500 (25, 50, 100, 125, 200, 250, 500) or your own list of `$levels`;
- Saturation stabilization of preset colors shades(`$consistent-chroma`);
- Selecting the gamut (`$gamut`) from "srgb", "display-p3", "rec2020";
- Setting a prefix (`$prefix`) to avoid collisions with other libraries;
- Entry in `:root` or only in the Sass map `$palette` (`$root-rule`);
- And of course, your own set of custom colors.

### Configuration example

```scss
@use "var-colors" with (
  $colors: (
    "grey",
    "indigo",
    "rose",
  ),
  $levels-step: 100,
  $consistent-chroma: true
);
```

### Configuration from file example

```scss
$config: (
  colors: (
    "grey",
    "indigo",
    "rose",
  ),
  levels-step: 100,
  consistent-chroma: true,
  gamut: "display-p3",
  prefix: "vc",
  root-rule: true,
  custom-colors: (
    "primary": (
      hue: 295,
      max-chroma: 0.3,
      max-chroma-lightness: 0.54,
    ),
    "secondary": (
      hue: "grey",
    ),
    "danger": (
      hue: "red",
    ),
  ),
);
```

```scss
@use "configuration" as vc;
@use "var-colors" with (
  $config: vc.$config
);
```

## Generation via mixin

For modular Sass (`@use`), auto‑generation during loading needs to be disabled; otherwise, the palette will be collected twice:

```scss
@use "var-colors" with (
  $auto-generate: false
);

@include var-colors.generate(
  (
    colors: (
      "grey",
      "indigo",
    ),
    levels-step: 100,
    gamut: "display-p3",
    prefix: "vc",
    root-rule: true,
    custom-colors: (
      "primary": (
        hue: 295,
        max-chroma: 0.3,
      ),
    ),
  )
);
```

If `$root-rule: false`, CSS variables are not written: the result remains in `$palette` (and `$var-hues` for dynamic shades) — this is convenient for your own utilities or for exporting tokens.

## Custom colors

Each color has its own `hue` set:

- the hue number (`295`) — a unique brand identifier;
- the preset name (`"red"`) — calibration of the finished color to a semantic name;
- `none` — without saturation (like `grey`).

Optional: `max-chroma`, `max-chroma-lightness`, `var-hue: true` — in this case, the hue is stored in `--primary-hue` and can be changed in CSS without recompiling Sass. For a live hue change, it’s better to enable `$max-chroma: "consistent"`.
