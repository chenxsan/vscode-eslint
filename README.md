<h1 align="center">vscode-standardjs</h1>

<p align="center">
  <strong><a href="https://code.visualstudio.com/">Visual Studio Code</a> extension for <a href="https://standardjs.com">JavaScript Standard Style</a> with automatic fixing.</strong>
</p>

<p align="center">
   <a href="https://www.npmjs.com/package/ts-standard"><img alt="TypeScript Standard Style" src="https://camo.githubusercontent.com/f87caadb70f384c0361ec72ccf07714ef69a5c0a/68747470733a2f2f62616467656e2e6e65742f62616467652f636f64652532307374796c652f74732d7374616e646172642f626c75653f69636f6e3d74797065736372697074"/></a>
   <a href="https://travis-ci.org/github/standard/vscode-standardjs"><img src="https://img.shields.io/travis/standard/vscode-standardjs/master.svg" alt="Travis CI" /></a>
   <a href="https://marketplace.visualstudio.com/items?itemName=chenxsan.vscode-standardjs"><img src="https://vsmarketplacebadge.apphb.com/version/chenxsan.vscode-standardjs.svg" alt="Visual Studio Marketplace" /></a>
   <img alt="Downloads Visual Studio Marketplace" src="https://vsmarketplacebadge.apphb.com/downloads-short/chenxsan.vscode-standardjs.svg" />
   <br/> <br/>
   <a href="https://standardjs.com"><img src="https://raw.githubusercontent.com/standard/vscode-standardjs/master/standard_icon.png" alt="Standard - JavaScript Style Guide" width="200"></a>
</p>

## How to use

1. **Install the 'JavaScript Standard Style' extension**

   If you don't know how to install extensions in VSCode, take a look at the [documentation](https://code.visualstudio.com/docs/editor/extension-gallery#_browse-and-install-extensions).

   You will need to reload VSCode before new extensions can be used.

2. **Install `standard`, `semistandard`, `standardx` or `ts-standard`**

   This can be done globally or locally. We recommend that you install them locally (i.e. saved in your project's `devDependencies`), to ensure that other developers have it installed when working on the project.

3. **Disable the built-in VSCode validator**

   To do this, set `"javascript.validate.enable": false` in your VSCode `settings.json`.

## Plugin options

We give you some options to customize vscode-standardjs in your VSCode [`settings.json`](https://code.visualstudio.com/docs/getstarted/settings).

| Option                           | Description                                                                                                                                                                                                  | Default                                                             |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| `standard.enable`                | enable or disable JavaScript Standard Style                                                                                                                                                                  | `true`                                                              |
| `standard.run`                   | run linter `onSave` or `onType`                                                                                                                                                                              | `onType`                                                            |
| `standard.autoFixOnSave`         | enable or disable auto fix on save. It is only available when VSCode's `files.autoSave` is either `off`, `onFocusChange` or `onWindowChange`. It will not work with `afterDelay`.                            | `false`                                                             |
| `standard.nodePath`              | use this setting if an installed `standard` package can't be detected.                                                                                                                                       | `null`                                                              |
| `standard.validate`              | an array of language identifiers specify the files to be validated                                                                                                                                           | `["javascript", "javascriptreact", "typescript", "typescriptreact]` |
| `standard.workingDirectories`    | an array for working directories to be used.                                                                                                                                                                 | `[]`                                                                |
| `standard.engine`                | You can use `semistandard`, `standardx` or `ts-standard` instead of `standard`. **Just make sure you've installed the `semistandard`, the `standardx` or the `ts-standard` package, instead of `standard`.** | `standard`                                                          |
| `standard.usePackageJson`        | if set to `true`, JavaScript Standard Style will use project's `package.json` settings, otherwise globally installed `standard` module is used                                                               | `false`                                                             |
| `standard.treatErrorsAsWarnings` | Any linting error reported by Standard will instead be displayed as a warning within VS Code.                                                                                                                | `false`                                                             |

## Configuring Standard

You can still configure `standard` itself with the `standard.options` setting, for example:

```json
"standard.options": {
	"globals": ["$", "jQuery", "fetch"],
	"ignore": [
		"node_modules/**"
	],
	"plugins": ["html"],
	"parser": "babel-eslint",
	"envs": ["jest"]
}
```

It's recommended to change these options in your `package.json` file on a per-project basis, rather than setting them globally in `settings.json`. For example:

```json
"standard": {
	"plugins": ["html"],
	"parser": "babel-eslint"
}
```

If you've got multiple projects within a workspace (e.g. you're inside a monorepo), VSCode prevents extensions from accessing multiple `package.json` files.

If you want this functionality, you should add each project folder to your workspace (`File -> Add folder to workspace...`). If you can't see this option, download the [VSCode Insiders Build](https://code.visualstudio.com/insiders/) to get the latest features.

### Commands

When you open the Command Palette in VSCode (⇧⌘P or Ctrl+Shift+P), this plugin has the following options:

- `Fix all auto-fixable problems` - applies JavaScript Standard Style auto-fix resolutions to all fixable problems.
- `Disable JavaScript Standard Style for this Workspace` - disable JavaScript Standard Style extension for this workspace.
- `Enable JavaScript Standard Style for this Workspace` - enable JavaScript Standard Style extension for this workspace.
- `Show output channel` - view the linter output for JavaScript Standard Style.

### FAQ

1. How do I lint `script` tags in `vue` or `html` files?

   You can lint them with `eslint-plugin-html`. Make sure it's installed, then enable linting for those file types in your `settings.json`:

   ```json
   "standard.validate": [
   	"javascript",
   	"javascriptreact",
   	"html"
   ],
   "standard.options": {
   	"plugins": ["html"]
   },
   "files.associations": {
   	"*.vue": "html"
   },
   ```

   If you want to enable `autoFix` for the new languages, you should enable it yourself:

   ```json
   "standard.validate": [
   	"javascript",
   	"javascriptreact",
   	{
   		"language": "html",
   		"autoFix": true
   	}
   ],
   "standard.options": {
   	"plugins": ["html"]
   }
   ```

## How to develop

1. Fork this repo, and clone your fork locally.
2. Run `npm install` right under project root.
3. Open project in VSCode. The plugin should be disabled whilst developing.
4. Run the `watch` build task (⇧⌘B or Ctrl+Shift+B) to compile the client and server.
5. To run/debug the extension, use the `Launch Extension` launch configuration (from the VSCode debug panel).
6. To debug the server, use the `Attach to Server` launch configuration.

## How to package

1. Run `npm install`
2. Run `npm run package` to build a .vsix file
3. You can install it with `code --install-extension vscode-standardjs.vsix`

## License

[MIT](./LICENSE)
