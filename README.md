# python-health-checks

This is a github action that you can use to set up a [pipenv based](https://pipenv.pypa.io/en/latest/index.html) python health check.

You can use it as follows in a `.github/workflows` `*.yml` file -

## use the action
build pipenv (use cached dependencies if possible) and then run linting, type, and style checking
```yml
...

jobs:
  your_job:
    steps:
      - name: 'set up python and run health checks'
        uses: equator-analytics/python-health-checks/health-check@main
```

or if you just want something to build and cache the pipenv dependencies
```yml
...

jobs:
  your_job:
    steps:
      - name: 'set up python and run health checks'
        uses: equator-analytics/python-health-checks/build@main
```

## use the composite workflow

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
