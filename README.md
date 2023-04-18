# python-health-checks

This is a github action that you can use to set up a [pipenv based](https://pipenv.pypa.io/en/latest/index.html) python health check.

You can use it as follows in a `.github/workflows` `*.yml` file -

## Prequisites
You will need to set up the following commands in your `Pipfile`.
* `lint`
* `style-check`
* `type-check`

### Prequisite tools we recommend
You can set up the pipenv scripts however you wish. We use the following -
```
lint = "flake8 <YOUR_SRC_DIRECTORIES>"
style-check = "black -l 88 <YOUR_SRC_DIRECTORIES> --check"
type-check = "mypy <YOUR_SRC_DIRECTORIES>"
```

see: [flake8](https://flake8.pycqa.org/en/latest/), [black](https://github.com/psf/black), and [mypy](https://www.mypy-lang.org/)

note: if you also choose to use flake8 and black, you will need to set up custom compatability config for [flake8/black like so](https://black.readthedocs.io/en/stable/guides/using_black_with_other_tools.html#flake8), which you can add to a `.flake8` config file at the root of the project.

---

## Use the action
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

## Use the composite workflow

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
