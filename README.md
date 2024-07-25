# Cookie Cutter for HDX Python Scrapers

### Usage

Make sure you have the `cookiecutter` package installed.

Navigate to the directory where you want to create the scraper, then execute:

    cookiecutter path/to/hdx-scraper-cutter

Fill in the values as prompted. Cookiecutter will use these values to generate
the project files and directories.

## Development

### Pre-commit

Be sure to install `pre-commit`, which is run every time
you make a git commit:

```shell
pip install pre-commit
pre-commit install
```

The configuration file for this project is in a
non-start location. Thus, you will need to edit your
`.git/hooks/pre-commit` file to reflect this. Change
the first line that begins with `ARGS` to:

    ARGS=(hook-impl --config=.config/pre-commit-config.yaml --hook-type=pre-commit)

With pre-commit, all code is formatted according to
[black]("https://github.com/psf/black") and
[ruff]("https://github.com/charliermarsh/ruff") guidelines.

To check if your changes pass pre-commit without committing, run:

    pre-commit run --all-files --config=.config/pre-commit-config.yaml

## Packages

[pip-tools](https://github.com/jazzband/pip-tools) is used for
package management.  If you’ve introduced a new package to the
source code please add it to the `dependencies` section of
`pyproject.toml` with any known version constraints.

For adding packages for testing, add them to
the `test` sections under `[project.optional-dependencies]`.

Any changes to the dependencies will be automatically reflected in
`requirements.txt` and `requirements-test.txt` with `pre-commit`,
but you can re-generate the file without committing by executing:

    pre-commit run pip-compile --all-files --config=.config/pre-commit-config.yaml
