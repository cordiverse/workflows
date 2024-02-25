# Cordiverse Workflows

This repository contains a collection of GitHub Actions [reusable workflows](https://docs.github.com/en/actions/learn-github-actions/reusing-workflows) that can be used in other repositories.

## Workflows

### Build

The build workflow contains the `build`, `lint` and `test` jobs, the `build` job is always available while options should activate the `lint` and the `test` job.

Every job in the build workflow would checkout the current repository first, then run the `yarn` and `yarn build` commands iteratively.

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

### Publish

The publish workflow contains the `publish` job, which can publish your plugin(s) onto [`npmjs.com`](https://npmjs.com).

The `publish` job would checkout the current repository fist, then run the `yarn`, `yarn build` and `yarn pub` commands iteratively. You should pass the `NPM_TOKEN` to the workflow with the `secrets` option, see below for details.

Example:

```yaml
name: Publish

on:
  push:
    branches:
      - main

jobs:
  publish:
    uses: cordiverse/workflows/.github/workflows/publish.yml@main
    # or you can also set `secrets: { inherits: true }` to inherit every secret.
    secrets:
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

Options:

|Name|Type|Required|Default|Description|
|:-:|:-:|:-:|:-:|:-:|
|`fetch-submodules`|`boolean`|No|`false`|Whether to fetch submodules|
|`node-version`|`string`|No|`null`|Node.js version|

Secrets:

|Name|Required|Default|Description|
|:-:|:-:|:-:|:-:|
|`NPM_TOKEN`|Yes|null|The token used for publishing plugins on npmjs.com|
