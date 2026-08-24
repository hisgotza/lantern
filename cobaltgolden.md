# LinkPilot 资源导航引擎

LinkPilot 是一个面向技术内容创作者、开源社区维护者及数字档案管理者的轻量级资源外链聚合与导航系统。该项目定位为“技术化书签管理基础设施”，非普通用户端收藏工具，而是提供结构化外链入库、分类索引、状态监控与快速分发能力的后端服务与静态生成工具。其核心目标是解决个人或团队在维护大量外部参考链接、镜像站点、文档镜像或社区资源池时面临的链接散落、不可用感知滞后、分类混乱与复用困难问题。

LinkPilot 不提供前端界面，专注提供可编程的链接元数据管理接口、健康检查守护进程、按维度（域名、内容主题、语言、地区、可用性）生成 markdown 目录索引的能力，以及基于规则集的链接自动分类与标签推导引擎。本项目适用于构建技术文档站的后台链接库、开源项目 README 自动外链更新模块、或作为镜像站链接聚合器的数据层。

## 功能概览

- **外链元数据注册与版本追踪**：支持为每个链接记录添加标题、描述、来源上下文、添加时间、最后校验时间、标签与备注，所有变更以增量日志形式存储，便于回溯。

- **声明式分类规则引擎**：用户可编写基于域名、路径关键词、页面标题正则表达式的分类规则集，LinkPilot 在链接入库或更新时自动推导所属类别与子类别，减少人工打标成本。

- **主动健康检查与可用性报告**：内置异步 HTTP/HTTPS 探测模块，可配置超时、重试与状态码白名单，定期对所有注册链接执行可达性检查，生成可用性变化趋势报告，并标记失效链接至隔离区。

- **多维度索引生成器**：根据用户配置的模板（如按域名分组、按内容语言分组、按最后可用时间分组），自动生成结构化 markdown 索引片段，可直接嵌入 README、文档站或 wiki。

- **链接关系图谱导出**：支持将链接之间的引用关系（如“替代站”、“镜像站”、“历史存档”）记录为有向边，导出为 Graphviz dot 格式或 JSON 图数据，便于可视化分析。

- **导入与批量操作接口**：提供从 CSV、JSON Lines、浏览器书签 HTML 导出文件批量导入链接的能力，并支持按标签、时间范围、域名模式进行批量更新标签或批量移动至指定分类。

## 应用场景

- **技术文档站外链自动化维护**：开源项目文档中常常引用大量第三方工具站、规范文档或社区讨论链接，这些链接随时间推移容易失效。LinkPilot 可每日运行健康检查并自动生成“已验证链接”与“需关注链接”列表，帮助文档维护者快速定位死链并替换或移除。

- **社区资源聚合页动态生成**：技术社区或垂直领域知识库需要维护“推荐工具”“学习资料”“镜像站点”等聚合页面。维护者仅需在 LinkPilot 中维护链接池，每次构建站点时通过索引生成器输出最新的 markdown 列表，保证页面内容与后台数据一致，避免手动更新遗漏。

- **镜像站或备用站点关联管理**：当主站点不可用时，用户需要快速找到可用的镜像或替代站点。LinkPilot 可记录主站点与多个备用站点的关联关系，并在健康检查报告中按组显示可用性状态，方便运维人员在故障时迅速切换。

- **历史链接存档与迁移辅助**：在进行网站改版或域名迁移时，大量旧链接需要映射到新地址或标记为过期。LinkPilot 支持批量导入旧链接清单，并通过自定义规则进行路径重写测试，同时保留原始链接作为存档参考，降低迁移过程中的外链断裂风险。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 1. 克隆仓库
git clone https://github.com/your-org/linkpilot.git
cd linkpilot

# 2. 安装依赖（使用 pip 虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化配置与本地数据库
cp config.example.yaml config.yaml
python scripts/init_db.py --config config.yaml

# 4. 导入示例链接数据（含本批次资源）
python scripts/import_links.py --source data/sample_batch_28.csv

# 5. 运行一次健康检查并生成索引报告
python pilot check --config config.yaml --output reports/
python pilot generate --config config.yaml --template README_INDEX.tmpl --output index_output.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 核心运行环境，类型提示与 async/await 语法依赖 |
| pip | 21.0+ | 包管理工具，用于安装项目依赖 |
| SQLite | 3.35+ | 内置数据库，用于存储链接元数据、检查日志与标签体系；生产环境可切换 PostgreSQL |
| Git | 2.25+ | 用于克隆仓库及后续拉取更新 |
| curl | 7.68+ | 健康检查模块默认使用 pycurl 作为后端之一，需系统预装 libcurl 开发头文件 |
| make | 3.81+ | 用于执行常见开发任务（格式化、测试、迁移）的辅助工具（非强制但推荐） |

## 文档导航

| 层面 | 目录 / 文档 | 回答的问题 |
|---|---|---|
| 入门指南 | `docs/quickstart.md` | 如何在 5 分钟内完成首次链接导入并生成索引；基础配置项含义；如何验证安装成功 |
| 配置参考 | `docs/configuration.md` | 配置文件 `config.yaml` 中每个字段（检查间隔、超时、通知钩子、分类规则语法）的完整说明与示例 |
| API 接口 | `docs/api_reference.md` | 内部 Python API 文档，含 `LinkRegistry`、`HealthChecker`、`IndexBuilder` 等核心类的使用方法与参数说明 |
| 运维手册 | `docs/operations.md` | 如何设置定时任务（cron / systemd timer）、如何迁移数据库、如何接入告警通知（邮件/Webhook）以及性能调优建议 |

## 资源列表

本批次入库资源共 7 项，均为中文视频/字幕相关站点。这些链接已作为示例数据包含在初始化导入包中，用户可根据自身需求增删或重新分类。

影视/字幕资源类：
- <code>mianfeizhuijuwangzhanb.org.cn</code>
- <code>gaoqingzhongwenzimub.org.cn</code>
- <code>zaixianbofangnidongdeb.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikanc.org.cn</code>
- <code>zaixianshipinzhongwenzimuc.org.cn</code>
- <code>zaixianbofangzhongwenzimuc.org.cn</code>
- <code>zhongwenshipinzaixianguankanc.org.cn</code>

## 项目结构

```
linkpilot/
├── config.yaml                    # 主配置文件，含检查间隔、分类规则、输出模板路径
├── requirements.txt               # Python 依赖清单（aiohttp, pyyaml, jinja2, pytest 等）
├── Makefile                       # 常用任务快捷命令（init, check, generate, test）
├── README.md                      # 项目概述与快速开始（当前文档）
│
├── linkpilot/                     # 核心源码目录
│   ├── __init__.py               # 版本号与公开 API 导出
│   ├── registry.py               # LinkRegistry 类：链接 CRUD、标签管理、版本日志
│   ├── checker.py                # HealthChecker 类：异步探测、超时控制、状态持久化
│   ├── classifier.py             # 规则引擎：基于域名/路径/标题正则的自动打标
│   ├── generator.py              # IndexBuilder 类：从模板生成 markdown/HTML 索引
│   └── graph.py                  # 关系图构建与导出（dot / JSON）
│
├── scripts/                       # 运维与数据操作脚本
│   ├── init_db.py                # 初始化 SQLite 表结构与迁移
│   ├── import_links.py           # 从 CSV/JSON/书签 HTML 批量导入链接
│   ├── export_links.py           # 按过滤条件导出链接清单
│   └── batch_tag.py              # 按规则批量更新标签
│
├── tests/                         # 单元测试与集成测试
│   ├── test_registry.py
│   ├── test_checker.py
│   └── fixtures/                 # 测试用的示例链接数据与配置文件
│
├── templates/                     # 索引生成器的 Jinja2 模板
│   ├── README_INDEX.tmpl         # 适用于开源项目 README 的外链列表模板
│   ├── wiki_page.tmpl            # 适用于 wiki 的详细分类索引
│   └── health_report.tmpl        # 健康检查报告邮件格式模板
│
├── data/                          # 示例数据与历史导入批次存档
│   ├── sample_batch_28.csv       # 第 28 批次示例链接（含上述 7 个资源）
│   └── archive/                  # 历史导入记录的原始文件备份
│
└── reports/                       # 运行输出目录（健康报告、索引文件、图表）
    ├── latest_health.json
    ├── index_output.md
    └── graph.dot
```

## 贡献指南

1. 阅读 `CONTRIBUTING.md` 了解项目代码规范与提交签名要求，所有 Pull Request 需通过单元测试（`make test`）与代码格式检查（`make lint`）。

2. 在 `issues` 页面选择或创建待解决的问题，建议先讨论设计方向再编写代码，避免较大重构未被提前沟通。

3. 克隆项目并创建新的功能分支（`feature/xxx` 或 `fix/xxx`），确保所有新功能包含对应的单元测试，测试用例覆盖正常路径与异常路径。

4. 提交前运行 `make pre-commit` 自动执行格式化（black）、排序导入（isort）与基础静态检查（flake8），并更新 `docs/` 中相关章节（如新增配置项必须同步更新配置参考文档）。

5. 发起 Pull Request 到主分支，描述中须注明关联的 Issue 编号、变更范围、以及如何验证变更正确性（例如提供测试命令或手动测试步骤）。

## 常见问题

**Q: 健康检查模块是否会误判某些正常站点为不可达？**

A: 有可能。部分站点可能对非浏览器 User-Agent 或特定 IP 范围返回非标准状态码。您可以在配置文件中调整 `checker.valid_status` 白名单列表，以及设置 `checker.custom_headers` 模拟浏览器请求。此外，`checker.follow_redirects` 选项默认开启，若目标站点存在多重跳转且耗时较长，可适当调大 `timeout` 值（单位秒）。建议首次运行时先使用 `--dry-run` 模式观察结果，再调整参数。

**Q: 如何将现有的大量书签（如浏览器导出的 HTML）迁移到 LinkPilot？**

A: 项目提供 `scripts/import_links.py` 脚本，支持 `--format bookmarks_html` 参数解析 Firefox/Chrome 导出的书签文件。解析时会提取书签名称作为标题，URL 作为链接地址，并将书签文件夹路径转换为标签（例如 `收藏夹/技术/后端` 转为 `技术` 和 `后端` 两个标签）。若书签数量极大（超过 5000 条），建议分批导入并利用 `--batch-size` 控制每批提交数量，避免 SQLite 事务过大。

**Q: 生成的索引 markdown 中链接排序混乱，能否按指定规则排序？**

A: 可以。在 `config.yaml` 中 `generator.sort_key` 字段支持多级排序表达式，例如 `['-health_status', 'domain', 'title']` 表示先按健康状态降序（可用优先），再按域名字母序，最后按标题字母序。若需要完全自定义，可编写 Jinja2 模板并在其中使用 `sort` 过滤器，或调用 `IndexBuilder` 时传入 `sort_func` 回调函数。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
