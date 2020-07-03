# excalidraw-cli
[![npm version](https://img.shields.io/npm/v/@tommywalkie/excalidraw-cli)](https://www.npmjs.com/package/@tommywalkie/excalidraw-cli) [![Bundlephobia badge](https://badgen.net/bundlephobia/min/@tommywalkie/excalidraw-cli)](https://bundlephobia.com/result?p=@tommywalkie/excalidraw-cli@latest) ![build](https://github.com/tommywalkie/excalidraw-cli/workflows/build/badge.svg?branch=master)

Experimental Excalidraw CLI tool.

Parses Excalidraw JSON schemas (`*.excalidraw`) into PNGs (`*.png`).

This project is a follow-up to [excalidraw#1261](https://github.com/excalidraw/excalidraw/issues/1261) and strives to provide a CLI for **[excalidraw](https://github.com/excalidraw/excalidraw)**.

![demo](https://raw.githubusercontent.com/tommywalkie/excalidraw-cli/master/.github/assets/demo.gif)

_Demo_ ⤴️

## Install

```bash
npm install -g @tommywalkie/excalidraw-cli
```

## Usage

```bash
$ excalidraw-cli --help
Parses Excalidraw JSON schemas into PNGs

USAGE
  $ excalidraw-cli [INPUT] [OUTPUT]

ARGUMENTS
  INPUT   [default: {cwd}] Excalidraw file path / directory path
  OUTPUT  [default: {cwd}] Output PNG file path / directory path

OPTIONS
  -h, --help     show CLI help
  -q, --quiet    disable console outputs
  -v, --version  show CLI version
```

## How it works ?

Currently, [`excalidraw`](https://www.npmjs.com/package/excalidraw) NPM package only exports a React component. `excalidraw-cli` uses **[node-canvas](https://github.com/Automattic/node-canvas)** at its core, this allows to generate canvas without relying on the `window` context, and uses a home-made renderer which tries to _mimic_ Excalidraw's as much as possible, using [**Rough.js**](https://roughjs.com/) API primarily.

Hopefully, `excalidraw-cli` will directly use Excalidraw renderer methods for consistent results, once Excalidraw provides some Node-compatible API.

See the related issue thread [excalidraw#1780](https://github.com/excalidraw/excalidraw/issues/1780).

#### Caveats

The currently used home-made renderer now supports any Excalidraw shape element but it's not perfect, there are still a few known issues :
- Rotated objects may exceed canvas dimensions if too close of one side
- Font ligatures are not supported yet

## Contributing

> **Note**: Most of the codebase is currently in **ES2017**, it will soon be converted to **TypeScript** for educational purposes, but also for easier integration with Excalidraw.

Fork the repo and clone it on your machine.

```sh
git clone https://github.com/<MY-USERNAME>/excalidraw-cli.git
```

Install dependencies with `npm` or `yarn`.

```sh
npm install
```

Export fonts, transpile **TypeScript** / **ES2017** source into **CommonJS** for production.

```sh
npm run prepack
```

Start using the CLI in production. 

```sh
node ./bin/run           # Run with Node
npm run excalidraw-cli   # Run with NPM script
```

Prepack and launch Jest tests.

```sh
npm run test
```

You can check requested / planned / work-in-progress features in [Projects](https://github.com/tommywalkie/excalidraw-cli/projects).

## License

MIT