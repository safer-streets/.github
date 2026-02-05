# [Safer Streets](http://safer-streets.github.io)

## Getting started

1. Create a folder to contain all the repos (e.g. `safer-streets`). In that folder clone the repos you require, e.g.

    ```sh
    git clone git@github.com:safer-streets/safer-streets-core
    git clone git@github.com:safer-streets/safer-streets-eda
    # other repos as necessary...
    ```


1. In that folder create a `.env` file containing definitions for `SAFER_STREETS_DATA_DIR` (where you intend to cache
data - absolute path recommended) `SAFER_STREETS_API_URL`, `SAFER_STREETS_API_KEY` and `NOMIS_API_KEY` (if you will be
downloading census data). Also if necessary put other credentials in here, e.g. Azure, Github, Gemini.

1. In each repo create an [uv](https://docs.astral.sh/uv/) env.:

    ```sh
    uv sync --dev
    ```

    NB `safer-streets-core` is installed as an editable dependency of both `safer-streets-eda` and `safer-streets-apps` so
    that changes you make to the core package are immediately visible to the dependent packages.

1.  Download and extract the last 3 years of public crime data (this can be done from core, eda or apps):

    ```
    uv run extract latest
    ```

    Repeat this when new data is released (normally mid-monthly).

1.  Manually install geospatial datasets. Easiest option is to take a copy all the top-level files from our [Azure blob
storage](https://portal.azure.com/?l=en.en-gb#view/Microsoft_Azure_Storage/ContainerMenuBlade/~/overview/storageAccountId/%2Fsubscriptions%2F118c6c89-fae8-4343-9942-cca5541cb536%2FresourceGroups%2Fuol-a011-prd-uks-wkld025-rg%2Fproviders%2FMicrosoft.Storage%2FstorageAccounts%2Fsaferstreets/path/safer-streets-data/etag/%220x8DE00EE2AF0D870%22/defaultId//publicAccessVal/None)

1. Refer to the `README` in each repo for specific instructions.