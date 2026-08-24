# CloudStream Resource Aggregator

CloudStream Resource Aggregator is a high-performance, open-source metadata and resource indexing platform designed for developers building media discovery applications, content aggregation services, and language-localized streaming tools. It targets technical users who require programmatic access to structured resource entries, including subtitle mappings, streaming endpoints, and localization data. The project solves the fragmentation problem of scattered multimedia references by providing a unified, queryable index with predictable schemas and stable API responses.

Unlike traditional bookmark collections or manual link directories, CloudStream Aggregator treats external references as first-class data entities. It validates accessibility, extracts metadata headers, and enriches entries with response time, content type hints, and regional availability flags. The system is built for extensibility, allowing contributors to append new source entries through a standardized pull request workflow. The core philosophy emphasizes reliability over quantity, ensuring every listed endpoint is continuously verified through an integrated health-check daemon.

## 功能概览

- **Structured Metadata Indexing** – Parses and stores domain-level attributes including SSL status, HTTP response codes, and server fingerprinting for each registered resource endpoint.

- **Automated Health Verification** – Runs a lightweight background scheduler that probes all indexed URLs at configurable intervals (default 300 seconds), marking unhealthy entries and logging degradation patterns.

- **RESTful Query API** – Exposes read-only JSON endpoints for filtering resources by category, status, or last-verified timestamp; supports pagination and field selection to minimize payload size.

- **Localization Tagging** – Assigns language-specific tags (e.g., subtitle language, audio track availability) based on domain pattern analysis and optional user-provided annotations.

- **Batch Import/Export** – Provides CLI utilities for ingesting raw URL lists from CSV or plaintext files and exporting verified entries into JSON Lines format for offline processing.

- **Historical Availability Logging** – Retains up to 7 days of probe history per endpoint, enabling trend analysis and outage visualization through optional Prometheus exporter integration.

- **Access Control Stub** – Includes a pluggable authentication middleware for protecting administrative endpoints, with built-in support for API key verification and IP allowlisting.

## 应用场景

- **Media Application Backend Integration** – Developers building streaming clients or media browsers can embed the aggregator's API to obtain up-to-date subtitle domain references, reducing hardcoded fallback chains and improving user experience during regional content shifts.

- **Localization Quality Assurance Pipelines** – Quality engineers can use the health-check logs to monitor the availability of Chinese-subtitle resources across different geographic zones, automatically flagging endpoints that fail to respond within 800 milliseconds.

- **Research and Data Journalism** – Academics or analysts studying online content distribution patterns can export the aggregated history logs to analyze uptime trends, domain rotation behaviors, and regional blocking events over extended time windows.

- **Educational Tool for Network Programming** – Instructors can utilize the batch import feature to distribute curated resource lists to students, who then practice building custom monitoring dashboards or alerting rules using the exposed metrics.

## 快速开始

Clone the repository, install Python dependencies, and launch the development server using the built-in CLI runner. The following commands assume a Unix-like environment with Python 3.10 or later installed.

```bash
git clone https://github.com/cloudstream-agg/cloudstream-aggregator.git
cd cloudstream-aggregator
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver --host 0.0.0.0 --port 8080
```

For production deployments, replace the development server with Gunicorn or uWSGI. The configuration file `config/production.yaml` contains sample worker and timeout settings. After starting the service, the health-check daemon automatically initializes and begins probing the default resource set within 30 seconds.

## 安装要求

The following table lists mandatory runtime dependencies along with their minimum versions and primary roles within the system. All dependencies are available via the Python Package Index (PyPI) and are resolved automatically when installing from `requirements.txt`. Additional optional packages for Prometheus integration and advanced logging are listed in `requirements-extra.txt`.

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 - 3.12 | Core runtime interpreter; type annotations rely on PEP 604 union syntax |
| SQLite | 3.35.0+ | Embedded database for metadata storage and probe history retention |
| aiohttp | 3.9.0+ | Asynchronous HTTP client for non-blocking health checks |
| pydantic | 2.5.0+ | Data validation and settings management using Python type hints |
| pyyaml | 6.0.0+ | YAML configuration file parser for environment-specific overrides |
| click | 8.1.0+ | CLI argument parser for administrative commands and batch operations |
| prometheus-client | 0.19.0+ | Optional: metrics export for Prometheus scraping (requires extra flag) |
| uvicorn | 0.27.0+ | Optional: ASGI server for high-concurrency production deployments |

## 文档导航

The documentation is organized into four logical layers to accommodate different user roles, from system administrators to frontend integrators. Each layer addresses a distinct set of questions commonly encountered during adoption and maintenance.

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 运维部署 | `docs/deployment/` | How to configure reverse proxies, tune worker processes, set up SSL termination, and manage log rotation |
| API 集成 | `docs/api/` | Which endpoints exist, how to filter results, interpret status fields, and handle rate-limiting responses |
| 数据模型 | `docs/models/` | What fields are stored per resource, how timestamps are formatted, and what status transitions are possible |
| 开发扩展 | `docs/development/` | How to add new resource parsers, write custom validation rules, and contribute test fixtures |

## 资源列表

The following URLs constitute the primary indexed resource set distributed with the default installation. These entries are curated from public sources and are subject to continuous validation. Users are strongly encouraged to review the terms of use for each domain before integration into production systems. All URLs are reproduced exactly as provided by the original data source without modifications to protocol or hostname casing.

**Streaming and Subtitle Domain Index**

<code>yinghuadongmanguanfangbanb.org.cn</code>

<code>zhongwenzimuyongjiuzaixianb.org.cn</code>

<code>mianfeizhuijuwangzhanb.org.cn</code>

<code>gaoqingzhongwenzimub.org.cn</code>

<code>zaixianbofangnidongdeb.org.cn</code>

<code>zhongwenzimuzaixianmianfeikanc.org.cn</code>

<code>zaixianshipinzhongwenzimuc.org.cn</code>

## 项目结构

The source tree follows a modular layout that separates configuration, core logic, storage interfaces, and auxiliary tooling. Each major directory contains an `__init__.py` marker and a `README.md` explaining internal conventions. The structure is designed to facilitate incremental refactoring and parallel feature development.

```
cloudstream-aggregator/
├── config/                                 # Environment configuration files
│   ├── base.yaml                           # Default settings shared across all environments
│   ├── development.yaml                    # Overrides for local development (debug mode on)
│   └── production.yaml                     # Production tunings (worker count, probe intervals)
├── src/
│   ├── core/                               # Core domain models and validation logic
│   │   ├── models.py                       # Pydantic schemas for Resource and ProbeRecord
│   │   └── validators.py                   # Custom URL normalizers and tag sanitizers
│   ├── probe/                              # Health-check engine implementation
│   │   ├── runner.py                       # Asynchronous scheduler with exponential backoff
│   │   └── reporters.py                    # JSON and plaintext log formatters
│   ├── api/                                # RESTful endpoint handlers
│   │   ├── routes.py                       # Route definitions for list, detail, and status views
│   │   └── middlewares.py                  # CORS, logging, and authentication stubs
│   ├── storage/                            # Database abstraction layer
│   │   ├── connection.py                   # SQLite pool manager with retry logic
│   │   └── migrations/                     # Schema versioning scripts (v1 to v4)
│   └── cli/                                # Command-line utilities for admin tasks
│       ├── import_cmd.py                   # CSV/plaintext ingestion entrypoint
│       └── export_cmd.py                   # JSON Lines exporter with field filtering
├── tests/                                  # Unit and integration test suite
│   ├── test_probe.py                       # Mock-based health-check scenarios
│   └── fixtures/                           # Sample URL lists and expected API responses
├── scripts/                                # Helper shell scripts for deployment
│   ├── startup.sh                          # Systemd-compatible start script
│   └── backup.sh                           # Daily database dump with rotation
├── requirements.txt                        # Production dependency pins
├── requirements-dev.txt                    # Linting, formatting, and testing tools
└── README.md                               # This document
```

## 贡献指南

Community contributions are welcomed following a structured process that ensures consistency in code quality, documentation, and resource curation. All submissions are reviewed with attention to backward compatibility and performance implications.

1. **Fork the repository** and create a feature branch from `main` using the naming convention `feature/short-description` or `fix/issue-reference`. Ensure your local environment passes all pre-commit hooks (black, isort, mypy) before pushing.

2. **Add or modify resource entries** by editing the YAML seed files located in `config/seeds/` rather than modifying the database directly. Include a one-line justification for each added URL, referencing public sources or personal testing results.

3. **Write or update tests** in the `tests/` directory covering any new validation logic, API filters, or probe behaviors. Aim for at least 80% line coverage for changed modules.

4. **Update the documentation** – if your changes affect configuration variables, API responses, or installation steps, reflect those changes in the corresponding `.md` files under `docs/`.

5. **Submit a pull request** with a clear title prefixed by `[FEATURE]`, `[FIX]`, or `[DOCS]`. Include a bulleted list of changes and reference any related issues. Pull requests must pass the continuous integration workflow, which runs on GitHub Actions.

## 常见问题

**Q: How frequently does the health-check daemon probe each URL, and can I adjust the interval?**

A: The default probe interval is 300 seconds (5 minutes) for all active entries. You can change this value by setting the `PROBE_INTERVAL_SECONDS` environment variable or modifying the corresponding key in your active YAML configuration. The scheduler respects a minimum interval of 60 seconds to avoid excessive network load. After changing the value, restart the service or send a SIGHUP signal to the main process to reload the settings.

**Q: What happens when an indexed domain becomes unreachable or returns an unexpected status code?**

A: The probe runner updates the resource status to `unhealthy` and increments a failure counter. If the domain remains unreachable for three consecutive probe cycles, the system generates a warning log entry and optionally sends a webhook notification if configured. The resource remains in the index but is excluded from default API responses unless the `include_unhealthy=true` query parameter is supplied. Administrators can manually re-verify any resource using the CLI command `python manage.py reprobe --url <domain>`.

**Q: Can I use this aggregator behind a corporate proxy or in an air-gapped environment?**

A: Yes, the aiohttp client respects the standard `HTTP_PROXY` and `HTTPS_PROXY` environment variables. For air-gapped deployments, you can populate the initial resource set through the batch import command using a local CSV file instead of relying on external seed lists. The SQLite database operates entirely offline, and the Prometheus exporter is optional. No external telemetry or phone-home calls are made by the core system.

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:00
