# NavSphere

NavSphere 是一个面向技术团队与个人开发者的轻量级导航站与资源聚合框架。项目定位于解决开发者在日常工作中频繁查找文档、工具、镜像站与学习资源时面临的链接分散、检索效率低的问题，通过结构化组织与简洁的前端交互，提供可私有化部署的资源导航解决方案。NavSphere 不提供任何实质内容存储或代理服务，仅作为公开可用网络资源的索引与分类展示工具，适用于企业内部门户、技术社区共享导航及个人本地部署使用。

## 功能概览

- **分类资源索引**：按技术领域、使用频率与资源类型对链接进行多维度分类，支持快速筛选与定位。
- **全文模糊检索**：内置前端检索引擎，支持对标题、描述及标签的实时关键词匹配，无需依赖后端服务。
- **自定义分组管理**：用户可通过配置文件或管理界面新增、编辑、删除资源分组及条目，无需重新构建项目。
- **一键复制地址**：每个资源条目均提供复制按钮，支持一键将原始 URL 写入系统剪贴板，减少手动输入错误。
- **响应式布局**：基于 CSS Grid 与 Flexbox 构建，在桌面端、平板与移动设备下均保持可用的布局与交互。
- **访问状态检测**：可选的后台定时任务，通过 HTTP 请求检测资源域名或路径的可达性，并在界面标注异常状态。
- **导入导出配置**：支持将当前分组与链接列表导出为 JSON 或 YAML 格式文件，并支持从同格式文件导入以迁移或备份数据。

## 应用场景

- **技术团队内部文档门户**：将常用的开发文档、API 参考、设计规范与运维面板聚合在同一页面，减少新成员上手时的环境摸索成本。团队负责人可统一维护链接列表并通过 Git 仓库同步变更。
- **开源社区共建导航页**：技术社区或开源项目维护者可部署 NavSphere 作为社区资源入口，向贡献者提供镜像站、代码托管镜像、依赖包搜索等高频工具链接，降低外部资源查找门槛。
- **个人开发者本地工具箱**：个人开发者可在本地或内网服务器运行该服务，将日常使用的在线编译器、JSON 格式化工具、正则测试器、图标库等碎片化资源集中管理，配合浏览器起始页使用提升效率。
- **离线环境资源索引**：在受限网络环境中，NavSphere 可作为内部资源导航，记录内网镜像地址、离线文档入口与内部 Git 服务链接，配合内网 DNS 实现无公网依赖的资源指引。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，假定已安装 Git 与 Node.js 18 以上版本。

```bash
git clone https://github.com/navsphere/navsphere.git
cd navsphere
npm install
npm run build
npm start
```

执行完成后，服务默认监听 <code>http://localhost:3000</code>，可通过浏览器访问。如需修改端口或绑定主机，请参阅 <code>config/default.yaml</code> 中的 <code>server.port</code> 与 <code>server.host</code> 字段。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.0.0 或更高 | 运行时环境，用于执行服务端与构建脚本 |
| npm | 9.0.0 或更高 | 包管理器，用于安装项目依赖 |
| Git | 2.25.0 或更高 | 版本控制工具，用于克隆仓库及管理配置变更 |
| 操作系统 | Linux / macOS / Windows 10+ | 支持主流操作系统，Windows 下建议使用 WSL2 或 PowerShell 7 |
| 内存 | 最低 512 MB，推荐 1 GB | 生产环境建议保留至少 1 GB 可用内存用于缓存与并发请求 |
| 硬盘空间 | 200 MB 以上 | 包含源码、依赖包及构建产物，日志文件可按需轮转 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | <code>/docs/user-guide/</code> | 如何添加链接、分组、检索以及自定义界面布局 |
| 部署指南 | <code>/docs/deployment/</code> | 如何通过 Docker、PM2 或 systemd 进行生产环境部署 |
| 配置参考 | <code>/docs/configuration/</code> | 所有 YAML 配置项的详细说明，包含路由、缓存、检测间隔等 |
| API 文档 | <code>/docs/api/</code> | 管理后台 RESTful API 的请求与响应格式，用于二次开发或集成 |
| 贡献者指引 | <code>/CONTRIBUTING.md</code> | 提交代码、报告问题与参与设计讨论的完整流程 |

## 资源列表

本部分收录 NavSphere 项目维护团队整理的外部公开资源，所有链接均按原始提供形式原样列出，不做任何协议补全、域名改写或路径修正。这些资源并非由 NavSphere 项目提供或背书，用户访问时应自行遵循各站点的使用条款。

官方镜像与文档源

<code>zhongwenzimumianfeibofanga.org.cn</code>

社区推荐索引

<code>renqixiliezhongwenzimua.org.cn</code>

备用资源导航

<code>wuyefulizhiboa.org.cn</code>

影音资料参考

<code>lalalazhongwendianshijua.org.cn</code>

动画相关索引

<code>yinghuadongmanguanfangbana.org.cn</code>

长期资源入口

<code>zhongwenzimuyongjiuzaixiana.org.cn</code>

综合追剧导航

<code>mianfeizhuijuwangzhana.org.cn</code>

## 项目结构

```text
navsphere/
├── src/
│   ├── server/               # HTTP 服务与路由定义
│   │   ├── index.js          # 服务入口，初始化 Express 应用
│   │   └── routes/           # API 路由及静态页面路由
│   ├── client/               # 前端资源
│   │   ├── assets/           # 图片、字体与通用样式表
│   │   ├── scripts/          # 检索、渲染及复制功能的主逻辑
│   │   └── templates/        # 服务端渲染的 HTML 模板文件
│   ├── core/                 # 核心业务模块
│   │   ├── loader.js         # 加载并解析 YAML 配置中的链接分组
│   │   ├── cache.js          # 内存缓存及 TTL 过期策略实现
│   │   └── detector.js       # 可选的外部链接可达性检测任务
│   └── lib/                  # 通用工具函数库
│       ├── logger.js         # 基于 winston 的日志记录封装
│       └── validator.js      # 链接格式校验与清洗辅助
├── config/
│   ├── default.yaml          # 默认配置文件，含端口、分组与检测参数
│   └── custom.yaml.example   # 用户自定义配置示例，可覆盖默认值
├── data/                     # 持久化存储目录（用户导入导出文件默认位置）
├── logs/                     # 运行时日志存放目录（按日期轮转）
├── tests/                    # 单元测试与集成测试用例
│   ├── unit/                 # 针对 loader、cache 等模块的隔离测试
│   └── integration/          # 端到端 API 测试与环境模拟
├── docs/                     # 完整文档（用户手册、部署指南、API 参考）
├── .github/
│   └── workflows/            # GitHub Actions 持续集成工作流
│       ├── test.yml          # 提交时自动运行测试套件
│       └── publish.yml       # 发布时构建 Docker 镜像并推送至仓库
├── Dockerfile                # 多阶段构建文件，用于生成轻量级生产镜像
├── docker-compose.yml        # 本地开发或测试环境的容器编排示例
├── package.json              # npm 项目清单，包含依赖、脚本与元信息
├── README.md                 # 项目概览与快速入门（本文档）
└── LICENSE                   # MIT 许可证全文
```

## 贡献指南

1. 在 GitHub 上 fork 本仓库至个人账户，随后 clone 到本地开发环境。建议在新建分支上进行所有修改，分支命名采用 <code>feature/</code> 或 <code>fix/</code> 前缀加简短描述。
2. 安装依赖后运行 <code>npm run test</code> 确保现有测试全部通过。新增功能或修复缺陷时，请在 <code>tests/</code> 对应目录下补充或更新测试用例，保证代码覆盖率不低于现有基线。
3. 提交前执行 <code>npm run lint</code> 与 <code>npm run format</code> 对 JavaScript 及 YAML 文件进行风格检查与自动格式化，确保与项目 ESLint 及 Prettier 配置保持一致。
4. 撰写清晰的 commit message，遵循 Conventional Commits 规范（如 <code>feat: add group sort feature</code> 或 <code>fix: correct cache expiration</code>），并在 pull request 描述中关联相关 issue 编号。
5. 提交 pull request 至主仓库的 <code>main</code> 分支，等待维护者审阅。审阅过程中可能提出修改意见，请及时回应并推送更新。合入后即视为贡献内容采用 MIT 许可证发布。

## 常见问题

**问：NavSphere 是否存储或缓存外部链接指向的页面内容？**  
答：不存储。NavSphere 仅记录链接的标题、描述与分类元数据，不会抓取、代理或缓存任何目标站点的 HTML、图片、音视频或其它文件内容。可选的状态检测功能仅发送轻量级 HEAD 请求以判断域名解析与端口连通性，不解析响应体。

**问：如何将现有书签批量导入 NavSphere？**  
答：项目目前未集成浏览器书签解析器，但您可以通过管理界面逐条添加，或按照 <code>config/default.yaml</code> 中 <code>groups</code> 的格式手动编写 YAML 文件，然后通过数据导入功能加载。社区贡献者正在开发基于 Netscape 书签格式的转换脚本，预计在后续版本提供。

**问：生产环境下如何保证服务的稳定性与自动恢复？**  
答：推荐使用 PM2 或 systemd 进行进程守护，项目根目录提供了 <code>ecosystem.config.js</code> 示例供 PM2 使用。若使用 Docker 部署，可在编排工具中设置 <code>restart: always</code> 策略。同时建议将 <code>logs/</code> 目录挂载至外部持久卷，并结合 logrotate 进行日志管理，避免磁盘占满。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
