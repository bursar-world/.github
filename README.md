# bursar-world/.github

This repository holds the public face of the Bursar organization on GitHub and the defaults every
Bursar repository falls back on.

| Path | Purpose |
|---|---|
| [`profile/README.md`](profile/README.md) | The page shown at [github.com/bursar-world](https://github.com/bursar-world). Its images and the architecture diagram source are in [`profile/assets/`](profile/assets). |
| [`SECURITY.md`](SECURITY.md), [`CONTRIBUTING.md`](CONTRIBUTING.md), [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md), [`SUPPORT.md`](SUPPORT.md), [`GOVERNANCE.md`](GOVERNANCE.md) | Policies GitHub shows for any Bursar repository that has no file of its own by the same name. |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE), [`.github/PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md) | Default issue forms and pull request template, used the same way. |
| [`workflow-templates/`](workflow-templates) | Starter CI workflows offered under **Actions → New workflow** in every Bursar repository: one for TypeScript with pnpm, one for Solidity with Foundry. |

A repository's own file always takes precedence. The [bursar](https://github.com/bursar-world/bursar)
repository has its own security policy, contribution guide and governance, and those are the ones
that apply to it.

## Updating the architecture diagram

The diagram appears twice: as a Mermaid block in `profile/README.md`, which GitHub renders, and as
`profile/assets/architecture.svg` for places that do not render Mermaid. Edit
`profile/assets/architecture.mmd`, paste it into the README block, and export the SVG:

```sh
npx -y @mermaid-js/mermaid-cli -i profile/assets/architecture.mmd \
  -o profile/assets/architecture.svg -c profile/assets/mermaid-config.json -b '#faf8f7'
```

## License

The text in this repository is available under the [MIT License](LICENSE). The Bursar name and logo
are not covered by that license.
