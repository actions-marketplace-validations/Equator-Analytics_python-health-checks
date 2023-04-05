# python-health-checks

This is a github action that you can use to set up a [pipenv based](https://pipenv.pypa.io/en/latest/index.html) python health check.

You can use it as follows in a `.github/workflows` `*.yml` file -

```yml
name: Your Python Github Action
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
permissions:
  contents: read

jobs:
  health-checks:
    uses: equator-analytics/python-health-checks/.github/workflows/python-health-checks.yml@main
```

You will of course need to set up the following commands in your `Pipfile` -
* `lint`
* `style-check`
* `type-check`
* `test`
