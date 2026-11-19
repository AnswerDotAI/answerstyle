# AnswerStyle source

The notebooks in `nbs/` own the styles. A `#| asset styles.css` cell contains a CSS string. `nbdev-export` joins these sections in notebook and cell order. The palette notebook can regenerate `nbs/palette.css` from the color calculations. Export reads that file without rerunning the calculations.

Run `npm run build` to export the styles using nbdev from your Python environment. `answerstyle/assets/` contains the generated styles, fonts and dependency-free browser modules. `npm pack` and `uv build` package those assets without running the notebooks. Keep the generated styles up to date with their source.

Run the examples in a notebook. `from answerstyle.preview import preview` renders a markup string in an isolated frame using the built stylesheet. Use `width='24rem'` for a narrow viewport or `height='10rem'` for top-layer content. The saved notebook keeps the example markup. Run `uv run --extra dev nbdev-preview` for the docs site.

Both distributions ship the same browser modules. `floating.js` uses CSS anchor positioning with a small geometry fallback. `interactions.js` supplies tabs, toolbar focus and hover-opening settings. Neither needs a bundler or a JavaScript dependency.

Both distributions use the same version. Consumers declare an ordinary `@answerdotai/answerstyle` version dependency. In a fastws workspace, include `AnswerDotAI/answerstyle[dev]` in the repo list: `ws-sync` installs the Python development dependencies, links the local npm package and exports its styles before building dependent apps. No per-consumer link or checkout path is needed. Outside the workspace, use the published package or a built package artifact.

## Release

For the first npm release, commit and push the reviewed changes, build with `npm run build`, then publish once using your normal authenticated `npm publish`. [npm requires the package to exist](https://docs.npmjs.com/cli/v12/commands/npm-trust/) before a trusted publisher can be configured.

Configure npm's trusted publisher for `@answerdotai/answerstyle` with GitHub owner `AnswerDotAI`, repository `answerstyle` and workflow `ci.yml`, selecting [**Allow npm publish**](https://docs.npmjs.com/trusted-publishers/) rather than the default staged-publishing action. Register PyPI's pending trusted publisher for `answerstyle` with the same repository and workflow before its first release. The workflow uses no GitHub environment or registry tokens.

After that initial npm publication, run `ship-bump` to advance both `answerstyle/__init__.py` and `package.json` before the first tag-driven release, since the bootstrap version already exists on npm. Commit and push the reviewed changes, then run `ship-release`.

For subsequent releases, commit and push the reviewed changes, then run `ship-release`. It tags the current shared version; the workflow exports the assets and publishes both packages through trusted publishing. Fastship bumps both version files for the next release.
