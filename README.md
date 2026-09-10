# var-colors

**var-colors** is a Sass-based utility designed to create color palettes in the **OKLCH** color space. It allows you to use a palette of preset colors and their shades, and also allows you to flexibly customize a custom palette option.

## Features

- 25 calibrated **preset colors**.
- Up to **977 shades** of preset colors.
- Saturation stabilization for **dynamic temization**.
- **Flexible configuration** settings for preset and custom colors

## Installation

```bash
npm install var-colors
```

## Import

After installation, you can import the SCSS file into your project

```bash
@import var-colors
```

When imported, 154 shades of 8 colors will be created in the root rule. This is enough for 95% of projects. If the specified shades are not enough for you, you can use a flexible configuration system to create your own palette

## Configuration

The configuration allows you to set:

- Your set of preset colors (out of 25 preset colors)
- Lightness levels step from 25 to 500
- Custom set of lightness levels
- Saturation stabilization of preset colors shades
- Selecting the gamut from "srgb", "display-p3", "rec2020"
- Setting a prefix to avoid collisions with other libraries
- And of course, customizing a set of custom colors

You need to create a configuration file and import it before importing the utility.

### Configuration file example

```bash
$colors: (
  "grey",
  "indigo",
  "rose",
);
$levels-step: 100;
$consistent-chroma: true;
$gamut: "display-p3";
$prefix: "mv";
$custom-colors: (
  "primary": (
    hue: 295,
    max-chroma: 0.3,
    max-chroma-lightness: 0.54,
  ),
  "secondary": (
    hue: "grey"
  ),
  "danger": (
    hue: "red"
  )
)
```

### Import example

```bash
@import configuration.scss
@import var-colors
```
