# ResourceBridge

ResourceBridge 是一个面向技术内容创作者与开发者的外链资源整合与导航工具。项目定位于解决个人或小型团队在项目文档、技术博客、社区内容中对外部优质资源引用分散、链接管理混乱、可用性难以追踪的问题。通过结构化元数据描述与自动化可访问性检查，ResourceBridge 帮助用户构建清晰、可控、可维护的外部资源引用体系，适用于技术文档站、开源项目 README 增强、以及知识库外链治理等场景。

ResourceBridge 不提供资源存储或代理服务，仅作为资源链接的整理、分类、状态监控与展示层。目标用户包括开源项目维护者、技术写作者、文档工程师以及需要频繁引用外部参考资料的技术团队。

## 功能概览

- **资源链接结构化录入**：支持按类别、标签、来源、状态等多维度描述外部链接，内置 YAML 与 JSON 两种导入导出格式。
- **自动化可用性检查**：每日定时检测所有已收录链接的 HTTP 状态码与响应时间，自动标记失效或响应超时的资源。
- **自定义资源分组展示**：支持按项目、按场景、按语言等多级分组生成静态导航页面或嵌入 Markdown 表格。
- **变更历史与回溯**：记录每次资源增删改的操作日志，支持回滚至任意历史版本。
- **链接关系图谱**：可视化展示资源之间的引用关系与依赖层级，辅助识别关键路径资源。
- **多格式导出适配器**：支持导出为 Markdown 列表、HTML 导航栏、JSON API 格式，便于集成至现有文档系统。
- **访问统计轻量埋点**：可选开启资源点击计数，帮助判断热门资源与低效资源。

## 应用场景

- **技术文档外链集中治理**：当技术文档中包含大量指向第三方规范、工具仓库、在线测试环境的链接时，可使用 ResourceBridge 统一管理这些链接，并在文档中统一引用 ResourceBridge 生成的链接标识，避免散落各处的硬编码链接难以维护。
- **开源项目 README 资源附录维护**：开源项目通常需要在 README 中列出相关资源、学习资料、社区渠道。ResourceBridge 可生成标准 Markdown 格式的资源列表，直接嵌入 README，并定时检查链接有效性，防止 README 中出现失效链接影响项目专业形象。
- **知识库外部参考资料整理**：团队内部知识库或个人技术笔记中经常引用外部文章、视频、工具站。ResourceBridge 提供分类与标签体系，帮助建立可检索的外部参考资料索引，并支持按场景快速筛选。
- **静态网站友情链接或推荐资源页**：个人技术博客或项目展示站需要展示友情链接或推荐工具时，ResourceBridge 可生成静态资源卡片页，支持自定义排序与样式模板，降低手动维护成本。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 克隆仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化配置与本地数据库
python scripts/init_db.py --config config/default.yaml

# 启动开发服务
python app.py --host 127.0.0.1 --port 8080
```

服务启动后，访问 http://127.0.0.1:8080 即可进入 ResourceBridge 仪表盘。默认管理员账号为 `admin`，初始密码在首次启动时打印于终端日志中，请及时修改。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.12 | 核心运行环境，推荐使用 3.11 |
| SQLite | 3.35.0 及以上 | 内置轻量数据库，用于存储资源元数据与检测记录 |
| Redis | 7.0 及以上 | 可选，用于缓存可用性检测结果与任务队列，生产环境建议启用 |
| Node.js | 18.x 及以上 | 仅用于前端静态资源构建，后端运行无需 |
| curl | 7.68 及以上 | 用于可用性检测模块的 HTTP 探活，系统自带 |
| git | 2.25 及以上 | 版本控制与自动更新检查依赖 |
| make | 3.81 及以上 | 用于执行构建脚本与测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting-started/ | 如何安装、配置、启动第一个资源导入任务 |
| 操作手册 | docs/user-guide/ | 如何批量导入链接、配置检测策略、生成导出文件 |
| 管理员指南 | docs/admin/ | 如何部署至生产环境、配置 Redis 缓存、设置定时任务 |
| API 参考 | docs/api/ | RESTful API 端点说明、请求与响应示例、鉴权方式 |
| 开发指南 | docs/development/ | 如何参与开发、代码规范、测试流程与 PR 要求 |
| 常见问题 | docs/faq/ | 收录社区高频问题及解决方案，持续更新 |

## 资源列表

本项目的资源导航模块收录了以下外部视频资源站点。所有资源链接均由用户提供，ResourceBridge 仅做展示与可用性跟踪，不涉及内容审查或存储。资源按类别划分如下：

中文视频字幕在线观看类：

<code>zhongwenzimuzaixianmianfeikanc.org.cn</code>

<code>zaixianshipinzhongwenzimuc.org.cn</code>

<code>zaixianbofangzhongwenzimuc.org.cn</code>

<code>zhongwenshipinzaixianguankanc.org.cn</code>

<code>shipinmianfeizaixianguankanc.org.cn</code>

日文视频与日韩双语类：

<code>rimanzaixianguankanc.org.cn</code>

<code>rihanzaixianmianfeishipinc.org.cn</code>

上述资源默认纳入 ResourceBridge 的示例数据集中，用户可在首次初始化时选择导入样例数据以快速体验功能。生产环境中建议替换或裁剪为项目自身的资源清单。

## 项目结构

```
resourcebridge/
├── app/                                 # 主应用模块
│   ├── __init__.py                      # 应用工厂与配置加载
│   ├── routes/                          # 路由层，处理 HTTP 请求分发
│   │   ├── api.py                       # RESTful API 端点
│   │   ├── dashboard.py                 # 管理后台页面路由
│   │   └── export.py                    # 导出格式路由
│   ├── models/                          # 数据模型与 ORM 定义
│   │   ├── resource.py                  # 资源实体模型
│   │   ├── check.py                     # 可用性检测记录模型
│   │   └── tag.py                       # 标签与分类模型
│   ├── services/                        # 业务逻辑层
│   │   ├── checker.py                   # 链接可用性检测服务
│   │   ├── exporter.py                  # 多格式导出服务
│   │   └── scheduler.py                 # 定时任务调度服务
│   └── utils/                           # 通用工具函数
│       ├── http.py                      # HTTP 请求与状态码处理
│       ├── logger.py                    # 日志配置与封装
│       └── validator.py                 # URL 校验与规范化
├── scripts/                             # 运维与初始化脚本
│   ├── init_db.py                       # 初始化数据库表与样例数据
│   ├── migrate.py                       # 数据库迁移工具
│   └── cron_check.sh                    # 外部 cron 调用的检测脚本
├── frontend/                            # 前端静态资源源码
│   ├── src/                             # Vue 3 组件与样式源码
│   ├── public/                          # 静态资源模板
│   └── build/                           # 构建配置文件
├── config/                              # 配置目录
│   ├── default.yaml                     # 默认配置项
│   ├── production.yaml                  # 生产环境覆盖配置
│   └── schema.yaml                      # 配置字段校验描述
├── tests/                               # 单元测试与集成测试
│   ├── unit/                            # 单模块测试用例
│   ├── integration/                     # 多模块联调测试
│   └── fixtures/                        # 测试固定数据集
├── docs/                                # 完整项目文档（详见文档导航）
├── requirements.txt                     # Python 依赖清单
├── Makefile                             # 构建与测试快捷命令
└── README.md                            # 项目入口文档（本文件）
```

## 贡献指南

1. 阅读项目行为准则与贡献者协议，确认遵守开源社区规范。所有贡献者需签署开发者原创声明，确保所提交代码无版权争议。
2. 在 GitHub Issues 中查找或创建与修改内容对应的问题编号，并等待维护者确认需求合理性，避免无效 PR。
3. 派生项目仓库至个人空间，基于 `develop` 分支创建功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式。
4. 完成代码或文档修改后，确保所有单元测试通过，并为新增功能补充测试用例与文档说明。提交信息需符合约定式提交规范。
5. 发起 Pull Request 至 `develop` 分支，描述修改目的、实现方式及测试情况。至少需要一位维护者审阅通过后方可合并。

## 常见问题

**问：ResourceBridge 是否会自动修改或删除我收录的外部链接内容？**

答：不会。ResourceBridge 仅存储用户提供的链接字符串及其元数据，不会对目标资源发起任何写操作，也不会代理或缓存资源内容。可用性检测模块仅执行 GET 请求获取状态码，不解析或存储响应体。

**问：可用性检测的请求频率和并发量是多少？是否会对目标站点造成压力？**

答：检测模块默认使用 5 秒超时、单线程顺序执行，每个链接每日最多检测一次。对于用户自定义添加的链接，检测间隔可配置为 6 小时至 7 天不等，同时支持配置 `rate_limit` 参数控制每秒最大请求数，默认值为每秒 2 个请求，以确保不对目标站点造成异常负载。

**问：如何将 ResourceBridge 生成的资源列表嵌入到我现有的 MkDocs 或 VuePress 站点中？**

答：ResourceBridge 支持导出为 Markdown 表格格式和 JSON 格式。您可通过管理后台的导出功能获取 Markdown 代码块，直接粘贴至 MkDocs 的 `.md` 文件中；对于 VuePress，可使用导出 API 获取 JSON 数据，并在前端组件中动态渲染。详细步骤请参考操作手册中的「导出与集成」章节。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:22
