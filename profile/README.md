# [Safer Streets](http://safer-streets.github.io)

## Getting started

1. Create a folder to contain all the repos (e.g. `safer-streets`)

2. In that folder create a `.env` file containing definitions for `SAFER_STREETS_DATA_DIR` (where you intend to cache data - absolute path recommended) and `NOMIS_API_KEY` (if you will be downloading census data)

3. Create a python venv. [uv](https://docs.astral.sh/uv/) is highly recommended for managing the environment, e.g.:

    ```sh
    uv venv --python 3.12
    ```

1. Install `safer-streets-core`, either:

    ```sh
    uv pip install "git+https://github.com/safer-streets/safer-streets-core"
    ```

    if you don't want a cloned copy, or clone it and then install the local version:

    ```sh
    uv pip install . --dev
    ```

1. Clone the EDA repo:

    ```sh
    git clone git@github.com/safer-streets/safer-streets-eda
    ```

1. Install extra dependencies required by the EDA notebooks

    ```sh
    uv pip install -r safer-streets-eda/requirements.txt
    ```

1.  Manually install geospatial datasets...




