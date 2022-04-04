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
      - uses: ucl/gh-actions/python/tox@v1
        with:
          python-version: '3.10'
```
Any inputs are specified using `with` under `uses`. Each action is documented
in README files in their respective folders in this repository.


## Adding new actions
To add a new action please open a pull request. The action itself should
live under `<language>/<description>/action.yml`, e.g.
`python/tox-tests/action.yml`. Alongside the action file should be a README
that documents what the action does and any inputs/outputs. Please also add a
test in `.github/workflows/test-<language>-<description>.yml` to check that
the action works as intended.
