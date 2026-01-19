# Recce Demo Monorepo

A demonstration monorepo containing multiple dbt projects for showcasing [Recce Cloud](https://cloud.datarecce.io/) monorepo support.

## Projects

| Project | Data Warehouse | Path |
|---------|----------------|------|
| Jaffle Shop Snowflake | Snowflake | `jaffle_shop_snowflake/` |
| Jaffle Shop BigQuery | BigQuery | `jaffle_shop_bigquery/` |

## Prerequisites

- [uv](https://docs.astral.sh/uv/) (Python package manager)
- Python 3.12+
- Access to Snowflake or BigQuery

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/DataRecce/recce-demo-monorepo.git
cd recce-demo-monorepo
```

### 2. Set Up Environment Variables

Each project includes a `profiles.yml` that references environment variables. Set them up before running dbt.

<details>
<summary><b>Snowflake Environment Variables</b></summary>

```bash
export SNOWFLAKE_ACCOUNT="your-account"
export SNOWFLAKE_USER="your-user"
export SNOWFLAKE_PEM_FILEPATH="/path/to/your/key.pem"
export SNOWFLAKE_PEM_PASSPHRASE="your-passphrase"
export SNOWFLAKE_SCHEMA="your-schema"  # optional, defaults to GITLAB_JAFFLE_SHOP_DEV
```
</details>

<details>
<summary><b>BigQuery Environment Variables</b></summary>

```bash
export BQ_PROJECT="your-gcp-project"
export BQ_DATASET="your-dataset"
export BQ_KEYFILE_PATH="/path/to/your/service-account.json"
```
</details>

### 3. Set Up and Run a Project

```bash
# Go to a project directory
cd jaffle_shop_snowflake  # or jaffle_shop_bigquery

# Create virtual environment
uv venv --python 3.12

# Install Python dependencies
uv pip install -r requirements.txt

# Install dbt packages
uv run dbt deps

# Load seed data and build models
uv run dbt seed --full-refresh --vars '{"load_source_data": true}'
uv run dbt build
```

## Recce Cloud Integration

To onboard this monorepo to Recce Cloud:

1. Connect your repository to Recce Cloud
2. Configure each dbt project path in settings
3. Set up warehouse credentials for each project

For detailed instructions, see the [Recce Cloud Documentation](https://datarecce.io/docs).

## Resources

- [Recce Cloud](https://cloud.datarecce.io/)
- [Recce Documentation](https://datarecce.io/docs)
- [dbt Documentation](https://docs.getdbt.com/)
- [uv Documentation](https://docs.astral.sh/uv/)
- [Original Jaffle Shop](https://github.com/dbt-labs/jaffle-shop)

## License

Based on [Jaffle Shop](https://github.com/dbt-labs/jaffle-shop) by dbt Labs, licensed under Apache License 2.0.
