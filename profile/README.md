# [Safer Streets](http://safer-streets.github.io)

## Getting started

1. Create a folder to contain all the repos (e.g. `safer-streets`)

2. In that folder create a `.env` file containing definitions for `SAFER_STREETS_DATA_DIR` (where you intend to cache data - absolute path recommended) and `NOMIS_API_KEY` (if you will be downloading census data)

3. Create and activate a python venv. [uv](https://docs.astral.sh/uv/) is highly recommended for managing the environment, e.g.:

    ```sh
    uv venv --python 3.13
    . .venv/bin/activate
    ```

    NB using `uv sync` to manage dependencies is not recommended (by default it will uninstall anything that isn't a
    direct dependency, unless you pass the `--inexact` flag)

1. Clone and install `safer-streets-core`. This will include the basic dependencies and some useful scripts (see below):

    ```sh
    git clone git@github.com:safer-streets/safer-streets-core
    cd safer-streets-core
    uv pip install -e . --group dev
    cd ..
    ```

1. Clone the EDA repo:

    ```sh
    git clone git@github.com:safer-streets/safer-streets-eda
    ```

1. Install extra dependencies required by the EDA notebooks.

    ```sh
    cd safer-streets-eda
    uv pip install -e . --group dev
    cd ..
    ```

1. (Optional) clone the apps repo and install it's dependencies

    ```
    git clone git@github.com:safer-streets/safer-streets-apps
    cd safer-streets-apps
    uv pip install -e . --group dev
    cd ..
    ```

1.  Download and extract the last 3 years of public crime data:

    ```
    extract latest
    ```

1.  Manually install geospatial datasets...


NB Documentation is developed within a separate environment - see the README at the
[blog/project site](https://github.com/safer-streets/safer-streets-eda)


