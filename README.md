**Looking for pre-Daylight icons?** They're [over here](https://github.com/Brightspace/d2l-icons-ui/tree/pre-daylight).

# d2l-icons
[![Bower version][bower-image]][bower-url]
[![Build status][ci-image]][ci-url]

`d2l-icons` contains SVGs, [Polymer](https://www.polymer-project.org/1.0/)-based web components and [Sass mixins](http://sass-lang.com) to incorporate D2L iconography into your application.

For further information on this and other D2L UI components, see the docs at [ui.valence.d2l.com](http://ui.valence.d2l.com/).

## Installation

`d2l-icons` can be installed from [Bower][bower-url]:
```shell
bower install d2l-icons
```

## Icon Categories

Each icon is grouped into a category, and every icon in a particular category has the same native size.

Currently, there are 4 icon categories:

| Name | Description | Samples | Size | List |
| :----: | --- | :---: | :---: | :---: |
| tier1 | general icons | ![print](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier1/print.svg?raw=true)&nbsp;&nbsp; ![gear](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier1/gear.svg?raw=true)&nbsp;&nbsp; ![save](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier1/save.svg?raw=true) | `18px` x `18px` | [Full set](d2l-icons.md#tier1) |
| tier2 | general icons | ![audio](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier2/file-audio.svg?raw=true)&nbsp;&nbsp; ![copy](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier2/copy.svg?raw=true)&nbsp;&nbsp; ![news](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier2/news.svg?raw=true) | `24px` x `24px` | [Full set](d2l-icons.md#tier2) |
| tier3 | general icons | ![notifications](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier3/notification-bell.svg?raw=true)&nbsp;&nbsp; ![help](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier3/help.svg?raw=true)&nbsp;&nbsp; ![search](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/tier3/search.svg?raw=true) | `30px` x `30px` | [Full set](d2l-icons.md#tier3) |
| html-editor | for use in the HTML editor | ![](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/html-editor/bold.svg?raw=true)&nbsp;&nbsp; ![](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/html-editor/indent-decrease.svg?raw=true)&nbsp;&nbsp; ![](https://cdn.rawgit.com/Brightspace/d2l-icons-ui/master/images/html-editor/source-editor.svg?raw=true) | `18px` x `18px` | [Full set](d2l-icons.md#html-editor) |

**[&gt; Browse ALL categories and icons](d2l-icons.md)**

**Note:** Always choose the icon whose native size best matches your desired icon size, ideally exactly.

## Usage

There are many ways to consume icons -- the best technique depends on your application and use case.

### Polymer Icon Sets

If your application is using Google's [Polymer](https://www.polymer-project.org/1.0/) framework, `d2l-icons` exposes [iron-iconset-svg](https://elements.polymer-project.org/elements/iron-iconset-svg) collections for usage with the Polymer [iron-icon](https://elements.polymer-project.org/elements/iron-icon) web component.

An iconset collection is available for each category (tier1, tier2, etc.), named `{category}-icons.html`. Also, an HTML import which imports ALL categories is also available by including `d2l-icons.html`.

Here's an example which consumes the "bookmark-filled" icon from the "tier1" category using an `iron-icon` web component:
```html
<link rel="import" href="../polymer/polymer.html">
<link rel="import" href="../iron-icon/iron-icon.html">
<link rel="import" href="../d2l-icons/tier1-icons.html">
<button>
	<iron-icon icon="d2l-tier1:bookmark-filled"></iron-icon>
	Bookmark
</button>
```

You'll need to set the size (ideally 18px, 24px or 30px) and color (tungsten) of the icon. [d2l-colors](https://github.com/Brightspace/d2l-colors-ui) comes in handy:

```html
<link rel="import" href="../d2l-colors/d2l-colors.html">
<style include="d2l-colors">
iron-icon {
	color: var(--d2l-color-tungsten);
	--iron-icon-height: 18px;
	--iron-icon-width: 18px;
}
</style>
```

If you'd like a different color when the user hovers:
```css
button:hover iron-icon, button:focus iron-icon {
	color: var(--d2l-color-celestuba);
}
```

### &lt;d2l-icon&gt; Web Component

Using Google's [iron-iconset-svg](https://elements.polymer-project.org/elements/iron-iconset-svg) and [iron-icon](https://elements.polymer-project.org/elements/iron-icon) directly (see above) works just fine, however we've created a wrapper component called `<d2l-icon>` which will automatically set the correct icon size and color.

Use it identically to `<iron-icon>`:
```html
<link rel="import" href="../polymer/polymer.html">
<link rel="import" href="../d2l-icons/d2l-icon.html">
<link rel="import" href="../d2l-icons/tier1-icons.html">
<button>
	<d2l-icon icon="d2l-tier1:bookmark-filled"></d2l-icon>
	Bookmark
</button>
```

The color will default to tungsten, and the size will be set automatically based on the category name.

To swap the color on-hover:
```css
button:hover d2l-icon, button:focus d2l-icon  {
	color: var(--d2l-color-celestuba);
}
```

#### Right-to-Left

If your application is being rendered in a right-to-left direction, `<d2l-icon>` will automatically flip the image horizontally.

This is typically desired, however in some cases flipping the icon will cause it to lose important meaning (e.g. the "B" bold icon). In those cases, set the `no-rtl` attribute:

```html
<d2l-icon icon="d2l-html-editor:bold" no-rtl></d2l-icon>
```

### Directly with an `<img>` element

Simply point an HTML `<img>` element's `src` attribute at the icon's SVG file. You can reference the files directly from `bower_components`, or copy the icons you need as part of your application's build process.

HTML:
```html
<img src="bower_components/d2l-icons/images/tier1/bookmark-filled.svg" alt="bookmarked" />
```

Don't forget to provide alternate text if the icon isn't accompanied by any other text.

### Background Images

In cases where the icon is purely decorative (it doesn't provide any additional information) and is accompanied by text and/or a tooltip, applying the icon using a background image is a good approach. It hides the icon from assistive technology (like a screen reader), allowing the accompanying text to stand alone.

First, create some CSS that points at the image you'd like and sets the correct size:

```
.my-app-bookmark-icon {
	background: url('bower_components/d2l-icons/tier1/bookmark-filled.svg');
	background-size: 18px 18px; /* needed for IE */
	display: inline-block;
	height: 18px;
	width: 18px;
}
```

Then apply the CSS class to an element:
```html
<button>
	<span class="my-app-bookmark-icon"></span>
	Bookmark
</button>
```

#### Background images with invisible text

If you would prefer the text accompanying the icon to be invisible, the background image approach can be combined with off-screen text. The text will be positioned outside of the visible screen area using CSS, essentially hiding it for everyone except those using assistive devices.

To position something off-screen, you can either use the [vui-offscreen](https://github.com/Brightspace/d2l-offscreen-ui) component, or follow [WebAIM's text-indent technique](http://webaim.org/techniques/css/invisiblecontent/).

For example, a button which contains only an icon:
```html
<link rel="import" href="../d2l-offscreen/d2l-offscreen.html">
<button title="Bookmark">
	<span class="my-app-bookmark-icon"></span>
	<d2l-offscreen>Bookmark</d2l-offscreen>
</button>
```

We've used the `title` attribute in this example to display tooltips on-hover.

#### Sass Mixins

If you'd like to use the [Sass](http://sass-lang.com) extension language in your application, `d2l-icons` provides an `icons.scss` file you can import which contains mixins to generate the background image CSS.

Import the mixin file and [include it](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#including_a_mixin) in a CSS class for each of the icons you'd like to use:

```scss
@import "bower_components/d2l-icons/icons.scss";

.my-app-bookmark-icon {
	@include d2l-icon-tier1-bookmark-hollow();
}

.my-app-print-icon {
	@include d2l-icon-tier1-print();
}
```

The name of the mixin will correspond to its location within the `images` directory, plus the subdirectory/category (e.g. `tier1`, `tier2`), plus the icon's filename -- all separated by hyphens.

Finally, consume the CSS class in your markup as before.

```html
<button>
	<span class="my-app-bookmark-icon"></span>
	Bookmark
</button>
```

## Coding styles

### Updating or contributing new icons

#### SVG format

When contributing changes to icons, the SVG files should be properly formatted. Follow these rules:
- native icon sizes need to be one of: 18, 24 or 30
- the `<svg>` element must:
  - have a `width` and `height` attribute which match the native size
  - not have an `id` or `data-name` attribute
- the `<svg>`'s `viewBox` attribute must:
  - have an origin beginning at `0 0`
  - be exactly square (e.g. `0 0 18 18`)
  - match the icon's native size
  - not contain negative values
- there should be no `<title>` element
- there should be no inline `<style>` -- all style for line fills should be applied directly to the SVG elements
- color of SVG elements should be "tungsten" (#72777a)

The best way to have most of these rules applied for you automatically is to put the icon through [SVGOMG](https://jakearchibald.github.io/svgomg/) with the "remove title" and "prettify code" options selected.

Here's a sample of a properly formatted SVG:

```svg
<svg width="18" height="18" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 18 18">
  <path fill="#72777a" d="..."/>
</svg>
```

#### Auto-generated files

The Polymer iconset files and Sass `icons.scss` file are automatically generated, so when making icon modifications, re-generate these files by running `npm run build`.

### General

See the [VUI Best Practices & Style Guide](https://github.com/Brightspace/valence-ui-docs/wiki/Best-Practices-&-Style-Guide) for information on VUI naming conventions, plus information about the [EditorConfig](http://editorconfig.org) rules used in this repo.

[bower-url]: http://bower.io/search/?q=d2l-icons
[bower-image]: https://img.shields.io/bower/v/d2l-icons.svg
[ci-url]: https://travis-ci.org/Brightspace/d2l-icons-ui
[ci-image]: https://travis-ci.org/Brightspace/d2l-icons-ui.svg?branch=master
