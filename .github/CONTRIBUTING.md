See the [Scientific Python Developer Guide][spc-dev-intro] for a detailed
description of best practices for developing scientific packages.

[spc-dev-intro]: https://scientific-python-cookie.readthedocs.io/en/stable/

# Quick development

The fastest way to start with development is to use `nox`. This will set up a
virtual environment for you to run all the checks and tests. There are 2 ways to
install `nox`:

## Codespaces

Nox is pre-installed in the Codespaces environment. So, after activating a
Codespace, you can just open the terminal and run `nox` to run all the checks
and tests.

## Local

If you don't have nox, you can do the following to install `nox`:

```bash
pip install nox
```

If you use macOS, then `nox` is in brew:

```bash
brew install nox
```

## Nox basics

### What is it?

`nox` is a command-line tool that automates testing in multiple Python
environments, similar to tox. Unlike tox, Nox uses a standard Python file for
configuration, you can find this configuration in [`noxfile.py`](../noxfile.py).

### How do I use it?

To use, run `nox`. This will lint and test using every installed version of
Python on your system, skipping ones that are not installed. You can also run
specific jobs:

```bash
nox -s lint  # Lint only
nox -s tests  # Python tests
nox -s build  # Make an SDist and wheel
```

Nox handles everything for you, including setting up a temporary virtual
environment for each run.

# Setting up a development environment manually

You can set up a development environment by running:

```bash
python3 -m venv .venv
source ./.venv/bin/activate
pip install -v -e .[dev]
```

If you have the
[Python Launcher for Unix](https://github.com/brettcannon/python-launcher), you
can instead do:

```bash
py -m venv .venv
py -m install -v -e .[dev]
```

# Post setup

You should prepare pre-commit, which will help you by checking that commits pass
required checks:

```bash
pip install pre-commit # or brew install pre-commit on macOS
pre-commit install # Will install a pre-commit hook into the git repo
```

You can also/alternatively run `pre-commit run` (changes only) or
`pre-commit run --all-files` to check even without installing the hook.

# Testing

Use pytest to run the unit checks:

```bash
pytest
```

# Coverage

Use pytest-cov to generate coverage reports:

```bash
pytest --cov=caustics
```

# Pre-commit

This project uses pre-commit for all style checking. While you can run it with
nox, this is such an important tool that it deserves to be installed on its own.
Install pre-commit and run:

```bash
pre-commit run -a
```

to check all files.
