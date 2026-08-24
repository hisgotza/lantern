# NexusIndex

NexusIndex 是一个面向技术社区与内容创作者的外链资源整理与分发工具。项目定位为“结构化外部链接索引系统”，主要服务于需要定期整理、分类、展示大量外部 URL 的技术博客、开源文档站、个人知识库及小型内容聚合平台。NexusIndex 通过清晰的目录分类、可配置的展示模板以及自动化的链接状态检查，帮助用户高效管理分散在多个领域的外部资源，降低人工维护成本，同时提升访问者对资源整体的可读性与信任度。

项目本身不存储任何实体内容，仅提供索引元数据与展示逻辑，适合用于技术导航站、镜像站入口、社区推荐列表等场景。NexusIndex 采用静态站点生成方式，默认输出纯 HTML 与 Markdown 混合结构，可无缝集成至 GitHub Pages、Nginx 或任何支持静态文件托管的服务中。

## 功能概览

- **多级分类索引**：支持无限层级的目录分类，每个分类可绑定独立描述与图标标识，便于快速定位资源领域。

- **外链自动状态检测**：内置 HTTP 状态码检查模块，可定时探测链接可用性，并在前端以标签形式标注失效或重定向链接。

- **自定义展示模板**：提供默认卡片式与列表式两种布局，用户可通过修改配置文件切换展示风格，或自定义 CSS 覆盖样式。

- **批量导入与导出**：支持通过 CSV 或 JSON 文件批量导入链接数据，同时支持导出为结构化 Markdown 列表或纯文本格式，便于备份或迁移。

- **链接访问统计**：基于轻量级日志记录，统计每个外链的点击次数与最后访问时间，帮助管理员识别高价值资源。

- **搜索与过滤**：提供关键词搜索及按分类、按状态（正常/失效/重定向）过滤功能，提升大型索引站的使用效率。

- **响应式布局**：默认适配桌面端与移动端浏览器，保证在不同屏幕尺寸下的可读性与操作可用性。

## 应用场景

- **技术社区资源导航**：技术论坛或开源社区可使用 NexusIndex 整理官方文档、工具链地址、镜像站及学习资料，为社区成员提供统一入口，减少重复提问。

- **个人知识库外链管理**：知识库作者可将零散收藏的博客、论文、视频教程等外链集中导入 NexusIndex，并按照主题分类，配合定期检查功能确保收藏链接长期有效。

- **项目文档附属索引**：开源项目可在其文档站点中独立部署 NexusIndex 作为“生态资源”页面，列出依赖项目、周边工具、部署示例等外部链接，增强项目生态的可发现性。

- **内部团队资源手册**：企业或团队内部可使用 NexusIndex 搭建私有的技术资源手册，存放内部工具地址、运维面板、监控系统入口等，配合访问统计了解团队常用工具。

## 快速开始

以下步骤适用于 Linux / macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/nexusindex/nexusindex.git
cd nexusindex

# 2. 安装依赖（使用 pip 与 npm）
pip install -r requirements.txt
npm install

# 3. 初始化配置并生成静态站点
cp config.example.yaml config.yaml
python scripts/init_db.py
npm run build

# 4. 启动本地预览服务
python server.py --port 8080
```

访问 `http://localhost:8080` 即可查看默认示例索引页。若需自定义链接数据，请编辑 `data/links.json` 或通过管理接口导入。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 及以上 | 用于后端服务、状态检测与数据管理脚本 |
| Node.js | 18.x 及以上 | 用于前端构建与静态资源打包 |
| npm | 9.x 及以上 | 管理前端依赖与构建工具 |
| SQLite | 3.35 及以上 | 默认数据库，用于存储链接元数据与访问日志 |
| Git | 2.30 及以上 | 用于版本管理与克隆仓库 |

额外建议：若启用 HTTPS 状态检测并发功能，需确保操作系统支持 `ulimit -n` 调整文件描述符限制；生产环境推荐使用 Nginx 或 Caddy 作为反向代理。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user-guide/` | 如何添加链接、分类、修改模板、查看统计 |
| 管理员指南 | `docs/admin-guide/` | 如何配置检测策略、备份数据、迁移数据库 |
| 开发参考 | `docs/developer-guide/` | API 接口说明、数据库表结构、插件扩展方式 |
| 部署示例 | `docs/deployment/` | Nginx 配置、Docker 部署、GitHub Actions 自动化构建 |

## 资源列表

### 综合资源索引

- <code>guomotaotu.net.cn</code>
- <code>hanmanguanfangmianfeirukou.net.cn</code>
- <code>guomosipaishipin.net.cn</code>

### 视频与多媒体分类

- <code>meinvwangzhanmianfeikan.net.cn</code>
- <code>jiqingshipinwang.net.cn</code>
- <code>oumeirihanzonghezaixian.net.cn</code>
- <code>miyouzaixianshipin.net.cn</code>

## 项目结构

```
nexusindex/
├── config.yaml               # 主配置文件，包含站点名称、分类映射、检测间隔
├── server.py                 # 轻量级开发服务器，提供预览与 API 接口
├── requirements.txt          # Python 依赖列表
├── package.json              # Node.js 项目配置与构建脚本
├── data/
│   ├── links.json            # 核心链接数据（分类、标题、URL、标签）
│   ├── categories.json       # 分类层级定义与显示顺序
│   └── audit.log             # 状态检测运行日志
├── scripts/
│   ├── init_db.py            # 初始化 SQLite 数据库表结构
│   ├── checker.py            # 外链 HTTP 状态并发检测模块
│   ├── importer.py           # CSV/JSON 批量导入工具
│   └── exporter.py           # 导出为 Markdown/JSON 工具
├── src/
│   ├── assets/               # 前端静态资源（CSS、JS、图片）
│   ├── templates/            # 页面模板（列表页、详情页、分类页）
│   └── utils/                # 前端工具函数（过滤、排序、高亮）
├── build/                    # 构建输出目录（静态站生成结果）
├── tests/                    # 单元测试与集成测试脚本
├── docs/                     # 完整文档（用户/管理员/开发/部署）
└── docker-compose.yml        # 容器化部署示例配置
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆至本地开发环境。请确保使用 `main` 分支作为基线，新建功能分支命名遵循 `feature/描述` 或 `fix/描述` 格式。

2. 安装开发依赖（`pip install -r requirements-dev.txt` 与 `npm install --include=dev`），运行 `npm run test` 确认现有测试全部通过后再进行修改。

3. 若新增功能或修改现有逻辑，请同步更新对应文档（位于 `docs/` 目录）并补充单元测试用例。代码提交时请使用清晰的中文或英文提交信息，说明变更原因与影响范围。

4. 提交 Pull Request 前，请执行 `npm run lint` 与 `npm run build` 确保代码风格一致且构建无误。PR 描述中需列出变更点、测试结果及是否影响已有配置。

5. 提交后等待维护者审阅，审阅周期通常为 3-5 个工作日。若有修改意见，请及时回应并更新代码。合并后您的贡献将列入项目贡献者列表。

## 常见问题

**Q：如何修改索引页的标题与分类名称？**

A：直接编辑 `config.yaml` 文件中的 `site.title` 与 `categories` 字段即可。修改后执行 `npm run build` 重新生成静态文件，无需重启服务。若使用管理后台，也可通过界面设置即时生效。

**Q：外链状态检测的频率与超时时间如何调整？**

A：在 `config.yaml` 中设置 `checker.interval`（单位小时）和 `checker.timeout`（单位秒）。默认每 24 小时检测一次，超时时间为 10 秒。检测为异步并发执行，建议根据服务器网络环境调整超时值，避免误判。

**Q：数据库从 SQLite 迁移到 MySQL 是否支持？**

A：项目默认使用 SQLite 以降低部署门槛，但提供了数据库抽象层。若需迁移至 MySQL，请修改 `server.py` 中的数据库连接字符串，并执行 `scripts/migrate_db.py` 进行数据迁移。迁移前请完整备份原有数据库文件。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:33
