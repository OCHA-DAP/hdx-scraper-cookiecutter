# Cookie Cutter for HDX Python Scrapers

## Usage

Make sure you have the `cookiecutter` package installed.

Navigate to the directory where you want to create the scraper, then execute:

    cookiecutter path/to/hdx-scraper-cookiecutter

Fill in the values as prompted. Cookiecutter will use these values to generate
the project files and directories.

### Values

Some fields have restricted values, here is how to obtain them:

* `license_id`: choose from the license class `id` values in
  [HDX-CKAN](https://github.com/OCHA-DAP/hdx-ckan/blob/dev/ckanext-hdx_package/ckanext/hdx_package/helpers/licenses.py)
* `methodology`: select from the methodology list in
  [HDX-CKAN](https://github.com/OCHA-DAP/hdx-ckan/blob/dev/ckanext-hdx_theme/ckanext/hdx_theme/helpers/helpers.py#L664)
* `dataset_expected_update_frequency`: should be a numeric value from one of
  the keys in the `UPDATE_FREQ_INFO` ordered dict in
  [HDX-CKAN](https://github.com/OCHA-DAP/hdx-ckan/blob/dev/ckanext-hdx_package/ckanext/hdx_package/helpers/freshness_calculator.py#L12)
* `private`: either "True" or "False"
* `dataset_maintainer`: the user ID, which you can obtain by querying the HDX
  API with the username: `https://data.humdata.org/api/action/user_show?id={username}`
  and selecting the `id` field
* `dataset_organization`: the organization ID, which you can obtain by finding
  the organization you require from
  [this search page](https://data.humdata.org/organization), then querying
  the HDX API using the slug from the organization page:
  `https://data.humdata.org/api/action/organization_show?id={organization-slug}`

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
source code please add it to `requirements.in`
with any known version constraints.

Any changes to the dependencies will be automatically reflected in
`requirements.txt` with `pre-commit`,
but you can re-generate the file without committing by executing:

    pre-commit run pip-compile --all-files --config=.config/pre-commit-config.yaml
