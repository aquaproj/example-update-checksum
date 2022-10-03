# example-aqua-update-checksum

Example of auto update `aqua-checksums.json` in CI.

- [GitHub Actions Workflow](.github/workflows/test.yaml)

## Motivation

If you enable [aqua's checksum verification](https://aquaproj.github.io/docs/reference/checksum),
you have to update `aqua-checksums.json` when packages are updated.
If you automate the update of packages by Renovate, you should also automate the update of `aqua-checksums.json`.

This repository shows a simple example to automate the update of `aqua-checksums.json`.

[GitHub Actions Workflow](.github/workflows/test.yaml)

## Example

`aqua-checksums.json` is automatically created.

https://github.com/suzuki-shunsuke/example-aqua-update-checksum/pull/1/commits/5e068579bd3d6189f9b65f63bdbb97450e06deee

![image](https://user-images.githubusercontent.com/13323303/193704192-b313a395-a294-43c8-b154-6f4f56b2865f.png)

`aqua-checksums.json` is automatically updated.

## Reference

- https://aquaproj.github.io/docs/reference/checksum

## LICENSE

[MIT](LICENSE)
