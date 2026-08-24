# Omei Resource Hub

Omei Resource Hub is a curated technical index and external link aggregation system designed for developers, researchers, and content curators who need to organize, categorize, and rapidly access a wide spectrum of online resources spanning video distribution, animation archives, and multimedia content repositories. Unlike general-purpose bookmark managers or browser-based link collections, Omei Resource Hub provides a structured, version-controlled, and machine-readable inventory of domain-specific assets, enabling teams to maintain consistent references across documentation, testing environments, and compliance audits.

This project targets technical leads, DevOps engineers, and QA specialists who routinely handle external dependencies such as test video streams, sample datasets, or third-party content sources that must be reproducibly referenced in automated pipelines. By treating URLs as first-class infrastructure assets with metadata annotations, Omei Resource Hub eliminates the friction of manual link discovery, reduces broken-reference incidents, and facilitates peer review of external resource selections. The system is deliberately lightweight, requiring no external databases or cloud services, and operates entirely from a static file hierarchy that can be served locally, mounted in CI runners, or published as a standalone static site.

## 功能概览

- **Hierarchical Categorization Engine** – Organizes raw URL lists into logical taxonomies such as video platforms, animation repositories, and comprehensive media portals, with automated category detection based on domain naming heuristics.

- **Metadata Annotation Framework** – Attaches descriptive tags, status flags (active/deprecated), and last-verified timestamps to each resource entry, supporting custom YAML frontmatter in resource definition files.

- **Static Site Generation Pipeline** – Transforms the underlying YAML/JSON resource manifests into a fully navigable HTML dashboard with search and filter capabilities, using a built-in templating system with zero runtime dependencies.

- **Integrity Verification Module** – Performs periodic HEAD requests and SSL certificate expiry checks on all registered URLs, logging failures to a structured report that can be consumed by monitoring agents or alerting systems.

- **Versioned Snapshot Mechanism** – Maintains immutable changelogs for every modification to the resource registry, enabling rollback to any previous state and facilitating compliance tracking for regulated environments.

- **RESTful Query Endpoint** – Exposes a lightweight HTTP API that returns resource lists in JSON or CSV format, allowing seamless integration with external automation tools, test harnesses, and data processing workflows.

- **Tag-Based Filtering and Search** – Supports multi-tag boolean queries (AND/OR) and fuzzy search over domain names and descriptions, with result ranking based on usage frequency and recency of verification.

## 应用场景

- **CI/CD Pipeline External Dependency Mirroring** – Teams can reference the curated resource list to pre-fetch or mirror external test assets (e.g., sample video streams or animation clips) before running integration suites, ensuring that transient network issues or domain outages do not cause spurious test failures.

- **Compliance Audit Trail for Third-Party Content** – Organizations subject to regulatory oversight can maintain an auditable inventory of all external media sources used in products or marketing materials, with timestamped records of when each URL was added, reviewed, and approved.

- **Documentation Consistency Across Distributed Teams** – Technical writers and API documenters can embed stable resource identifiers from the hub into their markdown files, guaranteeing that code examples, screenshots, and reference links remain consistent across multiple product versions and regional deployments.

- **Educational Curriculum Asset Management** – Instructors and course authors can batch-manage external reading lists, video references, and supplementary material links for multi-section courses, with the ability to produce per-module extracts from the central registry without duplicating entries.

- **Content Aggregator Proof-of-Concept Prototyping** – Product managers and frontend developers can rapidly prototype content aggregation dashboards by consuming the JSON API endpoint, iterating on UI designs without the need to repeatedly scrape or manually collect target URLs from disparate sources.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/omei-dev/omei-resource-hub.git
cd omei-resource-hub

# Install dependencies (Python 3.9+ required)
pip install -r requirements.txt

# Build the static site and verify all resources
python build.py --verify --output ./dist

# Start the local development server
python serve.py --port 8080 --root ./dist
```

After running the above commands, open your browser to `http://localhost:8080` to view the generated dashboard. The verification step will produce a `verification-report.json` in the project root, listing any unreachable or SSL-expired resources.

## 安装要求

| Dependency | Minimum Version | Required For |
|------------|----------------|--------------|
| Python | 3.9 | Core runtime, build scripts, and API server |
| PyYAML | 6.0 | Parsing resource manifests with metadata |
| requests | 2.28 | Integrity verification and HEAD request checks |
| markdown | 3.4 | Rendering documentation pages from markdown sources |
| jinja2 | 3.1 | Templating engine for static site generation |
| click | 8.1 | CLI command parsing and interactive prompts |
| pytest | 7.2 | Running unit and integration test suites (development only) |
| flake8 | 6.0 | Code style enforcement (development only) |
| mypy | 1.0 | Static type checking (development only) |

## 文档导航

| Layer | Directory / Entry | Questions Addressed |
|-------|-------------------|----------------------|
| User Guide | `docs/user-guide/` | How to navigate the dashboard, apply filters, interpret verification statuses, and export resource lists. |
| Administrator Handbook | `docs/admin/` | How to add, remove, or update resource entries; manage metadata schemas; and configure verification intervals. |
| API Reference | `docs/api/` | What REST endpoints are available, their request/response schemas, rate-limiting policies, and authentication methods. |
| Developer Cookbook | `docs/developer/` | How to extend the category classifier, write custom verification plugins, and contribute new themes to the static generator. |
| Deployment Guide | `docs/deployment/` | How to deploy the static output to S3, Netlify, or any origin server; and how to set up the verification cron job in production. |

## 资源列表

### Comprehensive Media Portals

- <code>oumeirihanzonghezaixian.org.cn</code>
- <code>youyouziyuanwang.org.cn</code>

### Online Video Platforms

- <code>miyouzaixianshipin.org.cn</code>
- <code>yejianfulishipin.org.cn</code>
- <code>hanshicaoshipinzaixianguankan.org.cn</code>

### Animation and Visual Content Archives

- <code>yinghuadongmanxiazai.org.cn</code>

### Standalone Image / Media Galleries

- <code>meinvzaixianguankan.org.cn</code>

## 项目结构

```
omei-resource-hub/
├── build.py                 # Main build script orchestrating site generation and verification
├── serve.py                 # Local development server with live-reload support
├── requirements.txt         # Production and development dependency list
├── config/
│   ├── categories.yaml      # Mapping of domain patterns to resource categories
│   ├── tags.yaml            # Predefined tag taxonomy with color and description
│   └── verify-policy.yaml   # Timeout, retry, and SSL tolerance settings
├── resources/
│   ├── manifests/           # YAML files each describing a resource entry with URL, tags, description
│   │   ├── media-portals.yaml
│   │   ├── video-platforms.yaml
│   │   ├── animation-archives.yaml
│   │   └── image-galleries.yaml
│   ├── snapshots/           # Historical copies of the full resource registry (read-only)
│   └── changelog/           # Individual change records with timestamps and author info
├── src/
│   ├── core/                # Resource model, validation logic, and category inference
│   ├── verifier/            # HTTP/S checker, SSL certificate inspector, and report aggregator
│   ├── generator/           # Static site renderer using Jinja2 templates
│   ├── api/                 # Flask-based REST endpoint implementation
│   └── cli/                 # Click command wrappers for build, verify, serve, and export
├── templates/               # HTML templates for dashboard, detail pages, and error views
├── static/                  # CSS, JavaScript, and font assets served alongside generated pages
├── tests/
│   ├── unit/                # Isolated tests for resource model, verifier, and category logic
│   └── integration/         # End-to-end build and API response tests
├── docs/                    # Full documentation split by user, admin, API, and developer guides
└── .github/
    └── workflows/           # GitHub Actions for CI verification, linting, and static deployment
```

## 贡献指南

1. **Fork the repository and create a feature branch** – Fork the main project on GitHub, then create a new branch with a descriptive name such as `feature/add-category-heuristics` or `fix/verifier-timeout`. Ensure your branch is based on the latest `main` commit.

2. **Update resource manifests or code following the existing style** – For resource additions, edit the appropriate YAML file under `resources/manifests/` and include all required fields (`url`, `category`, `tags`, `description`). For code contributions, adhere to the project's PEP8 style with line length 100, and run `flake8` and `mypy` locally before committing.

3. **Write or update unit tests covering your changes** – Place new unit tests in `tests/unit/` with filenames matching the module under test. For new features, achieve at least 85% coverage for the added code. Integration tests are required for any changes affecting the build pipeline or API endpoints.

4. **Run the full test suite and verify the build succeeds** – Execute `pytest tests/` from the project root. Also run `python build.py --verify` to ensure no resource entries are broken and the static site generates without errors. Fix any failures before proceeding.

5. **Submit a pull request with a clear change description** – Open a pull request against the `main` branch, referencing any related issues. In the PR description, summarize the changes, list the affected components, and note whether the verification report was regenerated. Await review from maintainers, who may request additional modifications.

## 常见问题

**Q: How often are the resources automatically verified, and what happens when a URL becomes unreachable?**

A: By default, the verification module runs every 24 hours when the system is deployed with the provided cron configuration (see `docs/deployment/`). When a URL fails the HEAD request or SSL check, it is flagged as `unreachable` in the verification report and marked with a warning icon in the generated dashboard. The build process does not fail for unreachable resources, but the report is persisted as `verification-report.json` for monitoring purposes. Administrators can manually re-run verification with `python build.py --verify --force` and update or deprecate entries as needed.

**Q: Can I host the static site on a CDN or object storage without running a Python server?**

A: Yes. The output generated in the `./dist` directory is completely static – HTML, CSS, JavaScript, and JSON data files. You can upload the entire `dist` folder to any static hosting service such as AWS S3, Cloudflare R2, Netlify, or Vercel. The dashboard includes client-side search and filter functionality that consumes the embedded JSON index, so no server-side processing is required at runtime. For the verification cron job, you only need a separate environment (e.g., a GitHub Actions scheduled workflow) that runs the build script periodically and re-deploys the updated static files.

**Q: How do I add custom metadata fields to a resource entry without modifying the core schema?**

A: The resource YAML schema supports an extensible `extra` dictionary field. For example, you can add `extra: { region: "cn-north", bandwidth: "high" }` to any entry. These fields are preserved during parsing and passed through to the JSON API endpoint and the template context. To display custom fields in the dashboard, override the `templates/resource-card.html` partial in your own theme directory (configured via `config/theme.yaml`). The core validation logic ignores unknown keys inside `extra`, so they do not interfere with required fields.

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
