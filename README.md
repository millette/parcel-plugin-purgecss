# parcel-plugin-purgecss

A Parcel plugin to remove unused rules from your bundled CSS files.

## How it works

This plugin uses [purgecss](https://github.com/FullHuman/purgecss) to remove unused CSS rules.

It works by reading your source files and checking which CSS selectors are mentioned in your HTML and Javascript code.

This is very useful if you're using a full-featured CSS framework like Bootstrap or Materialize, or even Atomic CSS libraries like Tachyons or BassCSS since you might not use all the provided components and helpers.

## Usage

1. Install the plugin as a dependency in your `package.json`.
2. Create a `purgecss.config.js` file in the root of your module and fill it out with the [options you need from PurgeCSS](https://www.purgecss.com/configuration). Note that the `content` option is **required**. You can also add your options to a `purgecss` key on your `package.json`.
3. Build normally

This plugin is only enabled when `minify: true`, which means it won't run on `parcel serve`.

## Options

They are passed directly to the purgecss postcs plugin. [Here's a list of the available options.](https://www.purgecss.com/configuration)

`purgecss.config.js`:

```js
module.exports = {
  content: ["**/*.html"],
  whitelist: [".my-very-special-class"]
}
```

## Installation

```
yarn add --dev parcel-bundler parcel-plugin-purgecss
```

or

```
npm install -D parcel-bundler parcel-plugin-purgecss
```

`parcel-bundler` is a peer dependency

## Known issues

[The entry stylesheet _must_ be in your package.](https://github.com/cprecioso/parcel-plugin-purgecss/issues/10) That means that if you a stylesheet of your npm dependencies directly from a JS or HTML file, it will not be purged. If you import it directly or indirectly from another stylesheet in your main package (or SASS, Stylus, etc), it's fine.
