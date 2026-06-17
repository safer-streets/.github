# [Safer Streets](http://safer-streets.github.io)

## Getting started

1. Create a folder to contain all the repos (e.g. `safer-streets`). In that folder clone the repos you require, e.g.

    ```sh
    git clone git@github.com:safer-streets/safer-streets-core  # required, even if not using directly
    git clone git@github.com:safer-streets/safer-streets-tooling  # required for ETL data pipeline
    git clone git@github.com:safer-streets/safer-streets-eda
    # other repos as necessary, e.g. safer-streets-apps...
    ```
    Refer to the `README` in each repo for specific instructions.

1. In the top-level folder create a `.env` file containing definitions for `SAFER_STREETS_DATA_DIR` (where you intend to cache
data - absolute path recommended) `SAFER_STREETS_API_URL`, `SAFER_STREETS_API_KEY` and `NOMIS_API_KEY` (if you will be
downloading census data). Also if necessary put other credentials in here, e.g. Azure, Github, Gemini.

1. In each repo you'll be using, create a [uv](https://docs.astral.sh/uv/) env.:

    ```sh
    uv sync --dev
    ```

    NB `safer-streets-core` is installed as an editable dependency of `safer-streets-eda`, `safer-streets-tooling` and `safer-streets-apps` - this way
    any changes you make to the core package are immediately visible to the dependent packages.

1. Create the datasets and database locally - this requires using the `data` tool in `safer-streets-tooling`. Whilst most raw datasets are downloaded automatically, in some cases the dataset requires a login for access so must be downloaded manually. Full instructions are in the [README](https://github.com/safer-streets/safer-streets-tooling/blob/main/README.md)
