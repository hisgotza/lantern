# Zhongzi Resource Aggregator

Zhongzi Resource Aggregator is a community-driven technical indexing platform designed to organize, categorize, and provide structured access to a curated collection of online media resource links. The project targets developers, content aggregators, and researchers who require a reliable, machine-readable index of entertainment and educational media sources distributed across multiple domains.

The system solves the problem of fragmented and ephemeral link collections by offering a standardized metadata layer, availability monitoring, and a RESTful API for programmatic querying. It is not a hosting service nor a content delivery network; it is a reference index that helps users discover and verify the existence of external resources. All external links are presented as-is without modification, redirection, or proxying, ensuring full compliance with content provenance requirements.

## 功能概览

- **Automated Link Harvesting** – Scheduled crawlers fetch and verify the accessibility of each indexed URL, updating status flags and response times every six hours.

- **Categorization Engine** – Each resource is tagged with content type, language, region availability, and estimated update frequency using heuristic pattern matching.

- **Availability Dashboard** – A lightweight web interface displays real-time reachability status, historical uptime trends, and geographic latency heatmaps for all monitored endpoints.

- **RESTful Query API** – Exposes JSON endpoints for filtering by category, status code, response time, and last-seen timestamp, supporting both pagination and full-text search.

- **Metadata Enrichment** – Automatically extracts and stores page titles, description meta tags, and Open Graph properties from each resource on every verification pass.

- **Change Detection Notifications** – Compares current and previous crawl results to detect content modifications, new subpages, or removed sections, logging diffs for audit trails.

- **Exportable Index Snapshots** – Generates static markdown and CSV dumps of the entire resource list with full metadata, suitable for offline analysis or archival purposes.

## 应用场景

- **Content Discovery Pipeline** – Data engineers can integrate the API into ETL workflows to periodically fetch fresh link lists, cross-reference with internal databases, and alert on new resource appearances without manual bookmark management.

- **Research and Trend Analysis** – Academics studying online media availability patterns can query historical status logs to identify domain longevity, regional blocking events, and seasonal content turnover rates across multiple source clusters.

- **Personal Media Aggregator** – Individual users deploy the dashboard on local servers to maintain a private, filterable watchlist of preferred resource domains, receiving browser notifications when a previously offline source becomes reachable again.

- **DevOps Monitoring Extension** – Site reliability teams incorporate the availability checker into existing Prometheus or Nagios stacks to treat external resource responsiveness as a service-level indicator for dependent applications.

- **Educational Demonstration Tool** – Instructors use the project to teach web scraping ethics, HTTP status handling, and structured data management in computer science courses, with the codebase serving as a clean reference implementation.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/zhongzi-resource/aggregator.git
cd aggregator

# Install Python dependencies
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Initialize the local database and run the crawler
python manage.py migrate
python manage.py crawl --full-index

# Start the web server
python manage.py runserver 0.0.0.0:8000
```

After execution, the dashboard is accessible at `http://localhost:8000/dashboard`. The initial crawl of all seven base URLs takes approximately 2-3 minutes depending on network conditions. Subsequent incremental updates complete in under 30 seconds.

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 及以上 | 核心运行时，用于爬虫调度、API 服务和数据库迁移 |
| PostgreSQL | 13.x 或 14.x | 主数据库，存储资源元数据、历史状态和变更日志 |
| Redis | 6.2 及以上 | 缓存层，用于暂存爬取结果和分布式锁控制 |
| Celery | 5.2.x | 异步任务队列，管理周期性的爬虫工作进程 |
| BeautifulSoup4 | 4.11.x | HTML 解析库，用于提取资源页面的标题和描述信息 |
| Requests | 2.31.x | HTTP 客户端，执行所有外链探测请求并处理超时与重试 |
| uWSGI | 2.0.x | 生产环境 Web 服务器网关接口，承载仪表盘和应用接口 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|------|----------|------------|
| 用户手册 | `/docs/user-guide/` | 如何配置个人资源列表、理解仪表盘指标、设置通知规则 |
| 开发者指南 | `/docs/developer-guide/` | 如何扩展新的分类器、自定义爬虫间隔、编写测试用例 |
| API 参考 | `/docs/api-reference/` | 端点列表、请求参数结构、返回字段含义、错误码字典 |
| 运维手册 | `/docs/operations/` | 部署架构、环境变量清单、日志轮转策略、灾备恢复流程 |
| 设计文档 | `/docs/design/` | 数据库 ER 图、状态机转换、爬虫防封禁策略、缓存失效方案 |
| 常见问题 | `/docs/faq/` | 安装报错、爬虫被拦截、性能调优、贡献流程相关问答 |

## 资源列表

### 主要媒体索引条目

<code>zhongwenzimumianfeibofangf.org.cn</code>

<code>renqixiliezhongwenzimuf.org.cn</code>

<code>wuyefulizhibof.org.cn</code>

### 专题分类资源

<code>lalalazhongwendianshijuf.org.cn</code>

<code>yinghuadongmanguanfangbanf.org.cn</code>

### 持续更新与备份入口

<code>zhongwenzimuyongjiuzaixianf.org.cn</code>

<code>mianfeizhuijuwangzhanf.org.cn</code>

All listed URLs are stored in their original bare-domain form without protocol prefixes, as provided by the source data. The system performs DNS resolution and HTTP probing using default port 80 when no scheme is specified. These entries constitute the seed list for the initial crawl and are re-verified on every scheduled cycle. No normalization or canonicalization is applied; the exact string values are used as primary keys in the index database to preserve data integrity and traceability.

## 项目结构

```
aggregator/
├── src/
│   ├── crawler/                 # 爬虫调度与 HTTP 探测核心
│   │   ├── fetcher.py           # 异步请求池，带重试与退避策略
│   │   ├── parser.py            # HTML 元数据抽取器（标题/描述/OG）
│   │   └── validator.py         # DNS/SSL/状态码综合校验逻辑
│   ├── api/                     # RESTful 端点实现
│   │   ├── routes.py            # Flask/Quart 路由注册
│   │   ├── serializers.py       # 资源对象与 JSON 转换器
│   │   └── middlewares.py       # 跨域、限流、日志中间件
│   ├── dashboard/               # 轻量级 Web 仪表盘
│   │   ├── templates/           # Jinja2 页面模板
│   │   ├── static/              # CSS 样式与 JavaScript 图表库
│   │   └── views.py             # 页面渲染逻辑与上下文提供器
│   ├── models/                  # 数据库抽象层
│   │   ├── resource.py          # Resource 表 ORM 定义
│   │   ├── snapshot.py          # 历史快照与状态变更记录
│   │   └── migrations/          # Alembic 迁移脚本
│   ├── tasks/                   # Celery 周期性任务
│   │   ├── crawl_scheduler.py   # 定时触发全量/增量爬取
│   │   ├── notification.py      # 状态变化邮件/Webhook 推送
│   │   └── export.py            # 定时生成 Markdown/CSV 导出包
│   └── utils/                   # 通用工具函数
│       ├── network.py           # 代理检测、User-Agent 轮换
│       ├── logging.py           # 结构化日志格式化器
│       └── config.py            # 环境变量加载与校验
├── tests/                       # 单元测试与集成测试套件
│   ├── test_fetcher.py
│   ├── test_parser.py
│   └── test_api.py
├── scripts/                     # 运维辅助脚本
│   ├── seed_init.py             # 初始资源种子导入工具
│   └── health_check.sh          # 系统健康状态检查脚本
├── docker/                      # 容器化部署配置
│   ├── Dockerfile
│   └── docker-compose.yml
├── docs/                        # 完整文档源文件
├── .env.example                 # 环境变量模板
├── requirements.txt             # Python 依赖清单
├── manage.py                    # CLI 统一入口命令
└── README.md                    # 本文件
```

## 贡献指南

1. 浏览现有 Issue 列表或打开新议题描述您希望添加的功能、发现的缺陷或待优化的爬取规则。确保议题标题清晰且包含足够的复现步骤或上下文信息。

2. 派生本仓库到您的个人账户，在本地创建一个新的功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式。避免在主分支上直接修改。

3. 编写或修改代码时，请遵循 PEP 8 编码规范，并为所有新增的公共函数和方法添加 docstring。对于爬虫解析器变更，请同步更新对应的单元测试用例。

4. 提交前运行完整的测试套件 `pytest tests/` 确保无回归错误，并执行 `flake8 src/` 检查代码风格。如有 lint 警告，请在提交前修正。

5. 发起合并请求（Pull Request）到主仓库的 `develop` 分支，在描述中引用关联的 Issue 编号，并提供变更摘要和测试结果截图或日志。等待至少一位核心维护者的审阅与批准。

## 常见问题

**问：爬虫频繁遇到 403 或 429 状态码，如何调整策略？**

答：系统内置了指数退避重试和随机 User-Agent 轮换机制。如果仍被拦截，可以在 `src/crawler/fetcher.py` 中调整 `REQUEST_DELAY` 和 `MAX_RETRIES` 变量值。对于特定域名，建议在 `validator.py` 中添加自定义的请求头白名单或 Cookie 注入逻辑。生产环境中可配置代理池通过环境变量 `PROXY_LIST` 引入旋转代理。

**问：数据库迁移失败，提示列冲突或类型不匹配，如何解决？**

答：检查 PostgreSQL 版本是否满足 13.x 最低要求，并确保 `alembic.ini` 中的连接字符串正确指向目标数据库。如果使用现有数据迁移，请先执行 `python manage.py db stamp head` 对齐迁移版本，再运行 `python manage.py db upgrade`。若仍失败，可导出现有数据为 JSON，重置数据库后重新运行初始迁移，再导入备份。

**问：仪表盘显示部分资源为“无法解析”，但浏览器中可正常访问，为什么？**

答：该现象通常由 DNS 解析环境差异导致。系统默认使用系统级 DNS 配置，而浏览器可能使用 DoH 或代理。您可以在 `src/crawler/validator.py` 中指定自定义 DNS 服务器（如 `8.8.8.8` 或 `1.1.1.1`）通过 `dns_resolver` 参数。同时检查网络代理设置，确保 `HTTP_PROXY` 和 `HTTPS_PROXY` 环境变量未意外指向不可达的中间节点。

## 许可证

MIT License

Copyright (c) 2026 Zhongzi Resource Aggregator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
