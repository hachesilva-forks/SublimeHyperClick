# Sublime HyperClick
Quickly and easily jump between your files.
The missing part of `Go to definition` functionality in Sublime.

![sublime hyperclick](https://cloud.githubusercontent.com/assets/3202/19578519/51558bb4-971c-11e6-8ef2-d256da53d1da.gif)

When you are navigating and reading a codebase, you need to jump between required/imported/included files.

HyperClick detects references to these files and lets you jump right to them, by pressing a key or clicking on an icon next to the filename.

Unlike Sublime Text's `Goto Definition`, HyperClick knows some specifics of the languages it supports, so even package names and filenames without an extension can be detected.

## Supported Languages

- JavaScript
- TypeScript
- Vue components
- Svelte components
- CSS
- Sass and SCSS
- LESS
- Stylus
- HTML
- PHP
- Twig
- Pug
- Nunjucks
- JSTL
- Jinja2
- Dart
- PostCSS
- SugarML
- SugarSS

If you'd like to request another language, [open an issue](https://github.com/aziz/SublimeHyperClick/issues) with an example project in that language.

## Installation
You can install HyperClick via [Sublime Package Control](https://packagecontrol.io/).

## Usage

HyperClick gives you three different ways to navigate:

### 1. Green arrows to the right of _imports_
In Sublime Text 3, you can jump to the file by clicking the arrow to the right of the filename.

This arrow shows up when you **hover your mouse cursor** or **move to the line** (with up/down keys, or Goto Line) that contains the filename.

### 2. Context Menu
If you right click on a required/imported line you'll get a `Jump To Source File ➜` menu item on the context menu.

<img width="748" alt="sublimehyperclickcontext" src="https://cloud.githubusercontent.com/assets/3202/19578923/480cacde-971e-11e6-9504-91c26737c486.png">

### 3. Shortcut key
By default, HyperClick uses <kbd>F12</kbd> (Sublime's default `Go to definition`) shortcut.

This does not override the default functionality since it's only using it in contexts that Sublime's own `Go to definition` cannot help you navigate.

You can still customize the shortcut by adding this code to your own key-binding settings.

```json
{
    "keys": ["f12"],
    "command": "hyper_click_jump",
    "context": [{ "key": "hyper_click_jump_line", "operand": true }]
}
```

## Settings
You can customize HyperClick settings by going to
`Preferences > Package Settings > HyperClick > Settings`

#### Disable Annotations (phantom arrow button)
If you don't like the arrow button, you can disable it by setting `annotations_enabled` to `false`

#### Change Annotations contents
HyperClick uses a greenish button with `➜` when it finds the destination file and a reddish button with `✘`. These symbols can be customized too.

```json
{
  "annotation_found_text": "➜",
  "annotation_not_found_text": "✘"
}
```

#### Default Settings
See [hyper_click.sublime-settings](https://github.com/aziz/SublimeHyperClick/blob/master/hyper_click.sublime-settings) for up to date settings.

## Project settings

Some languages and build tools let developers reference files without writing out the full path to the file.

You can use [project settings](https://www.sublimetext.com/docs/3/projects.html) to configure HyperClick to look for files at specific dirs, though the settings `"lookup_paths"` and `"aliases"`.

To open the project settings file, go to `Project > Settings`.

If the `Settings` option is grayed out, choose the option `Save Project As...` (right above it) to save it to disk. The `Settings` option can now be clicked.

### Project settings example

```json
{
	"folders":
	[
		{
			"path": "/computer/jane/projects/a-great-app"
		}
	],
	"settings": {
		"hyper_click": {
			"aliases": {
				"js": {
					"@": "src"
				}
			},
			"lookup_paths": {
				"twig": [
					"templates"
				]
			}
		}
	}
}
```

### Lookup paths

When an imported file can't be found inside the same directory as the file, HyperClick will search inside the directories set in `"lookup_paths"`.

### Aliases

An alias is a character or word at the start of the filename that maps to a fixed directory location inside the project.

Here's an example: by default, [vue-cli](https://cli.vuejs.org) uses `@` as an alias to the directory `src` inside the project. When you write
```js
import Toolbar from '@/components/Toolbar';
```

HyperClick will recognize it as the file `src/components/Toolbar.vue` in your project.

Tools that support aliases:

- [Webpack](https://webpack.js.org/configuration/resolve/#resolvealias)
- [vue-cli](https://cli.vuejs.org/guide/html-and-static-assets.html#url-transform-rules) comes with `@` aliased to `src` by default
- [Rollup](https://github.com/rollup/plugins/tree/master/packages/alias)
- [Parcel](https://parceljs.org/module_resolution.html#aliases)


## License
Copyright 2016-2017 [Allen Bargi](https://twitter.com/aziz).

Licensed under the MIT License
