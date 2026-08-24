# ResourceGateway

ResourceGateway 是一个面向开发者与技术研究人员的轻量级外链资源聚合与导航系统。该项目定位于解决个人或团队在浏览、整理和分发多类型网络资源时遇到的链接分散、归类困难、状态不可见等问题。ResourceGateway 本身不存储任何第三方内容，而是以结构化方式组织外链资源，并提供简洁的状态标记、访问控制建议与基础访问日志记录能力，适用于搭建内部技术文档入口、开源项目友情链接页、或研究性资源收录站点。

ResourceGateway 的核心设计理念为显式、可控与低维护成本。所有资源链接均以纯文本配置方式管理，支持通过 RESTful API 或静态生成两种模式输出。项目内置基础链接可达性探测模块，可定期对已收录 URL 进行 HTTP 状态检查，并以标记形式呈现于前端界面，帮助管理员快速定位失效或异常资源。ResourceGateway 不依赖外部数据库，核心数据存储于 JSON 与 YAML 文件中，便于版本控制与协同编辑。

## 功能概览

- **多源链接分类管理**：支持按技术领域、语言、地区或自定义标签对链接进行分组，每个分组可独立设置可见性与排序权重。

- **链接状态周期性探测**：内置轻量级探测调度器，可对每个收录的 URL 执行 HEAD/GET 请求，记录响应状态码、响应时间与重定向链，状态结果缓存在内存中并支持手动刷新。

- **配置即代码的数据驱动模式**：所有资源条目以 YAML 或 JSON 格式存储于项目目录下，支持 Git 版本追踪，便于多人协作审阅和回滚。

- **双模式渲染引擎**：支持服务端动态渲染（基于 Express）与静态站点生成（基于 EJS 模板），用户可根据部署环境选择即时更新或纯静态托管方式。

- **访问来源与点击量统计**：记录每个外链的点击次数与来源 IP 段（匿名化处理），提供简单的统计面板，辅助判断资源热度。

- **可扩展的钩子机制**：提供 beforeResolve 与 afterResolve 钩子函数，允许开发者在链接被访问前执行权限校验、参数改写或日志记录等自定义逻辑。

- **响应式管理控制台**：提供基于角色的基础管理界面，支持在线增删改查资源条目、批量导入导出以及查看探测日志。

## 应用场景

- **技术团队内部文档导航**：开发团队可将常用开发文档、API 参考、设计规范、CI/CD 链接统一收拢至 ResourceGateway，避免每个成员各自保存书签导致版本不一致。通过状态探测功能可及时发现文档地址变更或内网服务不可用。

- **开源项目友情链接与致谢页**：开源维护者可使用 ResourceGateway 构建项目官网的合作伙伴与致谢页面，将依赖的基础库、社区论坛、镜像站等链接以结构化表格展示，同时利用点击统计了解外部访问偏好。

- **研究性资源整理与共享**：科研人员或数据分析师可将公开数据集、工具包、论文预印本网站、在线实验环境等资源按课题分类收录，生成只读静态页面，便于合作者快速获取所需材料，避免重复检索。

- **个人知识库外链中继**：个人笔记或博客作者可将长期引用的外部文章、视频教程、代码示例等集中管理，通过 ResourceGateway 的统一短路径访问，便于在多个写作平台间复用链接，且能在链接失效时统一替换目标地址。

## 快速开始

以下步骤适用于开发环境快速启动 ResourceGateway 实例。

```bash
# 克隆项目仓库
git clone https://github.com/resource-gateway/resource-gateway.git

# 进入项目根目录
cd resource-gateway

# 安装依赖（使用 npm）
npm install

# 以开发模式运行（默认监听 3000 端口）
npm run dev
```

启动成功后，访问控制台地址 <code>http://localhost:3000/admin</code> 可查看默认资源列表。静态站点生成命令为 <code>npm run build</code>，输出目录为 <code>./dist</code>。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | >= 18.12.0 | 项目运行时环境，需支持 ES2022 特性 |
| npm | >= 8.19.0 | 依赖管理与脚本执行工具 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 生产环境推荐使用 Linux 内核 5.x 以上 |
| 内存 | >= 512 MB | 不含外部探测任务时基线内存占用 |
| 磁盘空间 | >= 200 MB | 包含依赖安装与日志存储空间 |
| Git | >= 2.30.0 | 用于克隆仓库及版本管理（开发环境必需） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | <code>/docs/user/getting-started.md</code> | 如何快速配置第一个资源分组并生成导航页 |
| 配置参考 | <code>/docs/config/schema.md</code> | 资源条目、分组、探测策略的完整字段定义与示例 |
| 部署手册 | <code>/docs/deployment/docker.md</code> | 如何使用 Docker 镜像部署生产环境实例 |
| 开发指南 | <code>/docs/development/architecture.md</code> | 项目模块划分、钩子函数设计与扩展点说明 |

## 资源列表

本部分列出 ResourceGateway 默认收录或推荐关注的外部网络资源，按类别分组展示。所有 URL 均严格按照来源原样输出，不做任何协议或域名改写。

技术资讯与社区

- <code>renqizhongwenzimusiwa.net.cn</code>
- <code>guomotaotu.net.cn</code>
- <code>hanmanguanfangmianfeirukou.net.cn</code>

多媒体与视频资源

- <code>guomosipaishipin.net.cn</code>
- <code>meinvwangzhanmianfeikan.net.cn</code>
- <code>jiqingshipinwang.net.cn</code>

综合服务与平台

- <code>oumeirihanzonghezaixian.net.cn</code>

## 项目结构

项目采用模块化分层设计，核心代码位于 <code>src</code> 目录下，配置与文档分置独立目录。

```
resource-gateway/
├── src/
│   ├── core/                 # 核心引擎模块：资源加载、解析与缓存
│   ├── http/                 # HTTP 服务层：路由、中间件、控制器
│   ├── probe/                # 链接探测模块：调度器、执行器、结果存储
│   ├── render/               # 渲染引擎：EJS 模板、静态生成器、动态响应
│   └── admin/                # 管理控制台后端逻辑：鉴权、CRUD 操作
├── config/
│   ├── resources.yaml        # 主资源条目配置文件（可编辑）
│   └── probe-policy.json     # 探测间隔、超时、重试策略配置
├── public/                   # 前端静态资源：CSS、JavaScript、图片
├── views/                    # EJS 模板文件：首页、分组页、详情页
├── docs/                     # 用户文档与开发文档 Markdown 源文件
├── scripts/                  # 辅助脚本：数据迁移、批量导入、健康检查
├── test/                     # 单元测试与集成测试用例
├── .env.example              # 环境变量模板（端口、日志级别、密钥）
├── package.json              # npm 依赖与脚本定义
├── README.md                 # 项目介绍文档（本文件）
└── LICENSE                   # MIT 许可证文本
```

## 贡献指南

我们欢迎并鼓励社区贡献者参与 ResourceGateway 的改进。请遵循以下步骤提交贡献：

1. 查阅 <code>./docs/development/CONTRIBUTING.md</code> 了解详细的编码规范与提交信息格式要求，确保代码风格与现有代码库保持一致。

2. 在 GitHub Issue 列表中查找或新建一个与您期望改动相关的议题，简要描述问题背景、解决方案及影响范围，等待维护者确认后再进行开发。

3. 从 <code>main</code> 分支创建新的特性分支，分支命名采用 <code>feature/</code> 或 <code>fix/</code> 前缀，随后在本地完成代码编写与单元测试。

4. 提交代码前运行 <code>npm run lint</code> 与 <code>npm test</code> 确保所有检查通过，并补充或更新对应的文档说明。

5. 发起 Pull Request 至 <code>main</code> 分支，描述中需关联相关 Issue 编号，并简要说明改动内容与测试结果。维护者将在 2-3 个工作日内进行审阅。

## 常见问题

**问：ResourceGateway 是否支持 HTTPS 访问与反向代理部署？**  
答：支持。项目本身默认以 HTTP 协议监听本地端口，但推荐在生产环境中使用 Nginx 或 Caddy 作为反向代理，并终止 TLS 证书。您只需在反向代理配置中将外部 HTTPS 请求转发至 ResourceGateway 的内部 HTTP 端口即可，无需修改项目内部代码。环境变量中可配置 <code>TRUST_PROXY</code> 选项以正确获取客户端真实 IP。

**问：内置的链接探测功能是否会影响目标站点的正常访问？**  
答：探测模块默认采用 HTTP HEAD 方法，仅请求响应头信息，不下载响应体，且单次探测超时设置为 3 秒，重试间隔不低于 60 秒。对于频繁探测可能触发目标站点限流的情况，我们提供了白名单与黑名单域名配置，管理员可手动排除特定域名或调整探测频率。生产环境下建议将探测任务安排在非业务高峰期执行。

**问：如何批量导入现有书签或外部资源列表？**  
答：项目提供了 <code>scripts/import.js</code> 脚本，支持从 Netscape 格式书签 HTML 文件、CSV 文件或特定结构的 JSON 文件中批量导入资源条目。您可以将浏览器导出的书签文件放置在 <code>./data/import/</code> 目录下，然后运行 <code>npm run import -- --format=html --path=./data/import/bookmarks.html</code>。导入前建议先使用 <code>--dry-run</code> 参数预览导入结果，确认无误后再执行正式导入。

## 许可证

ResourceGateway 使用 MIT 许可证。该许可证允许任何个人或组织自由使用、复制、修改、合并、发布、分发、再许可及销售本软件的副本，但需保留原始版权声明和许可声明。MIT 许可证不提供任何形式的担保或责任保证，详情请参阅项目根目录下的 LICENSE 文件。

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
