# ResourceBridge

ResourceBridge 是一个面向开发人员与技术研究者的外链资源聚合与导航系统。项目定位为高质量技术资源的中转枢纽，通过人工筛选与自动化检测相结合的方式，汇集全球范围内有价值的开发文档、学术镜像、工具站点与开放数据源。项目目标用户包括软件工程师、数据科学家、运维人员以及计算机相关领域的研究生。ResourceBridge 本身不存储任何版权内容，仅提供公开资源的链接索引与可用性状态监测，解决开发者在信息检索过程中面临的海量低质内容过滤困难、资源失效频繁、跨语言访问不便等实际问题。

## 功能概览

- **外链可用性实时检测**：对收录的每一个资源链接进行周期性 HTTP 状态码与响应时间监测，自动标记异常链接并生成告警通知。

- **多维度分类与标签系统**：支持按资源类型、语种、所属领域、更新频率等维度进行精细化分类，提供组合筛选与全文检索能力。

- **自定义收藏与私有集合**：允许注册用户创建个人收藏夹和主题集合，支持集合的公开分享与协作维护。

- **资源变更历史追踪**：记录每个收录链接的标题、描述、证书信息及页面结构变更，提供时间线回溯与变更对比视图。

- **批量导入与 API 集成**：提供 RESTful API 接口，支持第三方工具批量导入链接列表，并支持通过 Webhook 接收可用性状态变更事件。

- **访问统计与热度排序**：基于内部点击数据和外部反链分析，生成资源访问热度排行与趋势图表，辅助用户发现近期热门工具。

- **黑暗模式与阅读优化**：前端界面内置黑暗模式切换，并对长文本描述区域进行排版优化，提升长时间阅读的舒适度。

## 应用场景

- **技术选型阶段的资料收集**：架构师或技术负责人进行新项目技术选型时，可通过 ResourceBridge 快速查阅多个官方文档站点、性能对比报告和社区讨论帖的链接，避免在搜索引擎中反复试错。

- **离线开发环境的知识库搭建**：内网隔离环境下的开发团队可将 ResourceBridge 部署为内部导航页，统一收录内部 Wiki、代码仓库、CI/CD 控制台和监控面板地址，解决多服务入口分散的问题。

- **学术研究中的数据集查找**：数据科学方向的研究人员通过资源分类筛选功能，快速定位开放数据集索引站点、学术论文预印本镜像和标准化测试集下载地址，节省跨平台检索时间。

- **运维故障排查时的工具导航**：系统运维人员在大规模故障处理期间，通过 ResourceBridge 快速跳转至日志分析平台、链路追踪 UI、云服务商状态页和社区应急方案讨论帖，提升应急响应效率。

## 快速开始

以下操作步骤适用于 Linux / macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 第一步：克隆代码仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 第二步：安装项目依赖（使用 pipenv 或 poetry）
pip install pipenv
pipenv install --deploy --ignore-pipfile
# 若使用 poetry，执行：poetry install --no-dev

# 第三步：初始化配置文件并启动开发服务
cp .env.example .env
# 编辑 .env 文件，填写数据库连接字符串与检测参数
pipenv run python manage.py migrate
pipenv run python manage.py runserver --host=0.0.0.0 --port=8080
```

生产环境部署请参考 `docs/deployment.md`，建议使用 Gunicorn + Nginx 组合。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高版本 | 核心运行时，低于 3.10 将导致类型注解解析错误 |
| PostgreSQL | 14.x 或更高版本 | 主数据库，用于存储资源元数据、用户信息及检测历史 |
| Redis | 7.x 或更高版本 | 缓存与会话存储，同时用作 Celery 的消息代理 |
| Node.js | 20.x LTS 或更高版本 | 仅用于前端静态资源构建，后端运行时无需 |
| Nginx | 1.24 或更高版本 | 生产环境推荐反向代理，用于负载分发与静态文件缓存 |
| Celery Worker | 5.x 版本 | 独立进程，负责执行定时检测与异步任务，需与主服务分离部署 |
| Supervisor | 4.x 版本 | 用于生产环境进程守护，确保 Celery 与 Gunicorn 持续运行 |

## 文档导航

| 层面 | 目录路径 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/user-guide/` | 如何注册账号、创建收藏集、使用筛选与检索功能、配置个人通知偏好 |
| 管理员指南 | `docs/admin-guide/` | 如何审核新提交的链接、管理分类标签、调整检测频率与告警阈值 |
| API 参考 | `docs/api-reference/` | 所有 RESTful 接口的请求参数、响应结构、认证方式与错误码含义 |
| 部署运维 | `docs/deployment/` | 生产环境安装步骤、环境变量完整列表、容器化部署方案与监控指标配置 |
| 贡献者指引 | `CONTRIBUTING.md` | 代码风格规范、提交信息格式、PR 流程与测试用例编写要求 |

## 资源列表

本列表汇总当前版本内置的初始资源索引，按类别分组展示。用户亦可自行添加或移除链接。

**视频播放与字幕辅助类**

- <code>zaixianbofangnidongdea.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikanb.org.cn</code>
- <code>zaixianshipinzhongwenzimub.org.cn</code>
- <code>zaixianbofangzhongwenzimub.org.cn</code>
- <code>zhongwenshipinzaixianguankanb.org.cn</code>
- <code>shipinmianfeizaixianguankanb.org.cn</code>
- <code>rimanzaixianguankanb.org.cn</code>

## 项目结构

```text
resourcebridge/
├── backend/                        # 后端核心代码目录
│   ├── api/                        # RESTful API 路由与视图函数 (v1/v2)
│   ├── core/                       # 核心业务逻辑：资源检测、分类、收藏管理
│   ├── models/                     # SQLAlchemy ORM 模型定义 (User, Resource, Tag, DetectionLog)
│   ├── schemas/                    # Pydantic 请求/响应数据校验模型
│   ├── tasks/                      # Celery 异步任务定义 (检测、邮件、清理)
│   └── utils/                      # 工具函数：HTTP 客户端、缓存装饰器、日志配置
├── frontend/                       # 前端单页应用源码
│   ├── src/
│   │   ├── components/             # Vue 组件库 (导航栏、资源卡片、筛选面板、收藏按钮)
│   │   ├── views/                  # 页面级组件 (首页、详情页、个人中心、管理后台)
│   │   ├── stores/                 # Pinia 状态管理 (用户认证、收藏状态、主题模式)
│   │   └── styles/                 # 全局主题变量与暗色模式覆盖样式
│   └── static/                     # 构建后输出的静态资源目录
├── scripts/                        # 运维辅助脚本
│   ├── init_db.sql                 # 数据库初始化 SQL 脚本
│   ├── seed_links.py               # 批量导入初始链接列表的数据填充脚本
│   └── health_check.sh             # 系统健康状态检查脚本 (供监控系统调用)
├── docs/                           # 完整文档目录 (用户手册、管理员指南、API 参考、部署方案)
├── tests/                          # 单元测试与集成测试用例
│   ├── unit/                       # 针对 models / schemas / utils 的单元测试
│   └── integration/                # API 接口端到端测试与 Celery 任务模拟测试
├── docker-compose.yml              # 本地开发与测试环境容器编排文件
├── Dockerfile                      # 后端服务多阶段构建镜像描述文件
├── requirements.txt                # Python 生产依赖列表 (锁定版本)
├── requirements-dev.txt            # Python 开发额外依赖 (pytest, flake8, black)
├── .env.example                    # 环境变量配置模板 (含数据库、Redis、邮件服务、检测超时)
└── pyproject.toml                  # 项目元数据、构建系统与工具链配置 (black, isort)
```

## 贡献指南

1. **分支管理**：从 `develop` 分支切出新功能分支，命名格式为 `feature/功能简述` 或 `fix/问题简述`。禁止直接向 `main` 或 `develop` 提交代码。

2. **代码规范**：后端代码必须通过 `flake8` 与 `black` 检查，前端代码需通过 `eslint` 与 `prettier` 格式化。所有新增 API 接口须附带 `pytest` 单元测试，覆盖率不低于 80%。

3. **提交信息格式**：采用 Conventional Commits 规范，即 `<type>(<scope>): <subject>`，例如 `feat(detector): add TCP timeout retry mechanism`。提交内容应清晰描述变更意图，避免模糊表达。

4. **Pull Request 流程**：提交 PR 前请先同步上游 `develop` 分支的最新变更，解决所有冲突。PR 描述中需附上测试结果截图或日志，并至少获得一名维护者的 Approve。

5. **文档更新**：任何涉及接口变更、配置项增减或部署步骤调整的 PR，必须同步更新 `docs/` 目录下的对应文档文件，否则不予合并。

## 常见问题

**问：ResourceBridge 自身是否会缓存或代理外部资源的内容？**

答：不会。ResourceBridge 仅存储资源的元数据（标题、描述、URL、分类标签）以及可用性检测的状态记录（HTTP 状态码、响应时间、最后检测时间）。所有对外部资源的访问均通过用户浏览器直接发起，服务端不进行任何内容缓存、转码或代理转发，完全遵守 robots.txt 协议。

**问：可用性检测是否会对我自己的网站造成过大请求压力？**

答：默认检测频率为每 24 小时一次，且检测请求头中包含 `User-Agent: ResourceBridge-HealthCheck/1.0` 以及 `X-ResourceBridge-ID` 标识，方便网站管理员识别并屏蔽。检测超时时间设置为 5 秒，并启用指数退避重试策略（最多重试 2 次），避免在网络抖动时产生无效重试流量。

**问：如何将私有部署的数据迁移至另一台服务器？**

答：官方提供 `pg_dump` / `pg_restore` 配合 Redis RDB 持久化文件的迁移方案。详细步骤见 `docs/deployment/migration.md`。对于 Docker 部署环境，可直接备份 `postgres_data` 和 `redis_data` 两个卷目录，在新服务器上挂载相同路径并恢复容器即可。

## 许可证

MIT License

Copyright (c) 2026 ResourceBridge Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
