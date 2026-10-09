# Safer Streets @ Leeds

> **Not a developer?** Head to **[safer-streets.github.io](https://safer-streets.github.io)** for articles, research
> write-ups, interactive notebooks and the [Crime Capture Explorer](https://safer-streets.github.io/explorer/app/) app.
> This GitHub organisation holds the code behind them.

Open-data spatial analysis of crime in England & Wales. We combine [police.uk](https://data.police.uk) crime records
with ONS boundaries, census and other open geographic data (roads, buildings, land cover, amenities, transport), and
aggregate them onto equal-area spatial units — [H3](https://h3geo.org) and our own British National Grid hexagonal
index, [BEAHIV](https://github.com/safer-streets/beahiv) — to study hotspots, their stability and what characterises
them.

**Stack:** Python ≥ 3.13 · [uv](https://docs.astral.sh/uv/) · [DuckDB](https://duckdb.org) (spatial) · GeoParquet ·
Azure Blob Storage · Jupyter / [marimo](https://marimo.io) · Streamlit · [Zensical](https://zensical.org) for the site

## Public Repositories

| Repo | What it is |
| ---- | ---------- |
| [safer-streets-core](https://github.com/safer-streets/safer-streets-core) | Core library: statistical and geospatial primitives, config, storage access. Required by everything else. |
| [safer-streets-tooling](https://github.com/safer-streets/safer-streets-tooling) | The `data` CLI: extract → transform pipeline that builds the GeoParquet datasets and syncs them to Azure. |
| [beahiv](https://github.com/safer-streets/beahiv) | **B**ritish National Grid **E**qual-**A**rea **H**exagonal **I**ndex that's **V**ersatile — a fast, EPSG:27700-native alternative to H3. |
| [exploratory-data-analysis](https://github.com/safer-streets/exploratory-data-analysis) | Polished, runnable notebooks (also published on the site). |
| [peer-hex-explorer](https://github.com/safer-streets/peer-hex-explorer) | Streamlit app for finding the places that most resemble a given crime hotspot. |

## Getting started

1. Create a parent folder (e.g. `safer-streets`) and clone the repos you need into it, side by side:

    ```sh
    git clone git@github.com:safer-streets/safer-streets-core      # always required
    git clone git@github.com:safer-streets/safer-streets-tooling   # data pipeline
    git clone git@github.com:safer-streets/exploratory-data-analysis
    ```

    `safer-streets-core` is installed as an *editable* dependency of the other repos (resolved via the relative path),
    so changes to it are picked up immediately without reinstalling.

1. In the parent folder, create a `.env` file. Settings are read from the environment or the nearest `.env` (which is
   read directly, not exported into the environment), and each is only needed by the code that uses it:

    | Variable | Required? | Used for |
    | -------- | --------- | -------- |
    | `SAFER_STREETS_DATA_DIR` | Yes | Local data cache (absolute path recommended) |
    | `AZURE_STORAGE_CONNSTR` | For cloud data | Read access to the shared datasets |
    | `SAFER_STREETS_BLOB_STORAGE` | For `data sync` | Azure Blob storage account URL |
    | `AZURE_TENANT_ID` / `AZURE_CLIENT_ID` / `AZURE_CLIENT_SECRET` | For `data sync` | Azure service principal used to write to blob storage |
    | `NOMIS_API_KEY` | Optional | Downloading census data from [Nomis](https://www.nomisweb.co.uk) |
    | `CARTO_API_KEY` | Optional | [Carto](https://carto.com) map tiles |

    Other credentials (GitHub, LLM APIs etc.) can go here too. See the
    [core README](https://github.com/safer-streets/safer-streets-core#setup) for the full list.

1. In each repo, create the environment:

    ```sh
    uv sync --dev
    ```

1. Get the data. The preferred route is to query the prebuilt (Geo)Parquet directly from blob storage with an in-memory
    DuckDB - this has little or no overhead over local storage and needs only `AZURE_STORAGE_CONNSTR` - nothing is
    downloaded up front.

    Data supplied in confidence never goes to the cloud, so to work with it you must store it locally. If you want to
    work with *all* the data locally:

    ```sh
    cd safer-streets-tooling
    uv run data sync --update newer
    ```

    If you intend to change or extend the data extracts or transforms, see the
    [tooling README](https://github.com/safer-streets/safer-streets-tooling#usage) for further details.

Each repo's own `README` covers anything specific to it.

## Contributing

Issues and pull requests are welcome. Notebooks intended for an outside audience belong in
[exploratory-data-analysis](https://github.com/safer-streets/exploratory-data-analysis) and should be documented and
runnable by third parties (subject to data access).
