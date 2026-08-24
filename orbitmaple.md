# Rimanzaixian Resources Hub

Rimanzaixian Resources Hub 是一个面向中文互联网内容索引与导航的开源基础设施项目，旨在系统化整理并持续维护一批高频访问的在线媒体与内容资源入口。项目本身不存储、不分发、不缓存任何第三方内容，仅提供可公开访问的 URL 索引信息与结构化元数据，便于开发者、研究人员及内容消费者快速定位相关服务。

本项目面向以下用户群体：需要批量管理内容源地址的系统管理员、从事网络媒体观测的数据分析人员、以及对特定类型在线内容有持续访问需求的普通用户。通过本项目提供的索引表与工具脚本，用户可以一键完成资源可达性检测、响应时间监控、以及 URL 变更追踪，显著降低人工维护成本。

## 功能概览

- **资源索引聚合**：集中收录多个主流中文在线内容服务入口，按服务类型与访问频率分类管理，支持自定义标签扩展。

- **可达性健康检查**：内置基于 HTTP HEAD/GET 方法的主动探测脚本，可定时检测每个 URL 的响应状态码与延迟，输出结构化 JSON 报告。

- **变更通知机制**：当监测到 URL 响应内容长度、重定向目标或状态码发生异常变化时，通过标准输出日志与可选的 Webhook 接口发出告警。

- **元数据注解系统**：允许用户为每个 URL 添加备注字段，记录服务描述、备用入口、维护状态等关键信息，所有注解存储于 YAML 配置文件中。

- **批量导出与导入**：支持将当前索引库导出为 CSV、JSON 或纯文本列表格式，便于与其他自动化工具或监控平台集成。

- **轻量化部署**：项目无外部数据库依赖，所有配置与缓存数据存储于本地文件系统，可运行于任何 POSIX 兼容环境。

- **访问统计摘要**：对每次探测任务生成摘要报告，包含成功率、平均响应时间、最慢端点等关键指标，辅助评估服务质量。

## 应用场景

- **个人内容访问加速**：用户可将本项目作为个人浏览器的起始页或书签管理后端，通过本地脚本快速检测当前可用的服务入口，避免因个别域名不可达而中断访问。

- **网络质量监测**：运维人员可配置定时任务（如每 5 分钟执行一次探测脚本），结合项目输出的 JSON 报告与第三方告警系统（如 Prometheus、Zabbix）对接，实现对多个内容源可用性的持续监控。

- **数据采集前置检查**：在进行大规模数据采集或内容分析前，研究人员可运行本项目的预检模块，批量验证目标 URL 的可访问性与重定向链路，提前筛除异常端点，提升采集任务成功率。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，确保系统已安装 Git 与 Python 3.8 及以上版本。

```bash
# 1. 克隆项目仓库
git clone https://github.com/rimanzaixian/rimanzaixian-hub.git
cd rimanzaixian-hub

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 执行首次资源探测（默认读取 config/urls.yaml）
python src/probe.py --config config/urls.yaml --output reports/status.json

# 4. 查看探测结果摘要
cat reports/status.json | python src/summary.py
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.8 及以上 | 核心运行环境，用于执行探测脚本与工具链 |
| Git | 2.20 及以上 | 用于克隆仓库及版本管理 |
| pip | 21.0 及以上 | Python 包管理工具，用于安装依赖库 |
| requests | 2.25.0 及以上 | HTTP 请求库，用于发送探测请求 |
| PyYAML | 5.4.0 及以上 | YAML 配置文件解析支持 |
| colorama | 0.4.4 及以上 | 终端彩色输出支持（非强制，建议安装） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何配置探测参数、调整超时时间、添加自定义 URL 条目？ |
| 运维指南 | docs/operation-guide.md | 如何部署定时任务、配置告警 Webhook、备份索引数据？ |
| 开发者文档 | docs/developer-guide.md | 如何扩展探测协议（如 TCP/UDP）、新增输出格式插件？ |
| API 参考 | docs/api-reference.md | 各模块函数签名、参数说明及异常类型定义。 |
| 变更日志 | CHANGELOG.md | 每个版本的发布记录、新增功能与修复内容。 |
| 行为准则 | CODE_OF_CONDUCT.md | 社区贡献者之间的互动规范与冲突处理原则。 |

## 资源列表

### 中文在线视频内容索引

<code>rimanzaixianguankanc.org.cn</code>

<code>rihanzaixianmianfeishipinc.org.cn</code>

<code>zhongwenzimumianfeibofangc.org.cn</code>

<code>renqixiliezhongwenzimuc.org.cn</code>

<code>wuyefulizhiboc.org.cn</code>

<code>lalalazhongwendianshijuc.org.cn</code>

<code>yinghuadongmanguanfangbanc.org.cn</code>

## 项目结构

```text
rimanzaixian-hub/
├── config/                           # 配置文件目录
│   ├── urls.yaml                     # 核心 URL 索引表，含分类与备注
│   ├── probes.yaml                   # 探测参数配置（超时、重试、并发数）
│   └── alerts.yaml                   # 告警规则定义（阈值、通知目标）
├── src/                              # 源代码主目录
│   ├── probe.py                      # 主探测脚本，执行并发 HTTP 检查
│   ├── summary.py                    # 结果摘要生成器，输出统计信息
│   ├── exporter/                     # 导出器子模块
│   │   ├── json_exporter.py          # JSON 格式导出实现
│   │   └── csv_exporter.py           # CSV 表格导出实现
│   ├── notifier/                     # 通知子模块
│   │   ├── webhook.py                # HTTP Webhook 告警发送
│   │   └── logger.py                 # 本地日志记录器
│   └── utils/                        # 通用工具函数
│       ├── net.py                    # 网络探测底层封装（TCP/HTTP）
│       └── parser.py                 # YAML 配置解析辅助
├── reports/                          # 探测结果输出目录（自动生成）
│   ├── status.json                   # 最近一次探测完整报告
│   └── history/                      # 历史报告存档（按日期分目录）
├── tests/                            # 单元测试与集成测试用例
│   ├── test_probe.py                 # 探测模块测试
│   └── fixtures/                     # 测试用固定数据样本
├── requirements.txt                  # Python 依赖声明文件
├── setup.py                          # 项目安装脚本（pip install -e .）
├── CHANGELOG.md                      # 版本变更记录
├── LICENSE                           # MIT 许可证全文
└── README.md                         # 项目说明文档（本文件）
```

## 贡献指南

1. 在 GitHub 上 fork 本项目仓库至个人账号，然后 clone 到本地开发环境，确保基于最新的 main 分支进行开发。

2. 创建以 feature/ 或 fix/ 为前缀的语义化分支，例如 feature/add-tcp-probe，并在该分支上完成代码编写与本地测试，确保所有现有单元测试通过。

3. 更新对应文档，包括但不限于 config/ 目录下的 YAML 配置示例、docs/ 目录下的用户手册及 CHANGELOG.md 中的未发布变更条目。

4. 提交 pull request 至主仓库的 develop 分支，在请求描述中清晰说明改动目的、影响范围及测试覆盖情况，等待项目维护者代码审查。

5. 审查通过后，由维护者合并至 main 分支并打 tag 发布新版本。贡献者将自动列入项目贡献者列表（AUTHORS 文件）。

## 常见问题

**Q：项目是否提供对 URL 内容的缓存或代理转发功能？**

A：不提供。本项目仅执行轻量级 HTTP 探测（HEAD 请求为主，可选 GET 但不保存响应体），所有探测结果仅用于可用性判断与响应时间统计，不缓存任何页面内容，也不作为代理服务器转发请求。用户应遵守各目标站点的 robots.txt 及服务条款。

**Q：探测脚本的并发数与超时时间如何调整？**

A：所有可调参数均位于 config/probes.yaml 文件中。其中 concurrent 字段控制最大并发连接数，默认值为 10；timeout 字段控制单个请求的超时秒数，默认值为 5 秒。建议根据运行环境的网络状况和系统资源合理调整，避免过高并发导致源站压力或本地端口耗尽。

**Q：如何添加或移除索引中的 URL？**

A：直接编辑 config/urls.yaml 文件，按照既有的 YAML 列表格式添加或删除条目。每个条目包含 url（必填）、category（可选分类标签）、remarks（可选备注说明）。修改保存后，重新运行探测脚本即可生效。建议在修改前备份原始文件。

## 许可证

MIT License. 详见项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
