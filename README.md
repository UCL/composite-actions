‼️ This repository is no longer actively maintaned, and is therefore archived. If you're interested in reviving it, please ask someone at https://github.com/UCL-ARC ‼️


# Composite actions for GitHub Actions
Useful actions that can be used to reduce code duplication in GitHub Actions
configuration.

## What is a composite action?
A composite action is a series of steps that can be used as a step itself in another
workflow. [This blog post](https://github.blog/changelog/2021-08-25-github-actions-reduce-duplication-with-action-composition/) has a nice example of what one looks like.

## Using the actions
The actions can be used as individual steps inside jobs, e.g.:

```yaml
jobs:
  python-linting:
    name: Run linting
    runs-on: ubuntu-latest
    steps:
      - uses: ucl/composite-actions/python/tox@v1
        with:
          python-version: '3.10'
```
Any inputs are specified using `with` under `uses`. Each action is documented
in README files in their respective folders in this repository.

## Versioning
Within a major version (e.g. v1, v2) all actions will be backwards compatible.
New actions or bugfixes to existing actions will be released under a new minor version
(e.g. v1.1).

## Development
### Adding new actions
To add a new action please open a pull request. The action itself should
live under `<language>/<description>/action.yml`, e.g.
`python/tox-tests/action.yml`. Alongside the action file should be a README
that documents what the action does and any inputs/outputs. Please also add a
test in `.github/workflows/test-<language>-<description>.yml` to check that
the action works as intended.


### Releasing a new version

1. Create a new release through the GitHub releases UI. Make sure you add the appropriate tag to the release.
2. If incrementing a minor version (ie. going from 2.1 > 2.2), move the major tag (e.g. <tagname>=v2) to the most recent tag:

```bash
git push origin :refs/tags/<tagname>
git tag -fa <tagname>
git push upstream main --tags
```

  This means any actions specifying (e.g.) `v2` will automatically use the new minor version of the actions.
