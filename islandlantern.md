# NexusIndex

NexusIndex 是一个面向开发者与技术研究人员的轻量级外链资源导航系统，旨在解决技术社区中优质外部资源分散、链接失效快、检索成本高的问题。项目本身不存储任何实际内容，仅提供结构化索引与健康度监测，帮助团队或个人快速定位可用的一手资源节点。NexusIndex 适用于需要高频访问特定垂直领域资源的技术小组、开源项目文档站或内部知识库的外链治理场景。

## 功能概览

- **多源外链聚合管理**：支持将散落在各处的技术文档、社区帖子、数据源链接统一收录，并按自定义标签分类，减少上下文切换成本。
- **被动健康检查**：内置简易链接探活机制，可定期检测收录 URL 的可访问性，并在仪表盘标注异常状态，辅助维护者及时清理失效节点。
- **按需导出视图**：允许用户根据场景筛选链接子集，生成纯文本或 Markdown 格式的清单，便于嵌入 README、Wiki 或自动化脚本。
- **标签与全文检索**：为每个外链附加描述性标签与简短备注，支持基于关键词的快速过滤，提升海量链接中的查找效率。
- **访问统计快照**：记录每个外链的点击次数与最近访问时间，帮助团队识别高频使用资源，为链接优先级排序提供数据参考。
- **只读只写分离**：管理后台与前台展示分离，普通访客仅可见经过审核的已发布链接，维护者通过简易命令行工具或配置文件批量更新。
- **零外部依赖的前端渲染**：展示层使用原生 HTML 与 CSS，无需构建工具即可运行，兼容低版本浏览器，适合内网或受限网络环境部署。

## 应用场景

- **技术文档站外链治理**：开源项目维护者可将分散在 Issues、PR 评论、外部博客中的参考链接集中收录于 NexusIndex，避免文档正文因链接变更频繁修改。
- **数据采集管道资源登记**：数据工程团队可将常用公开数据源、API 网关地址、备份存储桶路径登记为外链，并通过健康检查预警源站宕机。
- **社区精选内容月刊**：技术社区运营人员可利用标签与导出功能，定期整理当周热门讨论帖、视频教程或工具站链接，生成纯文本月刊素材。
- **内部知识库快速导航**：企业技术部门可将内部 Jenkins、GitLab、SonarQube、监控大盘等内部系统入口统一纳管，新员工入职时一键导入浏览器书签。
- **离线文档辅助索引**：配合 HTTrack 或 wget 将外链指向的静态文档镜像至本地，NexusIndex 可作为镜像站的入口目录，清晰标注每个镜像的更新日期。

## 快速开始

以下步骤演示在 Linux/macOS 环境下从源码启动 NexusIndex 服务。

```bash
# 克隆项目仓库
git clone https://github.com/nexusindex/nexusindex.git
cd nexusindex

# 安装依赖（Python 3.9+ 与 pip）
pip install -r requirements.txt

# 初始化数据库并导入示例外链数据
python manage.py initdb
python manage.py import --source samples/links.yaml

# 启动本地开发服务器（默认监听 127.0.0.1:8080）
python manage.py runserver
```

启动后，在浏览器中访问 <code>http://127.0.0.1:8080</code> 即可查看前端展示页。如需管理后台，请访问 <code>http://127.0.0.1:8080/admin</code> 并使用初始管理员账户（admin / changeme）登录，首次登录后强制修改密码。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.12 | 核心运行环境，用于后端 API 与调度任务 |
| SQLite | 3.31+ | 内置轻量数据库，存储外链元数据与访问日志 |
| pip | 21.0+ | Python 包管理工具，用于安装第三方库 |
| git | 2.25+ | 克隆仓库与版本管理，非运行时强制依赖 |
| 操作系统 | Linux / macOS / Windows WSL2 | 生产环境推荐 Debian 11 或 Ubuntu 20.04 LTS |
| 内存 | 最低 512 MB | 单实例并发小于 50 时适用，推荐 1 GB |
| 存储 | 最低 200 MB 可用空间 | 用于存放数据库文件及日志，SQLite 默认容量限制内 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide.md | 如何添加、编辑、删除外链？如何批量导入 YAML 文件？ |
| 运维指南 | /docs/operations.md | 如何配置健康检查间隔？如何备份 SQLite 数据库？如何迁移至 PostgreSQL？ |
| API 参考 | /docs/api-reference.md | 提供哪些 RESTful 接口？如何通过 token 认证？分页参数如何设置？ |
| 开发规范 | /docs/development.md | 代码目录结构说明、测试用例如何编写、提交 PR 的流程是什么？ |
| 部署示例 | /docs/deployment-examples.md | 提供 systemd 单元文件、Dockerfile 以及 Nginx 反向代理配置片段 |
| 常见工作流 | /docs/workflows.md | 如何结合 GitHub Actions 自动检测外链有效性？如何定时生成统计报表？ |

## 资源列表

本项目的收录资源均来源于公开网络，NexusIndex 仅作为索引中介，不对链接指向的内容负责。所有链接按主题整理如下。

**视频与媒体类资源**

<code>hanshicaoshipinzaixianguankan.net.cn</code>

<code>mianfeizipaishipin.net.cn</code>

<code>diguashipin.net.cn</code>

<code>chengzishipin.net.cn</code>

**漫画与图文类资源**

<code>xiuxiumanhuaw.net.cn</code>

<code>meinvmanhua.net.cn</code>

<code>xiuxiumanhuazaixianguankan.net.cn</code>

> 注：上述链接按用户原始数据原样收录，未做任何格式修改，包括协议前缀与域名大小写。NexusIndex 不保证链接的长期有效性，建议使用者自行配置健康检查规则。

## 项目结构

```
nexusindex/
├── manage.py                 # 项目统一入口，包含 initdb、import、runserver 等子命令
├── requirements.txt          # Python 依赖清单（Flask、requests、pyyaml 等）
├── config/
│   ├── settings.py           # 应用配置（端口、调试模式、数据库路径）
│   └── logging.conf          # 日志级别与输出格式配置
├── core/
│   ├── __init__.py
│   ├── database.py           # SQLite 连接池与表结构初始化
│   ├── models.py             # 外链接、标签、访问日志的 ORM 映射
│   ├── health_check.py       # 异步链接探活任务（基于 requests 与超时重试）
│   └── importer.py           # YAML/JSON 批量导入解析器
├── web/
│   ├── __init__.py
│   ├── app.py                # Flask 应用工厂，注册蓝图与错误处理器
│   ├── routes/
│   │   ├── frontend.py       # 前端展示路由（首页、详情、搜索）
│   │   └── admin.py          # 管理后台路由（增删改、批量操作）
│   └── templates/            # Jinja2 模板文件（base.html, index.html, admin.html）
├── static/
│   ├── style.css             # 无框架纯 CSS 样式，支持暗色主题
│   └── script.js             # 前端交互（过滤、分页、点击计数异步上报）
├── samples/
│   └── links.yaml            # 示例外链数据文件，展示标签与字段格式
├── tests/
│   ├── test_models.py        # 模型层单元测试
│   ├── test_health.py        # 健康检查逻辑测试（使用 mock 避免真实网络请求）
│   └── test_importer.py      # 导入器边界条件测试
└── docs/                     # 详细文档目录，与文档导航章节对应
    ├── user-guide.md
    ├── operations.md
    ├── api-reference.md
    ├── development.md
    ├── deployment-examples.md
    └── workflows.md
```

## 贡献指南

1. **查阅现有 Issue 与 Project Board**：访问 GitHub Issues 页面，确认待解决的问题或功能请求，避免重复工作。对于新功能建议，请先创建一个讨论性 Issue 并获得维护者反馈。

2. **派生仓库并创建功能分支**：将主仓库 fork 至个人账户，然后基于 `main` 分支创建命名清晰的功能分支，例如 `feat/add-batch-tag-editor` 或 `fix/health-check-timeout`。

3. **编写或更新测试用例**：所有新功能或修复必须附带对应的单元测试或集成测试，确保测试覆盖率为新增代码的 80% 以上。运行 `pytest tests/` 验证本地无回归。

4. **遵循代码风格与提交规范**：Python 代码需符合 PEP 8 规范，使用 `black` 与 `flake8` 进行格式化与检查。提交信息采用 Conventional Commits 格式，如 `feat: 增加按标签筛选的 API 参数`。

5. **发起 Pull Request 并参与评审**：将功能分支推送至个人派生仓库，然后向主仓库的 `main` 分支发起 PR。PR 描述中需清晰说明变更动机、实现方式以及测试结果。维护者将在 3 个工作日内给出评审意见。

## 常见问题

**Q1：如何迁移 SQLite 数据库至生产级 PostgreSQL 或 MySQL？**

A：NexusIndex 使用 SQLAlchemy ORM，理论上支持多数据库后端。迁移时，请先修改 `config/settings.py` 中的 `SQLALCHEMY_DATABASE_URI` 为对应连接串，然后运行 `python manage.py db upgrade` 自动生成表结构。注意 SQLite 与其他数据库在布尔类型、默认值上存在细微差异，建议使用 `alembic` 生成迁移脚本前仔细校验模型定义。若数据量较大，可借助 `pgloader` 或 `mysqldump` 等工具进行离线迁移。

**Q2：健康检查任务会影响前端响应速度吗？**

A：健康检查采用独立线程池异步执行，默认间隔为 12 小时，单次任务超时设置为 5 秒。检查结果写入数据库的独立状态字段，前端访问时仅读取该缓存值，不会触发实时探测。若部署环境网络质量较差，可通过 `config/settings.py` 中的 `CHECK_TIMEOUT` 和 `CHECK_CONCURRENCY` 调节超时时间与并发数，避免资源耗尽。

**Q3：能否将 NexusIndex 部署为无状态服务，以支持多实例横向扩展？**

A：可以。默认 SQLite 为文件锁模式，不适合多进程并发写入，但可以通过将数据库更换为 PostgreSQL 或 MySQL 实现多实例共享数据。同时，需将会话存储切换至 Redis（通过 Flask-Session 扩展），并确保静态文件由 CDN 或 Nginx 代理，各实例自身不保存本地文件缓存。官方提供了一份 `docker-compose.yml` 示例，包含 Nginx 负载均衡、PostgreSQL 和 Redis 容器编排，详见 `/docs/deployment-examples.md`。

## 许可证

MIT License

Copyright (c) 2026 NexusIndex Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
