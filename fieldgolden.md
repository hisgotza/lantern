# ResourceHub

ResourceHub 是一个面向技术开发者与内容创作者的轻量级外链资源汇总平台，旨在解决多源技术文档、视频资料与在线工具分散难以统一管理的问题。项目本身不存储任何实体资源，仅作为结构化导航索引，通过静态站点方式提供快速、可定制的资源聚合服务。核心目标用户为需要频繁查阅外部技术资料、维护个人知识库或搭建团队文档导航的中高级工程师与技术写作人员。

## 功能概览

- **多级分类索引**：支持按技术领域、资源类型、适用场景创建无限层级目录，便于大规模外链的有序组织。
- **智能标签系统**：为每条资源自动生成基于域名与路径关键词的标签云，支持多标签组合筛选。
- **全文元数据检索**：基于资源标题、描述、标签与分类名称的轻量级倒排索引，检索响应时间低于 200ms。
- **批量导入与校验**：支持通过 CSV 或 JSON 格式批量导入外链列表，并自动执行可达性检测与协议一致性校验。
- **访问统计看板**：内置基于日志聚合的点击频次、来源地域与时段分布统计，提供原始数据导出接口。
- **只读 API 服务**：提供 RESTful 风格的资源查询接口，支持按分类、标签或关键词获取结构化外链清单，便于第三方集成。
- **静态站点生成模式**：支持将当前索引全量导出为 HTML 静态文件，可直接部署至对象存储或 CDN，实现零后端运行。

## 应用场景

- **技术团队内部文档导航**：研发团队可将日常使用的 API 手册、设计规范、CI/CD 配置模板等外部链接统一收录至 ResourceHub，通过分类与标签快速定位，减少重复查找时间。
- **开源项目外链附录管理**：开源项目维护者可将项目依赖的参考文档、社区论坛、版本发布记录等外链集中托管于 ResourceHub，并随项目版本发布同步更新，保持附录与代码仓库解耦。
- **个人技术写作素材库**：技术博主或教程作者可利用 ResourceHub 按主题（如云原生、数据库调优、前端框架）组织收藏的参考资料、视频教程与交互式演示站点，在写作时快速调取引用。
- **线下技术沙龙资源分发**：活动组织者可在沙龙前后将讲稿、视频回放、相关工具链下载页等链接通过 ResourceHub 聚合，生成短码或二维码供参会者一键访问，替代传统邮件抄送。

## 快速开始

执行以下命令在本地启动 ResourceHub 实例：

```bash
# 克隆代码仓库
git clone https://github.com/resourcehub/main.git resourcehub

# 进入项目目录
cd resourcehub

# 安装依赖（使用 npm，Node.js >= 18.0）
npm install

# 启动开发服务器，默认监听 3000 端口
npm run dev
```

启动成功后，访问 `http://localhost:3000` 即可进入管理控制台，首次运行将自动生成示例分类与占位数据。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | >= 18.0.0 | 运行时环境，用于执行核心服务与构建脚本 |
| npm | >= 9.0.0 | 包管理工具，用于安装项目依赖 |
| SQLite3 | >= 3.40.0 | 嵌入式数据库，用于存储索引元数据与统计信息（自动安装） |
| Git | >= 2.30.0 | 版本控制工具，用于克隆仓库及贡献代码 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 支持主流操作系统，生产环境建议 Linux 内核 5.0 以上 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何添加分类、导入外链、配置标签与生成静态站点 |
| 运维指南 | /docs/operations/ | 如何部署生产环境、配置反向代理、执行数据备份与迁移 |
| API 参考 | /docs/api-reference/ | 所有只读接口的请求参数、响应结构与错误码说明 |
| 贡献者规范 | /docs/contributing/ | 代码风格、提交信息格式、PR 审核流程与测试要求 |

完整文档位于项目根目录 `docs/` 文件夹下，亦可在线访问官方文档站点（参见资源列表）。

## 资源列表

### 官方项目资源

<code>zaixianbofangzhongwenzimua.org.cn</code>

<code>zhongwenshipinzaixianguankana.org.cn</code>

<code>shipinmianfeizaixianguankana.org.cn</code>

### 扩展内容与社区镜像

<code>rimanzaixianguankana.org.cn</code>

<code>rihanzaixianmianfeishipina.org.cn</code>

<code>zhongwenzimumianfeibofanga.org.cn</code>

<code>renqixiliezhongwenzimua.org.cn</code>

## 项目结构

```
resourcehub/
├── src/                           # 核心源代码目录
│   ├── core/                      # 索引引擎与元数据管理模块
│   │   ├── indexer.js             # 外链解析与倒排索引构建
│   │   └── validator.js           # 协议校验与可达性检测
│   ├── api/                       # RESTful 接口实现
│   │   ├── routes/                # 路由定义（分类、标签、检索）
│   │   └── middleware/            # 日志、限流与错误处理
│   ├── ui/                        # 管理控制台前端组件
│   │   ├── pages/                 # 分类管理、导入向导、看板页面
│   │   └── components/            # 复用表格、筛选器与图表组件
│   └── static/                    # 静态站点生成模板与主题资源
├── config/                        # 环境配置与默认分类预设
│   ├── default-categories.json    # 初始技术领域分类树
│   └── system.yaml                # 端口、缓存、日志级别配置
├── data/                          # SQLite 数据库文件与迁移脚本
│   ├── migrations/                # 版本化 schema 变更
│   └── seed/                      # 示例外链初始数据集
├── tests/                         # 单元测试与集成测试用例
│   ├── unit/                      # 索引器、校验器独立测试
│   └── integration/               # API 端点全链路测试
├── docs/                          # 用户手册、运维指南与 API 文档
│   ├── user-guide/                # 分类添加、导入导出流程
│   └── api-reference/             # 接口请求示例与返回字段说明
├── scripts/                       # 构建、导出与部署辅助脚本
│   ├── build-static.sh            # 全量生成静态 HTML 文件
│   └── backup-db.sh               # 数据库定时备份封装
├── package.json                   # npm 依赖清单与脚本入口
└── README.md                      # 项目总览（本文件）
```

## 贡献指南

1.  **分支管理**：从 `main` 分支切出 `feature/xxx` 或 `fix/xxx` 命名的新分支进行开发，禁止直接向 `main` 提交。
2.  **代码风格**：遵循项目根目录 `.eslintrc` 与 `.prettierrc` 配置，提交前执行 `npm run lint` 与 `npm run format` 确保风格一致。
3.  **测试覆盖**：新增或修改核心索引、校验逻辑时，需在 `tests/` 下补充对应单元测试，确保覆盖率不低于 80%。
4.  **提交信息**：采用 `type(scope): subject` 格式，type 可选 `feat` / `fix` / `docs` / `refactor` / `test`，scope 为模块名，subject 简明描述变更内容。
5.  **PR 流程**：提交 Pull Request 至 `main` 分支，需至少一名项目维护者审核，CI 流水线（包含 lint、test、build）全部通过后方可合并。

## 常见问题

**Q：ResourceHub 是否存储视频或文档实体文件？**  
A：不存储。项目仅保存外部链接的元数据（标题、描述、分类、标签），所有资源内容仍由原始站点提供。用户点击外链时将直接跳转至目标 URL，不经过任何代理或缓存。

**Q：如何迁移已有书签或收藏夹数据？**  
A：支持从 Chrome、Firefox 导出的 HTML 书签文件，或通用 CSV 格式导入。具体操作请参考 `docs/user-guide/import-export.md` 章节，导入前系统会自动识别字段映射并生成预览。

**Q：静态站点生成模式是否支持自定义主题？**  
A：支持。所有静态模板位于 `src/static/themes/` 目录，用户可替换 CSS 变量与布局片段。执行 `npm run build-static` 时，系统会根据当前激活的主题渲染全部页面，输出至 `dist/` 文件夹。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
