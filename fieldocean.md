# Terminus Resource Gateway

Terminus Resource Gateway is a curated technical documentation and multimedia resource aggregation platform designed for developers, content researchers, and digital archivists who require structured access to distributed subtitle and video metadata repositories. The project addresses the fragmentation of online media ancillary data by providing a unified, queryable index over heterogeneous external resources, enabling users to locate, cross-reference, and retrieve auxiliary content without navigating individual silos. It is not a hosting service nor a player; it is a lightweight gateway that normalizes resource locators, validates availability, and presents discoverable entry points for downstream processing pipelines.

## 功能概览

- **Unified Resource Indexing** – Aggregates external locators into a normalized catalog with deduplication and freshness tagging.

- **Locator Health Check** – Periodically probes each registered URL for HTTP reachability and TLS validity, flagging stale endpoints.

- **Categorized Browsing** – Groups resources by functional domains such as subtitle archives, video metadata, and streaming auxiliary data.

- **Plain-Text Query Interface** – Supports grep-style pattern matching over resource descriptions and locator strings.

- **Exportable Manifest** – Generates machine-readable JSON and plain-text lists of all tracked URLs for integration with external fetchers.

- **Minimal Dependency Footprint** – Runs on a single Node.js process with no persistent database, using file-based state snapshots.

- **Docker-Ready Deployment** – Includes a container definition for ephemeral, reproducible execution environments.

## 应用场景

- **Offline Media Analysis** – Researchers preparing offline corpora for subtitle alignment or speech-to-text validation can use the gateway to retrieve a comprehensive list of auxiliary resource endpoints without manual web scraping.

- **Streaming Pipeline Configuration** – DevOps engineers integrating third-party subtitle or metadata sources into transcoding workflows can query the gateway for validated locators and embed them into configuration management systems.

- **Educational Content Curation** – Educators compiling supplementary materials for language learning courses can leverage the categorized resource lists to quickly identify relevant subtitle repositories for specific genres or difficulty levels.

- **Accessibility Compliance Auditing** – Digital accessibility teams can cross-reference the gateway's resource catalog against internal databases to ensure that closed-captioning references remain current and resolvable.

- **Local Mirror Planning** – System administrators planning regional mirrors or offline caches can export the full manifest to prioritize which external domains to replicate based on update frequency and response times.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/terminus-resource-gateway/trg-core.git
cd trg-core

# Install dependencies
npm install

# Run the gateway in development mode
npm start

# Optionally, run a full resource health check
npm run probe:all
```

After startup, the gateway listens on port 3000 by default. Access the web interface at `http://localhost:3000` or use the REST API endpoints documented in the `/docs` route.

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | 18.x LTS or 20.x LTS | Runtime environment for the gateway core |
| npm | 9.x or higher | Package manager for dependency resolution |
| Git | 2.25+ | Required for cloning and version control operations |
| curl | 7.68+ | Used internally for outbound health probes (fallback) |
| wget | 1.20+ | Optional alternative for resource fetching in export scripts |
| ca-certificates | latest | Required for TLS validation during health checks |
| POSIX-compliant shell | bash 4.4+ / zsh 5.8+ | For running utility scripts and cron wrappers |
| Disk space | 50 MB minimum | For storing state snapshots and logs (no media content stored) |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user-guide/` | How to browse, search, and export resource lists; interpretation of health status indicators. |
| 运维参考 | `/docs/operations/` | Deployment strategies, probe scheduling, log rotation, and performance tuning. |
| API 参考 | `/docs/api/` | Endpoint specifications, request/response schemas, and authentication (if enabled). |
| 开发指南 | `/docs/development/` | Code architecture, testing procedures, and contribution workflows for maintainers. |
| 资源规范 | `/docs/specs/resource-manifest.md` | The formal schema for resource entries, including required and optional metadata fields. |
| 故障排查 | `/docs/troubleshooting/` | Common error codes, probe failures, and network constraint resolutions. |

## 资源列表

本网关当前索引的第三方资源均来源于公开可访问的域名，按内容类别划分如下。所有条目均以原始形式收录，不做协议补全或域名规范化。

### 字幕辅助资源

- <code>gaoqingzhongwenzimuc.org.cn</code>

- <code>zaixianbofangnidongdec.org.cn</code>

- <code>zhongwenzimuzaixianmianfeikand.org.cn</code>

### 视频元数据与播放辅助

- <code>zaixianshipinzhongwenzimud.org.cn</code>

- <code>zaixianbofangzhongwenzimud.org.cn</code>

### 综合媒体观赏索引

- <code>zhongwenshipinzaixianguankand.org.cn</code>

- <code>shipinmianfeizaixianguankand.org.cn</code>

These endpoints are periodically probed for availability. Users are advised to verify each locator's accessibility in their own network environment before integrating into production workflows.

## 项目结构

```
trg-core/
├── src/                           # Core source code
│   ├── index.js                   # Application entry point, server bootstrap
│   ├── routes/                    # REST API route handlers
│   │   ├── health.js              # /health endpoint for liveness checks
│   │   ├── resources.js           # /resources CRUD and query endpoints
│   │   └── manifest.js            # /manifest export handler (JSON/plain)
│   ├── probes/                    # Health probing subsystem
│   │   ├── http-probe.js          # HTTP/HTTPS reachability checker
│   │   ├── tls-validator.js       # Certificate expiration and cipher suite verifier
│   │   └── scheduler.js           # Cron-based periodic probe orchestrator
│   ├── store/                     # In-memory and file-backed state management
│   │   ├── memory-store.js        # Volatile key-value cache
│   │   ├── file-snapshot.js       # Snapshot serialization to /data/manifest.json
│   │   └── migrator.js            # Schema migration helpers for state upgrades
│   └── utils/                     # Shared utility functions
│       ├── logger.js              # Structured logging (JSON lines)
│       ├── config-loader.js       # Environment variable and .env parsing
│       └── url-normalizer.js      # Internal normalization (not for output)
├── config/                        # Environment-specific configurations
│   ├── default.json               # Baseline settings (port, probe interval)
│   ├── production.json            # Overrides for production deployment
│   └── development.json           # Overrides for local development
├── data/                          # Persistent state directory (git-ignored)
│   └── manifest.snapshot.json     # Current resource list with probe timestamps
├── scripts/                       # Maintenance and utility scripts
│   ├── import-csv.js              # Bulk import resources from CSV
│   ├── export-json.js             # Export manifest as JSON to stdout
│   └── health-report.sh           # Shell wrapper for email alerting
├── tests/                         # Unit and integration test suite
│   ├── unit/                      # Isolated function tests (Mocha + Chai)
│   ├── integration/               # End-to-end API tests (Supertest)
│   └── fixtures/                  # Mock probe responses and sample manifests
├── docs/                          # Full documentation (see navigation table)
├── Dockerfile                     # Multi-stage container build definition
├── docker-compose.yml             # Local orchestration with Prometheus sidecar
├── package.json                   # npm dependencies and script definitions
├── .env.example                   # Environment variable template
├── .gitignore                     # Standard ignore rules for Node.js
└── README.md                      # This file
```

## 贡献指南

We welcome contributions that improve resource indexing accuracy, expand probe coverage, or enhance documentation clarity. Please follow the steps below.

1. Fork the repository and create a new feature branch from `main` with a descriptive name, e.g., `feature/add-icmp-probe` or `docs/update-api-examples`.

2. Ensure all existing tests pass by running `npm test` and add new tests for any modified or introduced functionality. Code coverage should not decrease.

3. Update the resource manifest specification in `/docs/specs/resource-manifest.md` if your changes affect the state schema, and provide a sample entry illustrating the new fields.

4. Submit a pull request with a clear title and a detailed description of the motivation, implementation approach, and any potential side effects on existing probe schedules.

5. After review, a maintainer will merge your PR and trigger a staging deployment. Please monitor the GitHub Actions workflow for any post-merge failures and address them promptly.

For major architectural changes, please open an issue first to discuss the design with the core team before investing significant effort. We prioritize backward compatibility and minimal disruption to existing users.

## 常见问题

**Q: The gateway reports a resource as "unreachable" but I can access it from my browser. Why is that?**

A: The gateway performs probes from its own network context, which may differ from your local environment. Common causes include outbound firewall restrictions, DNS resolution differences, or TLS cipher suite mismatches. You can override the probe timeout and retry settings via the `PROBE_TIMEOUT_MS` and `PROBE_RETRY_COUNT` environment variables. Additionally, the gateway does not follow certain redirect chains beyond the first hop, so a multi-step redirection may be misinterpreted.

**Q: How often does the gateway refresh its resource list? Can I trigger a manual refresh?**

A: The automatic refresh interval is set to 3600 seconds (1 hour) by default. You can adjust this via the `REFRESH_INTERVAL_SECONDS` configuration. To trigger an immediate manual refresh, send a POST request to `/api/v1/probe/run` with an optional list of specific resource IDs, or omit the body to probe all indexed entries. The response includes a summary of newly updated statuses.

**Q: Does the gateway store any media content, subtitle files, or video data locally?**

A: No. The gateway only stores resource locators (URLs) and their associated metadata, such as last probe timestamp, HTTP status code, and response time. It does not download, cache, or relay any media payloads. All content referenced by the listed URLs remains exclusively on the respective third-party domains. Users are responsible for respecting the terms of service of each external resource.

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:25
