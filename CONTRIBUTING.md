# Contributors

# Reporting issues
* Describe (in detail) what should have happened. Include any supporting information (stack traces, errors, etc)
* Include any steps to replicate the issue
* Indicate OS and Python versions

# Development environment setup
1. Clone repository:
```
git clone https://github.com/mitre/caldera.git --recursive
```

2. Install [uv](https://docs.astral.sh/uv/getting-started/installation/):
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```

3. Create the virtualenv (`.venv`) and install all dependencies, including development tools, exactly as pinned in `uv.lock`:
```
uv sync
```

4. Install the pre-commit hooks:
```
uv run pre-commit install --install-hooks
```

## Managing dependencies
Dependencies are declared in `pyproject.toml` and locked in `uv.lock`. Do not edit `uv.lock` by hand; commit both files together.
```
uv add <package>==<version>          # add a runtime dependency
uv add --dev <package>               # add a development dependency
uv lock --upgrade-package <package>  # upgrade a single package
```

# Developing
We use the basic feature branch GIT flow. Fork this repository and create a feature branch off of master and when ready, submit a merge request. Make branch names and commits descriptive. A merge request should solve one problem, not many.

* Tests should cover any code changes that you have made. The test that you write should fail without your patch.
* [Run tests](#run-the-tests)

# Run the tests
Tests can be run by executing:
```
uv run pytest
```
This will run all unit tests in your current development environment. Depending on the level of the change, you might need to run the test suite on various versions of Python. The unit testing pipeline will run the entire suite across multiple Python versions that we support when you submit your PR.

We utilize `tox` (with the `tox-uv` plugin) to test Caldera in multiple versions of Python. uv will download any missing Python interpreter. To run tox, execute:
```
uvx --with tox-uv tox
```

# Code Coverage
You can generate code coverage reports manually or by running `tox`. To run them manually, run the following commands:
```
uv run coverage run -m pytest
uv run coverage report
uv run coverage html
```
You can find the code coverage report in `htmlcov/index.html`