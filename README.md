# Recce Demo Monorepo

A demonstration monorepo containing multiple dbt projects for showcasing [Recce Cloud](https://cloud.datarecce.io/) monorepo support.

## Repository Structure

```
recce-demo-monorepo/
├── jaffle_shop_snowflake/    # Snowflake-based dbt project
├── jaffle_shop_bigquery/     # BigQuery-based dbt project
└── README.md
```

## Projects

| Project | Data Warehouse | Description |
|---------|----------------|-------------|
| `jaffle_shop_snowflake` | Snowflake | Jaffle Shop demo project configured for Snowflake |
| `jaffle_shop_bigquery` | BigQuery | Jaffle Shop demo project configured for BigQuery |

## Prerequisites

- Python 3.9+
- dbt-core 1.5.0+
- Appropriate dbt adapter (`dbt-snowflake` or `dbt-bigquery`)

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/DataRecce/recce-demo-monorepo.git
cd recce-demo-monorepo
```

### 2. Configure Your Profile

Each project expects a profile named `default` in your `~/.dbt/profiles.yml`. Configure the appropriate profile for your data warehouse:

**For Snowflake (`jaffle_shop_snowflake`):**
```yaml
default:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: <your-account>
      user: <your-user>
      password: <your-password>
      role: <your-role>
      database: <your-database>
      warehouse: <your-warehouse>
      schema: jaffle_shop_snowflake
      threads: 4
```

**For BigQuery (`jaffle_shop_bigquery`):**
```yaml
default:
  target: dev
  outputs:
    dev:
      type: bigquery
      method: oauth
      project: <your-gcp-project>
      dataset: jaffle_shop_bigquery
      threads: 4
```

### 3. Install Dependencies

Navigate to the project you want to work with and install dependencies:

```bash
cd jaffle_shop_snowflake  # or jaffle_shop_bigquery
pip install -r requirements.txt
dbt deps
```

### 4. Run dbt

```bash
dbt seed    # Load seed data
dbt run     # Run models
dbt test    # Run tests
```

## Recce Cloud Monorepo Configuration

To onboard this monorepo to Recce Cloud:

1. Connect your repository to Recce Cloud
2. Configure each dbt project path in the Recce Cloud settings
3. Set up the appropriate warehouse credentials for each project

For detailed instructions, see the [Recce Cloud Monorepo Documentation](https://datarecce.io/docs/monorepo).

## Related Resources

- [Recce Cloud](https://cloud.datarecce.io/)
- [Recce Documentation](https://datarecce.io/docs)
- [dbt Documentation](https://docs.getdbt.com/)
- [Original Jaffle Shop](https://github.com/dbt-labs/jaffle-shop)

## License

This project is based on the [Jaffle Shop](https://github.com/dbt-labs/jaffle-shop) by dbt Labs, licensed under the Apache License 2.0.
