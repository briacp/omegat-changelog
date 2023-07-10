# OmegaT - Release notes action

This action generates the release notes from all the bugs/RFE fixed for a milestone.

## Inputs

## `milestone`

**Required** The name (or tag) of the milestone. Everything after and including `_` is discarded (e.g. `6.1.0_1` becomes `6.1.0`). This allows generating release notes for release candidate tags of a specific milestone. Also, a trailing `.0` is removed because in the SourceForge tracker, we use `6.1` instead of `6.1.0`.

## Outputs

A file named `changes_{milestone}.txt` is created.

## Example usage

```yaml
- name: Generate OmegaT release notes
  id: release-notes
  uses: briacp/omegat-changelog@v1.0.0
  with:
    milestone: ${{ github.ref_name }}
```

## Command-line

```shell
node omegat-changelog milestone
```

For example: `node omegat-changelog v6.1.0`

## Building the action

### Bundle with NCC

To make sure everything is bundled correctly when launching the action from GitHub, the `omegat-changelog.js` and all its dependencies are compiled into a single `dist/index.js` file with `ncc`. The resulting file must be commited to git. This step avoid fetching the dependencies from the GitHub build machine.

```shell
npx ncc build omegat-changelog.js --minify --out dist
```
