# Awesome-Open-Table-Format-Apache-Iceberg-Lakehouse

# Top Open Table Format & Apache Iceberg Lakehouse Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Open Table Standards, REST Catalogs & Self-Hosted Lakehouse Infrastructure*  
**Last updated: November 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Open Table Formats & Apache Iceberg Lakehouses**. These tools enable organizations to build vendor-neutral data lakes where multiple compute engines—Spark, Trino, Flink, Snowflake, BigQuery—can safely read and write the same tables concurrently, breaking the lock-in of proprietary warehouse formats.

**Examples** include Snowflake Apache Iceberg Integration, Tabular (Databricks), Dremio Arctic, Starburst Galaxy, AWS Glue Iceberg, Onehouse, Google BigLake Iceberg, CelerData, Cloudera Iceberg, and Upsolver (the category leaders).

**Open-source emphasis**: Open Table Format is a domain where open-source tooling is **foundational and rapidly maturing**. **Apache Iceberg** is the open standard itself—a table format that brings SQL-table reliability to big data, with multi-engine support for Spark, Flink, Hive, Trino, Presto, and Impala . The **Iceberg 1.11.0 release** (May 2026) added Spark 4.1 and Flink 2.1 support, server-side scan planning for REST catalogs, built-in table encryption with Google KMS, and a pluggable File Format API that opens the door to new formats like Vortex . For catalogs, **Apache Polaris** is the vendor-neutral open-source implementation of the Iceberg REST Catalog spec—graduated as an Apache TLP in February 2026 with contributions from Dremio and Snowflake . **Apache Gravitino** provides a federated metadata lake with native Iceberg REST catalog services, geo-distribution, and multi-engine compatibility . The critical caveat: **managed platforms differentiate on operational simplicity and integrated governance**—AWS Glue, Google BigLake, and Snowflake's Iceberg integration handle catalog management, security, and scaling, while open-source requires you to operate Polaris/Gravitino and the compute engines yourself.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Snowflake Apache Iceberg Integration](https://www.snowflake.com/)**  
  Snowflake's native support for reading and writing Apache Iceberg tables; enables external engines to access Snowflake-managed Iceberg data while Snowflake retains governance and performance optimizations.

- **[Tabular (Databricks)](https://www.tabular.io/)**  
  Managed Iceberg catalog and lakehouse platform (acquired by Databricks); provides REST catalog services, table management, and optimization for Iceberg workloads.

- **[Dremio Arctic](https://www.dremio.com/)**  
  Managed lakehouse catalog built on Apache Polaris (Dremio is a primary contributor to Polaris); provides a REST Iceberg catalog with governance and optimization features.

- **[Starburst Galaxy](https://www.starburst.io/)**  
  Managed Trino platform with Iceberg catalog support; enables federated queries across Iceberg tables and other data sources without data movement.

- **[AWS Glue Iceberg](https://aws.amazon.com/glue/)**  
  AWS Glue Data Catalog with native Iceberg table support; provides a managed REST catalog for Iceberg tables stored in S3, integrated with Athena, EMR, and Redshift Spectrum.

- **[Onehouse](https://www.onehouse.ai/)**  
  Managed lakehouse platform built on Apache Hudi (not Iceberg); provides automated data lake management and optimization.

- **[Google BigLake Iceberg](https://cloud.google.com/biglake)**  
  Google Cloud's managed lakehouse service with Iceberg support; provides a unified metadata layer across BigQuery and open formats.

- **[CelerData](https://celerdata.com/)**  
  Enterprise analytics platform built on StarRocks; provides high-performance query acceleration over Iceberg and other open formats.

- **[Cloudera Iceberg](https://www.cloudera.com/)**  
  Enterprise data platform with Iceberg support within Cloudera Data Platform; provides managed Iceberg tables with governance and security.

- **[Upsolver](https://www.upsolver.com/)**  
  Data lake platform with Iceberg table management; focuses on streaming ingestion and automated table optimization.

## Open-Source GitHub Projects

### The Open Table Format (Apache Iceberg)

- **[Apache Iceberg](https://github.com/apache/iceberg)**  
  The **open standard for huge analytic tables** (Apache 2.0) . Brings SQL-table reliability to data lakes with schema evolution, hidden partitioning, time travel, and ACID transactions. **Multi-engine support**: connectors for Spark, Flink, and Hive are maintained in the main repository; Trino, Presto, Impala, and others have separate integrations . **Iceberg 1.11.0** (May 2026) added Spark 4.1 and Flink 2.1 as default build targets, server-side scan planning for REST catalogs, built-in table encryption with envelope encryption and Google KMS support, and a **File Format API** that makes file formats pluggable (enabling future integration of Vortex, Lance, and other formats) . **Language implementations**: Rust (iceberg-rust 0.9.0), Go (iceberg-go 0.5.0), Python (PyIceberg 0.11.0), and C++ (0.2.0) are actively developed . **Best for organizations wanting a vendor-neutral table format** with the broadest engine ecosystem—but it is a format specification and library, not a managed service.

### REST Catalogs (Vendor-Neutral)

- **[Apache Polaris](https://github.com/apache/polaris)**  
  The **vendor-neutral implementation of the Iceberg REST Catalog spec** (Apache 2.0) . Graduated as an Apache TLP in February 2026 with contributions from Dremio and Snowflake—two competing companies collaborating under Apache governance. Provides a standard REST API for Iceberg catalog operations, enabling any compatible engine to access tables without proprietary catalog lock-in. **Best for organizations wanting a neutral, open catalog** that avoids vendor-specific metadata services—but it is a catalog only, not a full lakehouse platform.

- **[Apache Gravitino](https://github.com/apache/gravitino)**  
  High-performance, **geo-distributed, federated metadata lake** (Apache 2.0) . Manages metadata across Hive, MySQL, MariaDB, HDFS, S3, and other sources through a unified model and API. Features: **native Iceberg REST catalog service**, Lance REST catalog service, Trino connector for federated access, access control, auditing, and discovery across metadata assets. Supports multi-region metadata synchronization for hybrid/multi-cloud setups. **Best for organizations with heterogeneous data sources** wanting unified metadata access across lakes and warehouses—but it is a metadata layer, not a compute engine.

### Iceberg-Native Transformation (Data Branching)

- **[Reble](https://pypi.org/project/reble/0.6.1/)**  
  Open-source **transformation engine with Iceberg-native data branching** (pip-installable) . Works with any Iceberg catalog (Glue, Polaris, Nessie, Hive, any REST-compliant catalog)—**no new infrastructure required**. Models are plain SQL files; lineage is parsed with SQLGlot. **Branch creation is metadata-only** (< 10 ms for a 5M-row table); upstream inputs are pinned via Iceberg tags; row-level diffs are computed via DuckDB streaming. **Promote semantics**: fast-forward only when pinned bases still equal main; otherwise scoped re-run with fresh diff. **No three-way merge**—a change is either fast-forwarded or re-run. Measured lifecycle on AWS (Glue + S3, 1M rows): scoped run ~13s, diff ~4s, drift check ~2s . **Best for data teams wanting Git-like branching for Iceberg tables** without a new catalog or server—but it is a CLI/engine, not a full orchestration platform.

### Additional Strong Open-Source Options

- **Apache Spark + Iceberg Runtime** — The most common compute engine for Iceberg workloads; use the `iceberg-spark-runtime` jar for the appropriate Spark version (e.g., Spark 3.5 or 4.0) . **Best for batch and streaming workloads** over Iceberg tables—but Spark is a general-purpose engine, not a lakehouse platform.
- **Trino + Iceberg Connector** — High-performance SQL query engine with native Iceberg connector; enables federated queries across Iceberg and other sources. **Best for interactive analytics** over Iceberg lakes—but requires operating Trino clusters.
- **Nessie** — Open-source transactional catalog for Iceberg with Git-like branching and versioning; an alternative to Polaris for teams wanting data versioning capabilities. **Verify current project status** and compatibility with Iceberg 1.11.

**Frameworks for building custom systems**: For the **open table format itself**, Apache Iceberg provides the foundation with the broadest engine ecosystem and active multi-language development . For a **vendor-neutral REST catalog**, Apache Polaris is the standard open-source implementation . For **federated metadata across heterogeneous sources**, Apache Gravitino . For **data branching without new infrastructure**, Reble . **Managed platforms differentiate on operational simplicity**—AWS Glue, Google BigLake, and Snowflake's integration handle catalog management and scaling, while open-source requires you to operate Polaris/Gravitino and compute engines yourself.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Open table format and lakehouse platforms handling production data must comply with organizational security policies and data governance requirements; **Iceberg's table encryption (1.11.0+) provides fine-grained KMS-backed security**—verify configuration before storing sensitive data .
- **Open-source Iceberg lakehouse is mature at the format and catalog layers but requires operational investment**—Apache Iceberg provides the table format , Polaris provides the REST catalog , and Gravitino provides federated metadata . However, **managed platforms differentiate on operational simplicity**—AWS Glue, Google BigLake, and Snowflake handle catalog management, security, and scaling. Choose based on whether your team has the engineering capacity to operate open-source infrastructure or needs managed convenience.
- Verify license terms for commercial use; Apache Iceberg, Polaris, and Gravitino all use Apache 2.0 . Reble is open-source (check repository) .

---

**Made for data platform engineers, lakehouse architects, and organizations building vendor-neutral data infrastructure.**  
Let's make the Iceberg lakehouse more open, but with clear eyes about the operational responsibility that self-hosting a catalog and compute stack requires.
