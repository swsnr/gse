# gsebuild

![NPM Version](https://img.shields.io/npm/v/%40swsnr%2Fgsebuild)
![CI status](https://img.shields.io/github/actions/workflow/status/swsnr/gsebuild/ci.yaml)
![Apache 2.0 license](https://img.shields.io/github/license/swsnr/gsebuild)

Some kind of a build tool for GNOME extensions.

This tool adds some scaffolding for building GNOME Shell extensions, especially with Typescript:

- Provide recommended eslint and tsc configurations.

Planned features:

- Pack extensions from a conventional layout.
- Compile blueprint files to builder XML.
- Extract messages from sources and UI/BLP files with xgettext.
- Submit to extensions.gnome.org

## Installation

```console
$ npm install --save-dev @swsnr/gsebuild
```

## Setup

### Typescript

```console
$ npm install --save-dev typescript eslint
```

Then create a `tsconfig.json`:

```json
{
  "extends": "@swsnr/gsebuild/tsconfig.json",
  "compilerOptions": {
    "outDir": "build"
  },
  // ...
}
```

And a eslint configuration file `eslint.config.dist.js` to reformat typescript for submission to extensions.gnome.org:

```javascript
import eslint from "@swsnr/gsebuild/eslint";

export default [
  eslint.config.dist,
  {
    files: ["build/**/*"],
  },
];
```

Then add `package.json` scripts to build Typescript:

```json
{
    "scripts": {
        "compile": "tsc --build tsconfig.json",
        "postcompile": "eslint --no-config-lookup --config eslint.config.dist.js --quiet --fix ."
    }
}
```
