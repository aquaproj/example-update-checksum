# example-aqua-update-checksum

Example of auto update `aqua-checksums.json` in CI.

- [GitHub Actions Workflow](.github/workflows/test.yaml)

## Motivation

If you enable [aqua's checksum verification](https://aquaproj.github.io/docs/reference/checksum),
you have to update `aqua-checksums.json` when packages are updated.
If you automate the update of packages by Renovate, you should also automate the update of `aqua-checksums.json`.

This repository shows a simple example to automate the update of `aqua-checksums.json`.

[GitHub Actions Workflow](.github/workflows/test.yaml)

## Reference

- https://aquaproj.github.io/docs/reference/checksum

## LICENSE

[MIT](LICENSE)
