# Dual-Fonter
![Dual-Fonter Demo](https://github.com/domz-1/dual-fonter/blob/main/public/dual-fonter.png)

A lightweight, CSS-only library for handling dual-script fonts (Arabic and Latin) with easy variable customization.

## Features

- 🎨 **CSS-Only**: No JavaScript required.
- 🌍 **Dual-Script Support**: Automatically handles Latin and Arabic fonts.
- 🔧 **Customizable**: Easily override fonts using CSS variables.
- 🍎 **Emoji Support**: Uses system emoji fonts for a lightweight footprint.
- 📦 **Framework Agnostic**: Works with HTML, React, Vue, Angular, Svelte, etc.

## Installation

```bash
npm install dual-fonter
# or
yarn add dual-fonter
# or
pnpm add dual-fonter
```

## Usage

### 1. Import the CSS

#### HTML

```html
<link rel="stylesheet" href="node_modules/dual-fonter/src/css/dual-fonter.css" />
```

#### React / Next.js / Vue

Import it in your main entry file (e.g., `_app.js`, `main.ts`, `index.js`):

```javascript
import 'dual-fonter/css';
```

#### Angular

Add it to your `angular.json` styles array:

```json
"styles": [
  "src/styles.css",
  "node_modules/dual-fonter/src/css/dual-fonter.css"
]
```

#### Tailwind CSS

Import it in your main CSS file:

```css
@import 'dual-fonter/css';

@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 2. Apply Fonts

#### Global Application

To apply the dual-font stack globally to all elements:

```css
* {
  font-family: var(--dual-font);
}
```

#### Specific Elements

You can also apply it to specific elements using the `data-dual-font` attribute:

```html
<div data-dual-font>Hello World مرحبا بكم</div>
```

#### Any Selector

You can use the `dual-fonter` font stack with **any** CSS selector. Just apply the `--dual-font` variable to your desired class, ID, or element.

```css
/* Apply to a specific class */
.my-custom-text {
  font-family: var(--dual-font);
}

/* Apply to headings */
h1,
h2,
h3 {
  font-family: var(--dual-font);
}

/* Apply to an ID */
#special-section {
  font-family: var(--dual-font);
}
```

### 3. Customizing Fonts

You can override the default fonts by setting the CSS variables. You can do this globally in `:root` or locally on any element.

#### Global Override

```css
:root {
  --latin-font: 'Rubik', sans-serif;
  --arabic-font: 'IBM Plex Sans Arabic', sans-serif;
}
```

> [!IMPORTANT]
> **Avoid Generic Font Families in `--latin-font`**: Do not include generic families like `sans-serif`, `serif`, or `monospace` in the `--latin-font` variable. Many system generic fonts support Arabic characters, which will cause the browser to use them instead of falling back to your specified `--arabic-font`.
>
> **Correct**: `--latin-font: 'Rubik';`
> **Incorrect**: `--latin-font: 'Rubik', sans-serif;`

#### Local Override

```html
<div style="--latin-font: 'Open Sans'; --arabic-font: 'Amiri';">Custom Fonts Here</div>
```

## Emoji Support

### System Emojis

The library now relies on the operating system's default emoji fonts. This ensures the library remains lightweight and performant.

- **macOS / iOS**: Apple Color Emoji
- **Windows**: Segoe UI Emoji
- **Android**: Noto Color Emoji
- **Linux**: Noto Color Emoji or system default

### Using a Different Emoji Font

If you prefer to use a different emoji font (e.g., `Noto Color Emoji` or system defaults), you can override the `--emoji-font` variable:

```css
:root {
  /* Use Noto Color Emoji */
  --emoji-font: 'Noto Color Emoji', sans-serif;

  /* OR Use System Defaults */
  --emoji-font: 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji', sans-serif;
}
```

## CSS Reference

### Variables

| Variable        | Default                                                                | Description                                         |
| --------------- | ---------------------------------------------------------------------- | --------------------------------------------------- |
| `--latin-font`  | `'Poppins', sans-serif`                                                | Font family for Latin characters.                   |
| `--arabic-font` | `'IBM Plex Sans Arabic', sans-serif`                                   | Font family for Arabic characters.                  |
| `--emoji-font`  | `'Apple Color Emoji', 'Segoe UI Emoji', ...`                           | Font family for Emoji characters (System defaults). |
| `--dual-font`   | `var(--latin-font), var(--arabic-font), var(--emoji-font), sans-serif` | The combined font stack.                            |

### Utility Classes

| Class              | Description                                  |
| ------------------ | -------------------------------------------- |
| `.df-ar`           | Forces the Arabic font family.               |
| `.df-en`           | Forces the Latin font family.                |
| `.df-em`           | Forces the Emoji font family.                |
| `[data-dual-font]` | Applies the dual-font stack (`--dual-font`). |

## Troubleshooting

### Arabic Font Not Applying

If your Arabic text looks like a generic system font (or matches the English font), it likely means the **Arabic font is not loading**.

1.  **Check Imports**: Ensure you have imported the fonts (e.g., from Google Fonts) in your HTML or CSS. The library does _not_ include the font files for `Poppins` or `IBM Plex Sans Arabic` by default.
2.  **Verify Network**: Check your browser's network tab to ensure the font files are downloading successfully.
3.  **Font Names**: Ensure the font family names in your variables match exactly what is defined in the `@font-face` rules.

### "English" Font Used for Arabic

This happens if the Latin font (defined in `--latin-font`) includes Arabic glyphs (e.g., Arial, San Francisco) or if the stack falls back to a system font.

- **Solution**: Ensure your `--latin-font` is a font that _only_ supports Latin (like `Poppins`, `Rubik`, etc.) and that it is loading correctly.
- **Advanced Fix**: If you must use a Latin font that includes Arabic, you will need to define it using `@font-face` with a `unicode-range` that excludes Arabic, or put the Arabic font first in the stack (which might affect English text).

## License

ISC
