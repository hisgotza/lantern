# HyperLink Hub

HyperLink Hub 是一个面向技术内容创作者、开源项目维护者以及网络资源整理者的外链资源聚合与导航系统。该项目旨在解决分散的网络资源难以系统化管理、检索与共享的问题，通过标准化的外链收录机制、分类标签体系以及状态监控能力，为用户提供一个轻量级、可自托管的资源目录中枢。项目本身不生产内容，而是专注于提供高质量外部资源的结构化引用与健康度追踪，适用于个人知识库构建、团队技术文档外链整合以及社区资源导航站建设。

## 功能概览

- **资源条目化管理**：支持对外链资源进行标题、描述、分类、标签、状态等多维度字段录入与编辑，所有数据存储于本地 SQLite 数据库中，便于备份与迁移。
- **自动可用性探测**：集成异步 HTTP 健康检查模块，可定期对已收录的域名或 URL 发起请求，自动标记可访问性状态（正常/异常/超时），辅助维护者清理失效链接。
- **分类与标签过滤系统**：采用多级分类与自由标签双轨制，允许用户按技术领域（如前端、运维、AI）、资源类型（文档、工具、社区）或自定义关键词快速筛选目标资源。
- **全文检索支持**：基于 SQLite FTS5 扩展实现资源标题与描述的全文索引，支持中文分词与模糊匹配，提升查找效率。
- **导入与导出机制**：提供 CSV 与 JSON 格式的批量导入导出接口，便于与其他工具（如 Notion、Airtable、浏览器书签）进行数据交换。
- **RESTful API 接口**：所有核心操作均通过 JSON API 暴露，方便与其他内部系统或自动化脚本集成，无需依赖图形界面即可完成资源增删改查。
- **静态站点生成模式**：内置模板引擎，可根据当前数据库内容一键生成纯静态 HTML 导航页面，适合部署至 Nginx、GitHub Pages 或对象存储服务，降低公开访问成本。

## 应用场景

1.  **开源项目文档站外链管理**：当开源项目的 README 或官方文档需要引用大量外部参考资料（如规范标准、依赖项目主页、教程文章）时，可使用 HyperLink Hub 统一维护这些链接，并通过 API 动态生成文档中的外链列表，避免硬编码带来的维护负担。

2.  **技术团队内部知识库资源聚合**：企业研发团队可将常用的内部系统入口（如 Jenkins、SonarQube、Wiki）、云服务控制台、公共镜像源地址等录入系统，配合可用性探测功能，快速发现因证书过期或 IP 变动导致的不可用服务，减少故障排查时间。

3.  **个人技术博客友情链接与阅读清单**：技术博主可利用本系统管理友链互换信息以及待阅读的优质文章链接，通过分类标签区分“已读”、“待读”、“推荐”等状态，并定期生成静态页面作为博客的子页面发布，实现内容沉淀与分享。

4.  **社区导航站点运营**：技术社区运营者可以基于 HyperLink Hub 快速搭建垂直领域的资源导航站（如 Go 语言中文资源导航、Kubernetes 生态工具索引），通过分类与标签体系组织内容，利用静态导出功能降低服务器成本，同时保持数据更新的灵活性。

## 快速开始

以下步骤将指导您在本地环境中完成项目的克隆、依赖安装与服务启动。

```bash
# 1. 克隆仓库至本地
git clone https://github.com/hyperlink-hub/core.git
cd core

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate  # Windows 请使用 venv\Scripts\activate
pip install -r requirements.txt

# 3. 初始化数据库并启动开发服务器
python manage.py migrate
python manage.py runserver --host 0.0.0.0 --port 8080
```

启动成功后，访问 `http://localhost:8080` 即可进入 Web 管理界面。默认管理员账号为 `admin`，初始密码为 `admin123`，首次登录后请立即修改。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 – 3.12 | 核心运行环境，推荐使用 3.11 以获得最佳性能 |
| SQLite | 3.35.0 及以上 | 内置数据库，需启用 FTS5 扩展（默认已开启） |
| pip | 21.0 及以上 | Python 包管理工具，用于安装依赖 |
| aiohttp | 3.9.0 及以上 | 异步 HTTP 客户端，用于可用性探测 |
| jinja2 | 3.1.0 及以上 | 模板引擎，用于静态站点生成 |
| click | 8.1.0 及以上 | 命令行交互框架，用于自定义管理命令 |
| pytest | 7.4.0 及以上 | 仅开发测试时需要，生产环境可不安装 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user/quick-start.md` | 如何快速上手使用 Web 界面进行资源增删改查？ |
| 用户手册 | `/docs/user/classification.md` | 如何设计分类与标签体系以高效组织资源？ |
| 开发指南 | `/docs/dev/api-reference.md` | 各 RESTful 端点的请求/响应格式及鉴权方式是什么？ |
| 开发指南 | `/docs/dev/health-check.md` | 可用性探测模块的工作机制与超时阈值如何调整？ |
| 运维手册 | `/docs/ops/deployment.md` | 如何使用 uWSGI + Nginx 进行生产环境部署？ |
| 运维手册 | `/docs/ops/backup.md` | 数据库与配置文件的备份策略及恢复操作步骤？ |

## 资源列表

本节收录项目在建设过程中参考或推荐的互联网资源。所有链接均按类别分组，且严格按照用户提供的内容原样呈现，未作任何修改。

**影视资源类**

- <code>renqixiliezhongwenzimua.org.cn</code>
- <code>wuyefulizhiboa.org.cn</code>
- <code>lalalazhongwendianshijua.org.cn</code>
- <code>yinghuadongmanguanfangbana.org.cn</code>
- <code>zhongwenzimuyongjiuzaixiana.org.cn</code>
- <code>mianfeizhuijuwangzhana.org.cn</code>
- <code>gaoqingzhongwenzimua.org.cn</code>

## 项目结构

项目采用分层架构设计，核心代码与配置分离，便于维护与扩展。

```
.
├── manage.py                  # 项目入口脚本，包含 CLI 命令
├── requirements.txt           # 生产环境依赖列表
├── config/                    # 全局配置目录
│   ├── settings.py            # 基础配置（数据库路径、日志级别等）
│   ├── settings.dev.py        # 开发环境配置（覆盖基础配置）
│   └── settings.prod.py       # 生产环境配置（覆盖基础配置）
├── app/                       # 主应用模块
│   ├── __init__.py
│   ├── models.py              # SQLAlchemy ORM 模型（资源、分类、标签）
│   ├── schemas.py             # Pydantic 请求/响应数据校验模型
│   ├── api/                   # RESTful API 路由层
│   │   ├── v1/                # API 版本 v1
│   │   │   ├── resources.py   # 资源增删改查端点
│   │   │   ├── categories.py  # 分类管理端点
│   │   │   └── health.py      # 探测任务触发端点
│   │   └── __init__.py
│   ├── core/                  # 核心业务逻辑层
│   │   ├── resource_manager.py # 资源条目增删改查事务逻辑
│   │   ├── tag_engine.py      # 标签关联与冲突检测
│   │   └── importer.py        # CSV/JSON 导入解析器
│   ├── services/              # 独立服务模块
│   │   ├── checker.py         # 异步可用性探测服务
│   │   ├── static_gen.py      # 静态站点生成器
│   │   └── search.py          # FTS5 全文检索服务
│   ├── templates/             # Jinja2 模板目录
│   │   ├── base.html          # 基础骨架模板
│   │   ├── index.html         # 资源列表页模板
│   │   └── detail.html        # 资源详情页模板
│   └── static/                # 前端静态资源（CSS / JS）
│       ├── style.css
│       └── script.js
├── tests/                     # 单元测试与集成测试目录
│   ├── conftest.py            # pytest 全局 fixture
│   ├── test_models.py         # ORM 模型测试
│   ├── test_api.py            # API 端点测试
│   └── test_checker.py        # 探测服务测试
├── scripts/                   # 运维辅助脚本
│   ├── backup_db.sh           # 数据库备份脚本
│   └── gen_static.sh          # 一键静态导出脚本
└── docs/                      # 项目文档源文件
    ├── user/                  # 用户手册
    └── dev/                   # 开发与运维手册
```

## 贡献指南

我们欢迎并感谢任何形式的贡献。请遵循以下步骤以确保协作流程顺畅。

1.  **问题追踪**：在提交代码之前，请先在 GitHub Issues 中查找是否已有相关问题讨论。若无，请新建一个 Issue 清晰描述您发现的缺陷或希望新增的功能，并等待维护者确认可行性。
2.  **分支规范**：请从 `main` 分支创建您的功能分支，分支命名建议采用 `feat/xxx`（新功能）、`fix/xxx`（缺陷修复）或 `docs/xxx`（文档更新）前缀。
3.  **代码风格**：项目遵循 PEP 8 编码规范，并配置了 `black` 与 `isort` 自动格式化工具。提交前请执行 `make format` 以统一代码风格。同时，所有新增函数需包含 docstring 说明。
4.  **测试要求**：所有新增功能或缺陷修复必须附带相应的单元测试用例，并确保现有测试套件全部通过（执行 `pytest`）。对于涉及外部 HTTP 请求的模块，请使用 `aioresponses` 模拟网络交互。
5.  **提交合并请求**：推送分支至远程仓库后，创建 Pull Request（PR）并填写模板内容，简要描述变更目的与影响。PR 需要至少一名维护者审核通过后方可合并。

## 常见问题

**问：可用性探测服务是否会误判某些正常站点为不可达？**

答：探测模块默认使用 `GET` 请求，超时时间设为 5 秒，仅检查 HTTP 状态码是否为 200 或 301/302。部分站点可能屏蔽非浏览器 User-Agent 或存在前端渲染延迟，此类情况会被标记为异常。您可通过修改配置文件中的 `CHECK_TIMEOUT` 与 `CHECK_ALLOWED_CODES` 参数调整探测策略。对于特殊站点，支持在资源条目中单独配置自定义请求头。

**问：如何将现有浏览器书签批量导入到 HyperLink Hub？**

答：项目暂不提供直接导入浏览器书签 HTML 文件的功能，但您可以将书签导出为 CSV 格式（使用第三方工具或手动整理），列顺序为 `title,url,category,tags`，然后通过管理后台的“导入”功能上传。若您熟悉命令行，也可以使用 `python manage.py import --format csv --file bookmarks.csv` 完成批量导入。

**问：静态站点生成后，资源链接发生变化怎么办？**

答：静态站点是某一时刻数据库内容的快照，不会自动同步更新。您需要重新执行 `python manage.py gen-static --output ./dist` 命令生成新的静态文件，并重新部署至 Web 服务器。建议通过 crontab 设置每日定时任务自动生成并发布，以保持内容新鲜度。

## 许可证

MIT License

Copyright (c) 2026 HyperLink Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
