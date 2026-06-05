# CSS Minecraft

A Minecraft clone made with pure HTML & CSS – no JavaScript.

Play the game: [benjaminaster.com/css-minecraft](https://benjaminaster.com/css-minecraft/)

![screenshot of CSS Minecraft](./assets/screenshot.png)

## Project overview

This project renders a small Minecraft-style world directly in the DOM using Pug and SCSS.

There is no JavaScript controlling the game state. The interaction works through HTML radio inputs, labels, CSS selectors, `:has()`, 3D transforms and paused CSS animations.

## Source files

The repository should keep the source files:

```text
index.pug
main.scss
icons.css
assets/
README.md
```

The generated files do not need to be committed:

```text
index.html
main.css
main.css.map
```

These files can be regenerated locally from the source files.

## Requirements

You need Node.js and the following CLI tools:

```bash
npm install -g pug-cli sass
```

You can also run the tools with `npx` instead of installing them globally.

## Build

Generate the compiled HTML and CSS:

```bash
pug index.pug
sass main.scss:main.css
```

This creates:

```text
index.html
main.css
main.css.map
```

## Build without global installs

```bash
npx pug index.pug
npx sass main.scss:main.css
```

## Watch mode

During development, you can keep both compilers running:

```bash
pug index.pug -w
sass main.scss:main.css -w
```

## Run locally

After compiling, open `index.html` directly in the browser or use a local static server.

Example:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## World configuration

The world size is configured at the top of `index.pug`:

```pug
- const world = { layers: 9, rows: 9, columns: 9 };
```

These values mean:

- `layers`: vertical height of the world.
- `rows`: depth of the world.
- `columns`: width of the world.

The default world is:

```text
9 layers * 9 rows * 9 columns = 729 world positions
```

## Performance note

This project creates the interactive world directly in HTML.

Each position creates one radio group and one cube option per block type. Each cube also includes labels for the cube faces.

Because of that, increasing the world size can quickly make the DOM much heavier.

Recommended presets:

```pug
// Small
- const world = { layers: 7, rows: 7, columns: 7 };

// Default
- const world = { layers: 9, rows: 9, columns: 9 };

// Large
- const world = { layers: 11, rows: 11, columns: 11 };
```

For larger worlds, a JavaScript-based version would be more appropriate because it could render only the visible or changed blocks instead of generating every possible block state in advance.

## Browser support

This project requires support for the CSS `:has()` pseudo-class.

Modern Chromium, Safari and Firefox versions support it, but older browsers may not work correctly.
