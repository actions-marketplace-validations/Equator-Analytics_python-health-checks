# python-health-checks

This is a github action that you can use to set up a [pipenv based](https://pipenv.pypa.io/en/latest/index.html) python health check.

You can use it as follows in a `.github/workflows` `*.yml` file -

## Prequisites
You will need to set up the following commands in your `Pipfile`.
* `lint`
* `style-check`
* `type-check`
* `test`

### Prequisite tools we recommend
You can set up the pipenv scripts however you wish. We use the following -
```
lint = "flake8 <YOUR_SRC_DIRECTORIES>"
style-check = "black -l 88 <YOUR_SRC_DIRECTORIES> --check"
type-check = "mypy <YOUR_SRC_DIRECTORIES>"
test = "pytest"
```

see: [flake8](https://flake8.pycqa.org/en/latest/), [black](https://github.com/psf/black), [mypy](https://www.mypy-lang.org/), and [pytest](https://docs.pytest.org/)

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
        uses: Equator-Analytics/python-health-checks@v2.1.1
```

If special testing setup is required you can override the testing step as follows
```yml
...

jobs:
  your_job:
    steps:
      - name: 'set up python and run health checks'
        uses: Equator-Analytics/python-health-checks@v2.1.1
        with:
          checktests: false
```