# Project Resource Compass

Project Resource Compass is a curated technical index and external resource aggregation system designed for developers, researchers, and technical writers who need reliable, categorized access to specialized online tools and media resources. The project addresses the common challenge of discovering and maintaining bookmarks for niche web services that are often scattered across personal notes, browser bookmarks, or informal documentation. By providing a structured, version-controlled repository of resource links with metadata and usage context, Project Resource Compass transforms ad-hoc link collection into a maintainable knowledge base that can be shared across teams and integrated into CI/CD workflows for documentation validation.

The target audience includes backend engineers who need to verify media endpoint availability, DevOps practitioners who monitor external service health, technical documentation maintainers who embed reference links in user guides, and researchers who require reproducible resource lists for academic publications. Unlike generic bookmark managers, this project treats each URL as a first-class entity with associated status tracking, category tagging, and change history, enabling automated link rot detection and proactive maintenance alerts.

## 功能概览

- **Categorized Resource Indexing** - Organizes external URLs into logical groups such as media streaming, subtitle services, and real-time playback platforms, with each entry storing the original URL, a descriptive title, and optional tags.

- **Automated Availability Checking** - Periodically pings each registered endpoint to detect HTTP status changes, connection timeouts, or TLS certificate expiration, generating reports that highlight degraded services.

- **Markdown-Based Documentation Generation** - Compiles the resource index into human-readable README sections and separate markdown files that can be published directly to GitHub repositories or static site generators.

- **Version-Controlled Change Tracking** - Maintains a changelog of all URL additions, removals, and updates within the Git history, allowing full auditability and rollback capabilities for production documentation.

- **Batch Import and Export** - Supports importing URL lists from CSV, JSON, or plain text files, and exporting filtered subsets based on category, status, or custom query parameters.

- **Health Dashboard Summary** - Produces a concise terminal-based dashboard that displays the current health status of all monitored resources, color-coded by response category (healthy, warning, critical).

- **Custom Tagging and Annotation** - Allows users to attach arbitrary key-value metadata to each resource entry, enabling fine-grained filtering and integration with external monitoring systems.

- **Slack and Email Alert Integration** - Sends notifications to configured channels when resource availability drops below defined thresholds, ensuring rapid response to external service disruptions.

## 应用场景

- **Documentation Pipeline Validation** - Technical writing teams integrate Project Resource Compass into their CI pipeline to automatically validate that all external links referenced in product manuals resolve correctly before each release. The system flags broken links and generates a report that blocks the build if critical resources are unreachable, ensuring that end users never encounter dead references in published documentation.

- **Media Service Monitoring for Regional Deployments** - Operations teams use the resource index to track availability of region-specific media streaming endpoints across multiple cloud regions. When a particular endpoint fails health checks, the dashboard highlights the affected region, and the alert system notifies the on-call engineer with the exact URL and failure reason, reducing mean time to detection for service degradation incidents.

- **Academic Research Resource Preservation** - Researchers compiling datasets of online media tools use Project Resource Compass to maintain a permanent, citable list of resources referenced in their papers. The version history ensures that reviewers and future readers can see exactly which URLs were active at the time of publication, and the health-check logs provide evidence of availability during the research period.

- **Third-Party API Dependency Mapping** - Microservice teams map all external API endpoints their systems depend on into the resource index, with annotations for rate limits, authentication requirements, and fallback strategies. When an upstream service changes its endpoint structure, the change log helps identify which internal services need updates, streamlining impact analysis and migration planning.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/example/project-resource-compass.git
cd project-resource-compass

# Install dependencies using pip for Python-based tooling
pip install -r requirements.txt

# Initialize the resource database with the default catalog
python compass.py init --catalog resources/default_catalog.json

# Run the initial health check on all registered resources
python compass.py check --all --report summary

# Generate the markdown README from the current resource index
python compass.py generate --output README.md --template templates/readme.j2
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 或更高 | 核心运行环境，用于执行资源检查脚本和生成工具 |
| Git | 2.30 或更高 | 版本控制，用于克隆仓库和提交资源变更记录 |
| curl | 7.68 或更高 | HTTP 健康检查后端，用于执行实际的端点探测请求 |
| jq | 1.6 或更高 | JSON 处理工具，用于解析和格式化资源元数据文件 |
| make | 3.81 或更高 | 构建自动化，用于执行常用任务如更新、检查和生成报告 |
| OpenSSL | 1.1.1 或更高 | TLS 证书验证，用于检测 HTTPS 端点的证书有效性 |
| Bash | 5.0 或更高 | Shell 脚本执行环境，用于包装命令和调度任务 |
| SQLite | 3.31 或更高 | 本地数据库引擎，用于缓存历史检查结果和性能统计 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|-----------|
| 用户指南 | docs/user-guide/getting-started.md | 如何安装、配置首次运行、添加第一个资源条目？ |
| 运维手册 | docs/operations/health-check-config.md | 如何调整检查频率、配置告警阈值、设置通知渠道？ |
| 开发者参考 | docs/development/api-reference.md | 如何编写自定义检查插件、扩展资源导入导出格式？ |
| 设计文档 | docs/design/architecture-overview.md | 系统模块如何划分、数据流如何设计、扩展性如何保证？ |
| 故障排除 | docs/troubleshooting/common-issues.md | 遇到检查超时、证书错误、数据库锁定等问题如何解决？ |
| 版本说明 | CHANGELOG.md | 每个版本新增了哪些功能、修复了哪些缺陷、是否有破坏性变更？ |

## 资源列表

以下为当前索引中收录的全部外部资源链接，按功能类别分组。所有链接均保持用户提供的原始格式，未做任何修改或规范化处理。

### 字幕与媒体资源

- <code>zhongwenzimuzaixianmianfeikanb.org.cn</code>
- <code>zaixianshipinzhongwenzimub.org.cn</code>

### 在线视频播放平台

- <code>zaixianbofangzhongwenzimub.org.cn</code>
- <code>zhongwenshipinzaixianguankanb.org.cn</code>
- <code>shipinmianfeizaixianguankanb.org.cn</code>

### 日韩内容专区

- <code>rimanzaixianguankanb.org.cn</code>
- <code>rihanzaixianmianfeishipinb.org.cn</code>

## 项目结构

```
project-resource-compass/
├── compass.py                 # 主入口脚本，处理 init/check/generate 命令
├── requirements.txt           # Python 依赖列表 (requests, pyyaml, jinja2, click)
├── Makefile                   # 构建任务定义 (update, check-all, generate-docs)
├── config/
│   ├── default.yaml           # 全局配置 (检查间隔、超时阈值、通知渠道)
│   ├── alerts.yaml            # 告警规则定义 (错误率阈值、重试策略)
│   └── categories.yaml        # 资源分类映射 (媒体、API、文档等)
├── resources/
│   ├── default_catalog.json   # 主资源索引 (包含所有 URL 及其元数据)
│   ├── imported_batch_9.json  # 批次导入数据 (第 9 批原始链接)
│   └── archive/               # 历史版本存档 (按日期命名的完整快照)
├── src/
│   ├── checker/               # 健康检查模块 (HTTP/TLS/DNS 探测)
│   │   ├── http.py            # curl 包装器和响应解析
│   │   ├── tls.py             # OpenSSL 证书有效期验证
│   │   └── scheduler.py       # 基于 SQLite 的检查任务队列
│   ├── generator/             # 文档生成模块 (README/CHANGELOG)
│   │   ├── markdown.py        # Jinja2 模板渲染引擎
│   │   └── dashboard.py       # 终端仪表板输出 (彩色状态表)
│   ├── importer/              # 导入导出模块 (CSV/JSON/纯文本)
│   │   ├── csv_parser.py      # 逗号分隔值解析器
│   │   └── validator.py       # URL 格式验证和去重逻辑
│   └── notifier/              # 通知模块 (Slack/Email)
│       ├── slack_client.py    # Webhook 消息构造器
│       └── smtp_sender.py     # SMTP 邮件发送封装
├── templates/
│   ├── readme.j2              # README 主模板 (包含所有章节占位符)
│   └── health_report.j2       # 健康状态报告邮件模板
├── tests/                     # 单元测试和集成测试
│   ├── test_checker.py        # 检查模块测试用例 (mock HTTP 响应)
│   └── test_generator.py      # 生成模块测试 (验证输出格式)
├── docs/                      # 用户文档和运维文档 (Markdown 源码)
│   ├── user-guide/
│   ├── operations/
│   ├── development/
│   └── design/
└── .github/
    └── workflows/
        └── ci.yaml            # GitHub Actions 流水线 (每日检查 + 自动 PR)
```

## 贡献指南

1.  **Fork 仓库并创建功能分支** - 从主仓库 fork 副本到个人账户，然后基于 `main` 分支创建 `feature/your-feature-name` 分支，确保分支命名清晰反映变更内容。

2.  **添加或更新资源条目** - 在 `resources/default_catalog.json` 中按照既定的 JSON Schema 添加新 URL 条目，包括必填字段 `url`、`category`、`description` 和可选的 `tags` 数组。对于批量导入，将原始列表放入 `resources/imported_batch_*.json` 并使用导入命令合并。

3.  **运行本地验证和测试** - 执行 `make test` 运行全部单元测试，执行 `make check-all` 对所有新添加的资源进行实际健康检查，确保无超时或证书错误。如果添加了自定义检查插件，需补充对应的测试用例。

4.  **更新文档和示例** - 如果变更影响了用户可见的功能（如新增命令参数、修改配置格式），同步更新 `docs/` 下对应的用户指南章节，并在 `CHANGELOG.md` 中添加条目，注明变更类型（新增、修复、废弃）。

5.  **提交 Pull Request** - 将功能分支推送到个人 fork，然后向主仓库的 `main` 分支发起 PR。PR 描述中需引用相关 issue 编号（如有），并附上本地检查报告的输出摘要。等待 CI 流水线通过和至少一位维护者审核后即可合并。

## 常见问题

**Q: 健康检查报告显示大量超时，但这些资源在浏览器中可以正常访问，如何解决？**

A: 这种情况通常由网络环境差异引起。检查 `config/default.yaml` 中的 `timeout` 和 `retry` 参数，默认值为 10 秒超时和 2 次重试。对于响应较慢的媒体服务，建议增加超时到 30 秒，并将重试次数调整为 3 次。同时，确认运行检查的服务器是否具有访问目标域名的网络权限，某些区域可能需要配置代理或调整 DNS 解析器。如果问题持续，使用 `--verbose` 选项运行检查以获取详细的 curl 调试输出。

**Q: 如何批量导入大量 URL 而无需手动编辑 JSON 文件？**

A: 使用 `import` 命令支持多种格式。将 URL 列表保存为纯文本文件（每行一个 URL），然后执行 `python compass.py import --input urls.txt --format plain --category media`。对于 CSV 文件，确保列头包含 `url, category, description`，执行 `python compass.py import --input catalog.csv --format csv`。导入工具自动执行去重和格式验证，生成待审核的暂存条目，审核通过后使用 `--commit` 参数正式写入主索引。

**Q: 生成的 README 中 URL 被自动添加了 http:// 前缀，如何保持原始格式？**

A: 这是模板引擎的默认行为，用于确保链接可点击。如需保留纯文本格式，在 `templates/readme.j2` 中找到 `{{ resource.url | urlize }}` 过滤器，改为 `{{ resource.url }}` 即可禁用自动链接化。对于严格的纯展示需求，建议在资源条目的 `metadata` 字段中添加 `raw: true` 标记，并在模板中条件判断是否应用格式化。

## 许可证

MIT License

Copyright (c) 2026 Project Resource Compass Maintainers

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
