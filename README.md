# Cordiverse Workflows

This repository contains a collection of GitHub Actions [reusable workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows) that can be used in other repositories.

## workflows

### Build

The build workflow contains the `build`, `lint` and `test` jobs, the `build` job is always available while `lint` and `test` job should be activated by options.

Example:

```yaml
name: Build

on:
  push:
  pull_request:
    branches: [main]
    types: [opened, synchronize, reopened, labeled, unlabeled]

jobs:
  build:
    uses: cordiverse/workflows/.github/workflows/build.yml@main
    with:
      lint: true
      test: true
```

Options:

|Name|Type|Required|Default|Description|
|:-:|:-:|:-:|:-:|:-:|
|`fetch-submodules`|`boolean`|No|`false`|Whether to fetch submodules|
|`node-version`|`string`|No|`null`|Node.js version|
|`lint`|`boolean`|No|`false`|Whether to run linting|
|`test`|`boolean`|No|`false`|Whether to run tests|
