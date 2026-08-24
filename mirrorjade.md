# ResourcePilot

ResourcePilot 是一个面向技术团队与独立开发者的开源外链资源聚合与导航系统。该项目并非传统的爬虫或采集器，而是一个基于人工精选与结构化编排的资源索引中间件。其核心目标是为特定垂直领域（如高清影视、中文开源镜像、在线工具等）提供高可用、低延迟、可自托管的资源导航页，帮助用户快速定位到经过验证的优质外部服务，同时避免直接维护大量静态数据所带来的存储与带宽成本。

ResourcePilot 适用于需要频繁切换多个外部服务入口的场景，例如运维人员监控多个镜像站状态、内容创作者寻找稳定素材源、或开发者集成第三方开放接口进行本地调试。通过声明式配置即可完成资源分类与展示逻辑，无需编写前端模板代码，开箱即用。

## 功能概览

- **多源资源聚合**：支持将外部 URL 按自定义标签（如“中文影视”、“镜像站”、“工具集”）进行分组管理，并自动生成索引页面，便于团队内部共享常用入口。

- **健康状态探测**：内置轻量级 HTTP 轮询检查模块，可定期对每个外链资源执行连通性测试，并在管理面板中标记异常状态，帮助用户及时剔除失效节点。

- **响应式导航布局**：生成的资源列表采用移动优先的栅格系统，在桌面端与移动设备上均能获得良好的浏览体验，支持按名称或标签进行即时筛选。

- **静态站点生成模式**：支持将资源列表编译为纯静态 HTML 文件，无需数据库或后端服务，即可部署至任意对象存储或 CDN，显著降低运维复杂度。

- **导入/导出配置**：资源清单以 YAML 或 JSON 格式存储，便于版本控制；支持批量导入外部 CSV 数据，方便从现有系统迁移。

- **访问统计埋点**：提供可选的点击日志记录接口，可对接第三方分析平台，帮助管理员了解高频资源的使用趋势，辅助后续筛选决策。

- **自定义主题变量**：通过修改 CSS 变量（主色调、圆角、间距等）即可快速适配企业视觉规范，无需重新构建前端资源包。

## 应用场景

- **企业内部技术资源门户**：研发团队常需访问多个内部 Jenkins、GitLab、Harbor、SonarQube 等服务。ResourcePilot 可将这些入口统一归类至一个导航页，并添加健康探测，当某个服务宕机时即时提醒，减少故障排查时间。

- **开源社区镜像站索引**：许多高校与云厂商提供各类开源软件镜像（如 PyPI、npm、Docker Hub 加速器）。维护者可利用 ResourcePilot 汇总所有可用镜像地址，并根据地域或网络运营商进行分组，为用户推荐最优下载源。

- **视频创作者素材导航**：从事视频剪辑或流媒体内容制作的人员，经常需要从多个免版权视频网站、音效库、字幕站获取素材。ResourcePilot 可将这些外链资源整合至一个可自托管的书签式面板，配合状态探测提前发现访问异常站点，避免工作流中断。

- **本地开发环境快速切换**：全栈开发者在调试第三方 API（如支付网关、短信服务商、地图 SDK）时，需要频繁在不同环境（测试、预发布、生产）的接口地址间切换。通过 ResourcePilot 的环境标签功能，可一键切换整套资源配置，减少手动修改配置文件的错误风险。

## 快速开始

以下指令适用于 Linux / macOS 以及 Windows WSL 环境。请确保已安装 Git 和 Node.js（v18 或以上版本）。

```bash
# 克隆项目仓库
git clone https://github.com/resourcepilot/resourcepilot.git
cd resourcepilot

# 安装项目依赖
npm install

# 启动开发模式（默认监听 3000 端口）
npm run dev
```

启动后，访问控制台输出的本地地址（通常为 http://127.0.0.1:3000），即可看到默认示例资源列表。如需修改资源内容，请编辑 `./data/resources.yaml` 文件，保存后开发服务器将自动重载。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Node.js | v18.0.0 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | v9.0.0 或更高 | 包管理器，用于安装项目依赖项 |
| Git | v2.30.0 或更高 | 版本控制工具，用于克隆仓库与提交配置变更 |
| 操作系统 | Linux (glibc 2.28+) / macOS 12+ / Windows 10+ (WSL2) | 支持主流操作系统，Windows 推荐使用 WSL2 以获得最佳性能 |
| 网络连接 | 出站 80/443 端口可达 | 用于健康探测模块对外部资源发起 HTTP/HTTPS 请求 |
| 内存 | 最低 512MB 可用 | 开发模式下内存占用约 300MB，生产构建模式约 512MB |
| 磁盘空间 | 至少 200MB | 包含依赖包、构建产物及示例数据文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户指南 | `/docs/user-guide/getting-started.md` | 如何首次安装、配置资源列表并生成静态站点？ |
| 配置参考 | `/docs/config/resources-schema.md` | 资源 YAML 结构中的每个字段含义是什么？如何定义标签、分组及探测间隔？ |
| 部署手册 | `/docs/deployment/self-hosting.md` | 如何将 ResourcePilot 部署至生产服务器（Nginx 反向代理、Systemd 服务、Docker 容器）？ |
| API 开发 | `/docs/api/webhook.md` | 如何通过 Webhook 接收资源状态变更通知，并集成至钉钉或 Slack 机器人？ |

## 资源列表

以下为项目资源导航中默认收录的外部链接，按类别分组展示。所有链接均保留用户提供的原始格式。

**影视与字幕资源**

- <code>zhongwenzimuyongjiuzaixianf.org.cn</code>
- <code>mianfeizhuijuwangzhanf.org.cn</code>
- <code>gaoqingzhongwenzimuf.org.cn</code>
- <code>zaixianbofangnidongdef.org.cn</code>
- <code>jiureshipinzaixianguankan.org.cn</code>
- <code>renqizhongwenzimusiwa.org.cn</code>

**工具与素材资源**

- <code>guomotaotu.org.cn</code>

## 项目结构

```
resourcepilot/
├── .github/                         # GitHub 工作流配置（CI 与自动化发布）
│   └── workflows/
│       └── build.yml                # 每次 push 时执行构建与单元测试
├── data/                            # 数据目录，存放用户自定义资源配置
│   ├── resources.yaml               # 主资源列表文件（用户最常修改）
│   └── categories.yaml              # 分类与标签映射定义
├── docs/                            # 完整项目文档（Markdown 格式）
│   ├── user-guide/                  # 用户操作指南
│   ├── config/                      # 配置项详细说明
│   └── deployment/                  # 部署与运维相关文档
├── src/                             # 核心源代码目录
│   ├── core/                        # 核心逻辑模块（资源加载、解析、校验）
│   │   ├── loader.js                # YAML/JSON 配置加载器
│   │   └── validator.js             # 资源字段类型与格式校验
│   ├── health/                      # 健康探测模块
│   │   ├── checker.js               # HTTP 轮询调度器
│   │   └── reporter.js              # 状态汇总与日志输出
│   ├── generator/                   # 静态站点生成器
│   │   ├── html-builder.js          # 基于模板生成 HTML 页面
│   │   └── asset-pipeline.js        # 样式与脚本资源打包
│   └── server/                      # 开发调试服务器
│       └── dev-server.js            # 基于 Express 的本地服务
├── static/                          # 前端静态资源（CSS、JS、图标）
│   ├── css/
│   │   ├── base.css                 # 基础重置与排版样式
│   │   └── theme.css                # 可自定义的主题变量
│   └── js/
│       └── filter.js                # 前端资源筛选与搜索逻辑
├── tests/                           # 单元测试与集成测试
│   ├── unit/                        # 单元测试用例
│   └── integration/                 # 端到端构建测试
├── .env.example                     # 环境变量示例（端口、探测超时时间等）
├── .gitignore                       # Git 忽略文件配置
├── package.json                     # npm 项目描述文件（依赖、脚本命令）
├── README.md                        # 项目概览文档（即本文档）
└── LICENSE                          # MIT 许可证文本
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于报告问题、提交代码、完善文档或推荐新的优质资源。请遵循以下步骤参与协作：

1.  **查阅现有议题**：在提交新议题前，请先浏览 GitHub Issues 列表，确认是否已有相似讨论或解决方案。若发现重复议题，可在原议题下补充您的上下文信息。

2.  **派生仓库并创建特性分支**：从主仓库派生（Fork）至个人账户，然后克隆至本地。请基于 `main` 分支创建一个新的特性分支（例如 `feat/add-health-check-retry` 或 `docs/update-resources-schema`），避免在主分支上直接修改。

3.  **编写测试与更新文档**：任何功能新增或缺陷修复，请同步编写对应的单元测试用例。若涉及用户可见的行为变更，必须更新 `docs/` 目录下的相关文档，并在资源示例中添加必要的注释。

4.  **提交变更并发起拉取请求**：提交信息请遵循约定式提交规范（如 `feat: 支持自定义探测间隔` 或 `fix: 修复 YAML 解析特殊字符转义问题`）。推送分支后，通过 GitHub 界面发起 Pull Request 至主仓库的 `main` 分支，并在描述中清晰说明本次变更的目的与影响范围。

5.  **代码审查与合并**：维护者将在 48 小时内进行审查，可能会提出修改意见。请及时响应反馈，若需要协助可 @ 提及核心维护团队。合并后您的提交将自动包含在下一个发布版本中。

## 常见问题

**问：健康探测模块是否会对外部资源造成压力？探测的频率和超时时间如何调整？**

答：ResourcePilot 默认探测间隔为 15 分钟，超时时间设置为 5 秒，仅发送一次 HEAD 请求（若服务器不支持则回退为 GET 请求，但不下载响应体）。此配置对绝大多数标准 Web 服务几乎无感知。您可以通过修改项目根目录下的 `.env` 文件中的 `HEALTH_INTERVAL_MS` 和 `HEALTH_TIMEOUT_MS` 变量来调整探测频率与超时阈值。我们建议生产环境将探测间隔设置为 30 分钟以上，以避免触发目标服务的访问频率限制。

**问：如何添加需要特定请求头或 Cookie 才能访问的资源？**

答：对于需要认证或特定请求头的资源，您可以在 `resources.yaml` 中为对应条目添加 `headers` 字段，以键值对形式传入自定义请求头。例如：

```yaml
- name: 内部仪表板
  url: https://internal.company.com/dashboard
  headers:
    Authorization: Bearer your_token_here
    X-Custom-Header: value
```

请注意，敏感信息（如 Token）建议通过环境变量注入，避免硬编码在配置文件中。您可以在 `src/core/loader.js` 中参考 `process.env` 的替换逻辑。

**问：ResourcePilot 能否同时管理多个不同环境的资源列表（如开发、测试、生产）？**

答：可以。我们推荐使用不同的配置文件来区分环境，例如 `resources.dev.yaml`、`resources.test.yaml`、`resources.prod.yaml`。您可以通过启动参数或环境变量 `RESOURCE_CONFIG_PATH` 来指定加载哪个文件。在 CI/CD 流水线中，您也可以利用构建工具（如 webpack 或 vite）的条件编译功能，在构建阶段选择对应的配置进行打包，从而实现环境隔离。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:01
