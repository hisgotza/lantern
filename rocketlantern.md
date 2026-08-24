# NexusIndex

NexusIndex 是一个面向技术社区与开源开发者的轻量级外链资源聚合与导航系统。项目定位为“可信技术入口”，通过人工筛选与社区投票机制，将高频使用的开发文档、学习资料、工具站点与娱乐资源以结构化目录形式呈现，帮助开发者减少信息检索损耗，提升工作流切换效率。NexusIndex 不存储任何实体内容，仅作为 URL 元数据索引层，适用于个人开发者、技术团队及教育机构搭建内部或公开的技术资源导航站。

## 功能概览

- **多级分类索引**：支持按技术领域、资源类型、适用人群进行三层分类过滤，快速定位目标链接。
- **社区热度排序**：基于点击量、收藏数与社区投票综合计算资源热度，自动生成“本周热门”与“长期经典”榜单。
- **自定义标签系统**：用户可为任意链接添加自定义标签，实现个人化的资源分组与快速召回。
- **链接健康检测**：每日自动检测索引链接的可达性，标记失效链接并发送告警通知。
- **快速导入导出**：支持批量导入 URL 列表（CSV/JSON 格式），并支持导出为 Markdown 或 HTML 书签文件。
- **暗色主题与阅读模式**：内置两套视觉主题，并为文档类链接提供专注阅读模式，屏蔽侧边栏干扰。
- **RSS 订阅源生成**：为每个分类目录生成独立 RSS 订阅地址，方便用户通过阅读器跟踪更新。
- **访问统计看板**：提供轻量级仪表盘，展示总链接数、分类覆盖度、日活跃用户数等关键指标。

## 应用场景

- **个人开发环境起始页**：开发者可将 NexusIndex 设为浏览器新标签页，集中存放常用 API 文档、组件库与调试工具，每日开工一键抵达。
- **团队内部知识库导航**：技术团队可将私有部署的 NexusIndex 作为团队文档入口，统一存放设计规范、接口契约、运维手册与项目周报链接。
- **开源社区共建导航**：开源项目维护者可将项目相关的生态链接（如贡献指南、讨论区、CI 状态、版本发布记录）聚合为子目录，降低新贡献者的上手成本。
- **技术培训机构辅助教学**：讲师可提前将课程所需的在线实验环境、视频教程与代码仓库导入系统，学生通过统一入口访问，避免因拼写错误导致的教学中断。
- **极简信息收集站**：研究人员可将分散在多个平台的行业报告、数据看板与新闻资讯通过 NexusIndex 聚合，形成个人化的信息中继枢纽。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，帮助您在五分钟内启动本地开发实例。

```bash
# 克隆仓库
git clone https://github.com/nexus-index/nexusindex.git
cd nexusindex

# 安装依赖（使用 pip 与虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 初始化数据库并导入预置示例数据
python manage.py migrate
python manage.py loaddata fixtures/initial_links.json

# 启动开发服务器
python manage.py runserver 0.0.0.0:8000
```

启动后，访问 `http://localhost:8000` 即可进入 NexusIndex 首页。默认管理员账号为 `admin`，密码在首次启动时由系统随机生成并打印在终端日志中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.11 | 核心运行环境，3.12 暂不支持部分依赖库 |
| PostgreSQL | 13.0 及以上 | 生产环境推荐使用，开发环境可换用 SQLite |
| Redis | 6.2 及以上 | 用于缓存热点链接与临时存储会话数据 |
| Node.js | 18.x LTS | 仅用于前端资源构建（Webpack 与 Sass） |
| Nginx | 1.20 及以上 | 生产环境反向代理与静态资源服务（可选） |
| Supervisor | 4.2 及以上 | 进程守护工具，用于保持 Celery 后台任务稳定（可选） |
| Celery | 5.2 及以上 | 异步执行链接健康检测与统计更新任务 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | `/docs/quick-start/` | 如何快速部署、初始化管理员账户、导入第一批链接 |
| 运维手册 | `/docs/operations/` | 如何进行备份、迁移、日志轮转与性能调优 |
| API 参考 | `/docs/api/` | 如何通过 RESTful API 增删改查链接、分类与标签 |
| 自定义开发 | `/docs/development/` | 如何扩展新的检测器、编写插件或修改前端主题 |
| 安全策略 | `/docs/security/` | 如何配置访问控制、HTTPS 强制与防止 XSS 注入 |
| 社区治理 | `/docs/governance/` | 如何参与投票、申请新增资源目录及争议解决流程 |

## 资源列表

本系统聚合的外部资源按主题分组展示，所有链接均来自用户原始数据，未经任何格式修改。

**影视与娱乐类**

- <code>zaixianbofangnidongdef.org.cn</code>
- <code>jiureshipinzaixianguankan.org.cn</code>
- <code>renqizhongwenzimusiwa.org.cn</code>

**图像与设计类**

- <code>guomotaotu.org.cn</code>
- <code>guomosipaishipin.org.cn</code>

**综合资讯与门户类**

- <code>hanmanguanfangmianfeirukou.org.cn</code>
- <code>meinvwangzhanmianfeikan.org.cn</code>

## 项目结构

```
nexusindex/
├── .github/                         # GitHub 社区模板与 CI 流水线
│   ├── workflows/                   # 测试、构建、部署工作流定义
│   └── ISSUE_TEMPLATE/              # 问题与功能请求模板
├── backend/                         # Django 后端核心代码
│   ├── apps/                        # 模块化应用目录
│   │   ├── core/                    # 基础模型、抽象类与全局工具
│   │   ├── links/                   # 链接增删改查、分类、标签业务逻辑
│   │   ├── stats/                   # 点击统计、热度计算与看板数据
│   │   └── health/                  # 链接可达性检测与告警服务
│   ├── settings/                    # 多环境配置（开发、测试、生产）
│   ├── urls/                        # 根路由分发与 API 版本控制
│   └── wsgi.py / asgi.py            # 部署入口文件
├── frontend/                        # 前端 Vue 3 单页应用
│   ├── src/
│   │   ├── components/              # 可复用 UI 组件（卡片、导航、表格）
│   │   ├── views/                   # 页面级视图（首页、分类页、详情页）
│   │   ├── store/                   # Pinia 状态管理（用户偏好、缓存）
│   │   └── assets/                  # 静态资源（主题变量、字体、图标）
│   └── dist/                        # 构建输出目录（生产环境静态资源）
├── scripts/                         # 运维辅助脚本
│   ├── backup_db.sh                 # 数据库定时备份脚本
│   ├── import_links.py              # 批量导入外部链接命令行工具
│   └── health_check_runner.py       # 手动触发链接检测的独立脚本
├── docs/                            # 完整文档源文件（Markdown + Mermaid）
├── logs/                            # 应用日志存储目录（按天切割）
├── docker-compose.yml               # 本地开发与测试环境容器编排
├── Dockerfile                       # 多阶段构建镜像定义
├── requirements.txt                 # Python 依赖清单
├── package.json                     # 前端依赖与构建脚本
├── pytest.ini                       # 单元测试配置
└── README.md                        # 本文件
```

## 贡献指南

我们欢迎各类贡献，包括但不限于新增资源链接、修复前端样式缺陷、优化检测算法或完善文档。请遵循以下流程：

1. **查阅现有议题**：前往 GitHub Issues 搜索是否已有类似提议或待修复问题，避免重复劳动。若无相关议题，请新建一个并简要说明您的改进方向。
2. **派生仓库并创建分支**：将主仓库 Fork 至您的账号下，基于 `develop` 分支新建您的功能分支，分支命名采用 `feat/描述` 或 `fix/描述` 格式。
3. **编写或调整代码**：请遵守项目现有编码规范（Python 遵循 PEP 8，前端遵循 Prettier 默认规则）。对于新增链接，请务必提供官方来源说明或社区推荐理由。
4. **补充单元测试与文档**：所有新增函数或 API 端点需附带对应测试用例；若影响用户界面，请同步更新文档中的相关截图或操作描述。
5. **发起合并请求**：向主仓库的 `develop` 分支发起 Pull Request，并在描述中关联对应议题编号。项目维护者将在三个工作日内进行 Code Review，并给出合并或修改建议。

## 常见问题

**Q：NexusIndex 是否存储任何视频、图片或文档文件？**

A：否。NexusIndex 仅存储链接元数据（标题、分类、标签、描述与 URL 字符串），不缓存或代理任何外部资源。所有访问行为均直接重定向至原始地址，用户需自行遵守目标站点的使用条款。

**Q：如何迁移生产环境的数据库到新服务器？**

A：首先在源服务器执行 `python manage.py dumpdata --exclude auth.permission > backup.json` 导出数据（不含系统权限表避免冲突），然后将该文件传输至目标服务器，执行 `python manage.py loaddata backup.json` 即可。注意需保证 PostgreSQL 版本一致，并提前迁移表结构。

**Q：链接健康检测误报怎么办？**

A：检测器默认使用 HEAD 请求并设置 5 秒超时，部分站点可能拒绝 HEAD 请求或响应较慢。您可在管理后台将特定链接加入“检测白名单”，或调整 `HEALTH_CHECK_TIMEOUT` 环境变量（单位秒）。我们建议结合人工复核与自动检测结果，避免完全依赖自动化判定。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
