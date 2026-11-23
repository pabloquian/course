# Airbnb Analytics Pipeline with dbt and Snowflake
 
An analytics engineering project that turns raw Airbnb data into clean, tested and documented tables, ready for analysis and dashboards. Built with **dbt** on **Snowflake**.
 
> 🚧 **Work in progress.** I'm building this while following the [Complete dbt Bootcamp (Zero to Hero)](https://www.udemy.com/course/complete-dbt-data-build-tool-bootcamp-zero-to-hero-learn-dbt/) on Udemy. See [Progress](#progress) for what's done so far.
 
## What it does
 
Raw Airbnb data for Berlin (listings, hosts and reviews) is loaded into Snowflake. dbt then transforms it in layers:
 
- **Staging:** renames and cleans the raw columns, so every later model works with consistent names and types.
- **Core:** builds dimension and fact tables, such as cleansed listings and hosts, and an incremental reviews table that only processes new data on each run.
- **Marts:** combines core tables into business-ready tables for analysis and dashboards.
Every layer is covered by data tests, and the project generates its own documentation with a lineage graph showing how each table is built.
 
<!-- I will add a screenshot of the lineage graph once I have it -->
 
## Tech stack
 
- **dbt Core:** transformations, tests, snapshots, macros and documentation
- **Snowflake:** cloud data warehouse
- **SQL and Jinja:** model logic and reusable macros
- **Python with uv:** environment and dependency management
- **Git and GitHub:** version control
## Project structure
 
```
.
├── airbnb/                 # The dbt project
│   ├── models/             # SQL models (staging → core → marts)
│   ├── tests/              # Custom data tests
│   ├── macros/             # Reusable Jinja/SQL macros
│   ├── snapshots/          # Change tracking (SCD Type 2)
│   ├── seeds/              # Small reference datasets loaded from CSV
│   └── dbt_project.yml     # Project configuration
├── pyproject.toml          # Python dependencies
└── uv.lock
```
 
## Progress
 
- [x] Snowflake account and warehouse setup, with key-pair authentication for dbt
- [x] dbt project setup and connection to Snowflake
- [ ] Staging models
- [ ] Core dimension and fact models, including incremental models
- [ ] Snapshots (slowly changing dimensions)
- [ ] Data tests: generic, singular and dbt-expectations
- [ ] Macros and Jinja
- [ ] Documentation and lineage graph
- [ ] Dashboard
- [ ] Production setup
## How to run it
 
1. Clone the repo and install the dependencies with [uv](https://docs.astral.sh/uv/):
```bash
uv sync
```
2. Add your own `profiles.yml` with your Snowflake connection details to the `airbnb/` folder. It's listed in `.gitignore`, so credentials are never committed.
3. From the `airbnb/` folder, check the connection and build the project:
```bash
dbt debug
dbt build
```
 
The repo also includes a dev container configuration, so it can run in GitHub Codespaces without any local setup.
 
## About me

I'm Pablo Iglesias Quián, a Data / BI Analyst at [WebBeds](https://www.webbeds.com), a B2B travel technology company. In my day-to-day work I turn data into reports and insights for the business, and I build automations with Python, Power Automate and Power Apps.

I'm now growing towards **analytics engineering**: modeling data, testing its quality, and building the pipelines that make reporting reliable.

[LinkedIn](https://www.linkedin.com/in/pabloiglesiasquian/)
 
---
 
*Starting point: the student repository from [Zoltan C. Toth's](https://github.com/zoltanctoth/complete-dbt-bootcamp-zero-to-hero) Complete dbt Bootcamp.*
