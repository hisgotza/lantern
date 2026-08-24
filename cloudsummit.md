# VastLink Navigator

VastLink Navigator 是一个面向技术内容聚合与资源导航的开源工具集，定位于帮助开发者、技术写作人员与本地化运营团队高效管理、校验与展示分布式的多语言资源链接。项目解决的核心问题在于：当技术文档、多语言影视资料、开源教育内容分散在不同域名与协议下时，如何通过结构化方式统一收录、分类呈现，并提供基础的可用性检测与访问引导能力。

项目本身不存储任何第三方内容，仅提供链接元数据管理、分类索引生成与状态监控框架，适用于搭建个人或团队内部的技术资源导航站、多语言文档门户的链接底仓，或作为静态站点生成器的数据源插件。

## 功能概览

- **链接元数据登记**：支持记录 URL、来源站点、语言属性、内容类型与更新周期，形成结构化索引底表。

- **分类标签与全文检索**：内置标签系统，可按技术领域、语言种类、文件格式或机构来源进行筛选，并提供基于标题与描述的轻量级搜索。

- **可用性探测调度**：提供可配置的 HTTP/HTTPS 探活模块，支持超时设置、重试策略与状态快照记录，便于定期巡检外链有效性。

- **静态导航页生成**：内置模板引擎，可将索引数据渲染为纯 HTML 目录页，支持响应式布局与暗色模式，适合挂载至 GitHub Pages 或对象存储。

- **元数据导入导出**：支持 CSV、JSON 与 YAML 格式的批量导入导出，便于与现有文档工具链（如 MkDocs、VuePress）或电子表格软件对接。

- **变更审计日志**：记录每次链接新增、删除或字段修改的操作时间与操作人，便于多人协作时回溯历史状态。

- **协议与域名归一化校验**：自动检测 URL 是否缺失协议头或包含多余路径符，并根据规则给出标准化建议，降低人工录入错误。

## 应用场景

- **技术文档多语言版本管理**：当项目需要同时维护中、英、日等多语言版本文档时，可使用 VastLink Navigator 收录各语言部署地址，并统一生成语言切换导航栏，避免在多个仓库间手动同步链接。

- **开源教育视频资源索引**：社区运营人员可将定期发布的公开课录像、字幕文件与配套代码仓库地址录入系统，按季度或主题生成观看指南页面，供学习者快速定位所需资源。

- **内部工具链入口聚合**：中小型开发团队可将 CI/CD 面板、监控看板、日志平台、代码审查工具等内部系统的访问地址统一托管，配合可用性探测及时发现宕机或证书过期问题。

- **本地化翻译资产协同**：翻译协作团队可将术语表、翻译记忆库、风格指南等文档的云端存储链接集中管理，并为每个语种分配独立的访问路径，减少因链接分散造成的版本混淆。

## 快速开始

以下步骤帮助您在本地环境中快速启动 VastLink Navigator 的开发实例：

```bash
# 1. 克隆代码仓库
git clone https://github.com/example/vastlink-navigator.git
cd vastlink-navigator

# 2. 安装项目依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate   # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化示例数据并启动开发服务器
python scripts/init_db.py --sample-data
python app.py --host 127.0.0.1 --port 8080
```

启动后，在浏览器中访问 `http://127.0.0.1:8080` 即可查看默认导航界面，并可通过 `/admin` 路径进入管理后台进行数据操作。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，用于后端逻辑与调度任务 |
| SQLite | 3.35 及以上 | 默认元数据存储引擎，支持并发读取与基础事务 |
| Jinja2 | 3.1.x | 模板渲染引擎，用于生成静态导航页面 |
| requests | 2.31.x | HTTP 客户端库，用于链接可用性探测 |
| PyYAML | 6.0.x | YAML 格式解析与序列化，支持配置文件与导入导出 |
| pytest | 7.4.x | 单元测试框架，仅在开发环境中需要（非必须） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/quickstart.md` | 如何用示例数据快速体验核心功能？如何配置第一个数据源？ |
| 管理手册 | `docs/admin-guide.md` | 如何管理链接字段、自定义分类标签？如何查看探测历史？ |
| 模板定制 | `docs/template-custom.md` | 如何修改导航页的样式与布局？如何添加自定义 CSS 或 JavaScript？ |
| 部署运维 | `docs/deployment.md` | 如何将系统部署至生产环境？支持哪些 Web 服务器网关接口？ |

## 资源列表

### 影视与教育资源（中文）

- <code>renqixiliezhongwenzimuf.org.cn</code>
- <code>wuyefulizhibof.org.cn</code>
- <code>lalalazhongwendianshijuf.org.cn</code>
- <code>yinghuadongmanguanfangbanf.org.cn</code>
- <code>zhongwenzimuyongjiuzaixianf.org.cn</code>
- <code>mianfeizhuijuwangzhanf.org.cn</code>
- <code>gaoqingzhongwenzimuf.org.cn</code>

## 项目结构

```
vastlink-navigator/
├── app.py                     # 应用入口，注册路由与启动服务
├── config.yaml                # 全局配置文件（端口、探测间隔、日志级别）
├── requirements.txt           # Python 依赖清单
├── README.md                  # 项目说明文档（本文件）
├── LICENSE                    # MIT 许可证文本
│
├── core/                      # 核心业务逻辑层
│   ├── __init__.py
│   ├── registry.py            # 链接注册、去重与字段校验
│   ├── probe.py               # 可用性探测调度器与结果存储
│   └── exporter.py            # 数据导出为 CSV/JSON/YAML
│
├── web/                       # Web 界面与 API 层
│   ├── routes/                # 路由分组（首页、管理、静态生成）
│   ├── templates/             # Jinja2 模板文件（布局、列表、详情）
│   ├── static/                # 静态资源（CSS、JS、图标）
│   └── forms/                 # WTForms 表单定义（新增、编辑、筛选）
│
├── scripts/                   # 运维与工具脚本
│   ├── init_db.py             # 初始化数据库表结构
│   ├── import_data.py         # 从外部文件批量导入链接
│   └── scheduled_probe.py     # 定时探测任务（可配合 cron 调用）
│
├── tests/                     # 单元测试与集成测试
│   ├── test_registry.py
│   ├── test_probe.py
│   └── fixtures/              # 测试用示例数据文件
│
└── docs/                      # 用户文档与开发者文档
    ├── quickstart.md
    ├── admin-guide.md
    ├── template-custom.md
    └── deployment.md
```

## 贡献指南

1. 从主线仓库派生（Fork）项目至个人账户，并克隆派生仓库到本地开发环境。建议在新建分支上开展工作，分支命名遵循 `feature/功能简述` 或 `fix/问题简述` 格式。

2. 运行 `scripts/init_db.py` 初始化测试数据库，并执行 `pytest tests/` 确认现有测试全部通过。新增功能时，请同步补充对应的单元测试用例，覆盖核心逻辑的异常分支。

3. 提交代码前，使用 `black` 与 `flake8` 进行代码格式统一与静态检查。提交信息（commit message）应使用清晰英文描述变更意图，例如 `Add retry policy for probe timeout`。

4. 推送到派生仓库后，通过 GitHub 界面发起 Pull Request 到主仓库的 `main` 分支。PR 描述中需说明变更动机、实现方式以及是否影响现有接口兼容性。

5. 项目维护者将在 3 个工作日内进行 Code Review，可能要求补充测试或调整接口细节。合并后，相关变更将进入下一个版本发布计划。

## 常见问题

**问：项目是否提供在线演示站点？**

当前版本未提供公开演示实例，但您可按照快速开始步骤在本地完全运行。若希望快速预览导航页面效果，可使用 `scripts/init_db.py --sample-data` 加载内置的示例链接集合，无需额外配置。

**问：可用性探测是否会频繁访问目标站点，导致被屏蔽？**

探测模块默认采用单线程顺序执行，且每轮探测间隔不低于 60 分钟。用户可在 `config.yaml` 中调整 `probe_interval` 与 `timeout` 参数。对于高频访问风险，建议将探测源 IP 固定，并在目标站点允许的 User-Agent 白名单中增加标识。

**问：如何迁移 SQLite 数据库至生产级数据库？**

项目使用 SQLAlchemy ORM 作为数据库抽象层，您只需在 `config.yaml` 中修改 `database_url` 连接串为 PostgreSQL 或 MySQL 的 DSN 格式，并在 `core/registry.py` 中调整部分字段类型映射（如 JSON 字段）。迁移前请确保目标数据库已创建，且已安装对应的方言驱动（如 `psycopg2` 或 `pymysql`）。

## 许可证

MIT License。允许自由使用、修改、分发，但需保留版权声明与许可声明。详细信息请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
