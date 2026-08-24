# RZSource Navigator

RZSource Navigator 是一个面向中文互联网技术内容创作者、开源项目维护者及信息聚合平台运营者的外链资源导航与元数据管理工具。该项目旨在解决分散在网络各处的优质技术文档、社区论坛、在线工具及媒体资源难以统一归类、实时可用性监测困难的问题，通过结构化的资源清单管理与简洁的本地运维方式，帮助用户建立可维护、可分享的外链资源目录。

本项目定位为轻量级资源外链汇总站，不依赖外部数据库，所有资源记录以纯文本与 Markdown 格式存储，便于版本控制与协作。目标用户包括个人博客作者、小型团队文档维护者、开源社区布道师以及技术课程资料整理人员。

## 功能概览

- **资源条目结构化存储**：支持按类别、语种、资源类型对链接进行多维度标记，所有记录保存在单一 Markdown 文件中，便于人工审阅与脚本解析。
- **可用性自动化检查**：内置基于 curl 的简易健康检查脚本，可定时探测每个外链的 HTTP 状态码，自动标记异常链接并生成报告。
- **静态页面模板渲染**：提供可选的静态 HTML 生成器，将资源清单渲染为响应式导航页面，适合托管于 GitHub Pages 或任何 Web 服务器。
- **标签与全文检索**：支持基于 grep 的轻量级本地检索，可按关键字、域名后缀或描述文本快速筛选目标资源。
- **变更历史追踪**：依托 Git 提交记录，所有增删改操作均有日志，便于回溯误操作或恢复旧版本数据。
- **多用户协作支持**：资源清单文件采用清晰的行级格式，减少合并冲突概率，适合多人通过 Pull Request 方式共同维护。
- **导出与订阅功能**：可将资源列表导出为 JSON 或 OPML 格式，便于导入其他阅读器或导航工具。

## 应用场景

- **技术博客外链整理**：技术博主可将长期积累的参考文献、官方文档、工具站链接统一纳入 RZSource Navigator 管理，并在博客页面中嵌入生成的导航页，方便读者快速查阅。
- **开源项目文档中心**：开源项目维护者可使用本工具维护项目相关的依赖站点、API 参考、社区论坛等外部链接，避免重要资源散落在 README 或 Wiki 中难以维护。
- **在线课程资料汇总**：教育机构或独立讲师可将课程涉及的视频平台、在线编译器、代码托管仓库等资源集中管理，生成静态页面供学员访问，降低信息获取门槛。
- **企业内部技术周报**：技术团队可每周更新资源清单，收录行业动态、新发布工具或安全公告，形成团队知识沉淀的一部分。

## 快速开始

以下命令适用于 Linux 及 macOS 环境，Windows 用户建议使用 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/rzsource/navigator.git
cd navigator

# 安装依赖（核心脚本使用 bash 和 curl，无需额外依赖；若需静态生成，请安装 Node.js）
npm install --only=production

# 运行资源健康检查
bash scripts/check_health.sh resources/index.md

# 启动本地开发服务器（用于预览静态导航页）
npm run dev
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Bash | 4.0 及以上 | 用于运行健康检查脚本及辅助工具链 |
| curl | 7.68 及以上 | 执行 HTTP 探测及资源下载任务 |
| Git | 2.25 及以上 | 用于版本控制和协作提交 |
| Node.js | 16.0 及以上 | 仅当使用静态页面渲染或导出功能时需要 |
| npm | 7.0 及以上 | 管理前端构建工具及样式打包 |
| grep | 3.0 及以上 | 用于本地检索及日志过滤 |
| sed | 4.0 及以上 | 用于自动化编辑资源清单字段 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide.md | 如何增删改资源条目、如何运行健康检查、如何生成导航页 |
| 维护者指南 | docs/maintainer-guide.md | 如何审核 Pull Request、如何更新类别体系、如何处理冲突 |
| 模板语法参考 | docs/template-syntax.md | 静态页面渲染支持哪些变量、如何自定义样式与布局 |
| 脚本 API 说明 | docs/script-api.md | 各个 bash 脚本的入口参数、环境变量及返回值含义 |
| 设计决策记录 | docs/design-decisions.md | 为何选择纯文本存储、为何不采用数据库、后续演进计划 |

## 资源列表

本节收录本项目当前维护的全部外链资源，按类别分组展示。所有链接均按照用户提供的原始格式原样列出，未做任何协议补全、域名变更或路径修改。

### 在线视频与媒体类

<code>rimanzaixianguankana.org.cn</code>

<code>rihanzaixianmianfeishipina.org.cn</code>

<code>zhongwenzimumianfeibofanga.org.cn</code>

<code>renqixiliezhongwenzimua.org.cn</code>

<code>wuyefulizhiboa.org.cn</code>

<code>lalalazhongwendianshijua.org.cn</code>

<code>yinghuadongmanguanfangbana.org.cn</code>

## 项目结构

```
.
├── README.md                     # 项目首页及整体说明
├── LICENSE                       # MIT 许可证文本
├── package.json                  # Node.js 项目配置与构建脚本
├── .gitignore                    # Git 忽略规则
├── config/
│   └── categories.toml           # 资源分类映射表，可自定义扩展
├── scripts/
│   ├── check_health.sh           # 主健康检查脚本，遍历清单并记录状态
│   ├── export_json.sh            # 将 Markdown 清单导出为 JSON 格式
│   ├── export_opml.sh            # 导出为 OPML 订阅格式
│   └── utils.sh                  # 通用函数库，含日志及颜色输出
├── resources/
│   └── index.md                  # 核心资源清单文件，所有链接记录于此
├── src/
│   ├── render.js                 # 静态页面渲染入口
│   ├── parser.js                 # 解析 index.md 为内存数据结构
│   └── templates/
│       ├── base.html             # 基础 HTML 模板，含响应式框架
│       └── partials/             # 可复用的页眉、页脚、导航组件
├── public/
│   ├── css/
│   │   └── style.css             # 导航页样式，支持深色模式
│   └── dist/                     # 构建后的静态输出目录（自动生成）
├── tests/
│   ├── test_parser.sh            # 单元测试：解析器正确性验证
│   └── test_health.sh            # 模拟检查脚本的异常场景测试
└── docs/
    ├── user-guide.md             # 用户手册
    ├── maintainer-guide.md       # 维护者指南
    ├── template-syntax.md        # 模板语法说明
    ├── script-api.md             # 脚本 API 文档
    └── design-decisions.md       # 设计决策记录
```

## 贡献指南

我们欢迎各类形式的贡献，包括但不限于新增资源链接、修复健康检查脚本缺陷、完善文档或提交样式改进。请遵循以下步骤参与协作。

1. 复刻本项目仓库至个人账号，并在本地克隆复刻版本，确保远程 upstream 指向原始仓库以便同步更新。
2. 新建特性分支，分支名称简要描述本次变更内容，例如 `feat/add-video-category` 或 `fix/check-timeout`。
3. 在 `resources/index.md` 中依照现有格式添加或修改资源条目，保证每行包含类别、名称、URL 及简短描述，并以 Tab 分隔各字段。
4. 在本地运行 `bash scripts/check_health.sh resources/index.md` 确保新增链接可访问，且现有链接状态无退化；若新增链接无法通过检查，请补充备注说明。
5. 提交变更并推送至个人复刻，随后向原始仓库发起 Pull Request，PR 描述中需明确列出变更列表及测试结果概要。

## 常见问题

**问：健康检查脚本提示超时或连接拒绝，但浏览器可以正常访问该链接，该如何处理？**

答：部分站点可能对 curl 的 User-Agent 或 TLS 版本有特定要求。您可以在 `scripts/utils.sh` 中调整 `CURL_OPTS` 变量，添加 `--user-agent "Mozilla/5.0"` 或 `--tlsv1.2` 等参数。若仍失败，可考虑为该链接单独配置更长的超时时间（编辑 `check_health.sh` 中的 `--max-time` 参数）。请注意，本工具仅执行基础连通性检测，不替代完整的业务层可用性监控。

**问：静态导航页生成后，如何部署到公网？**

答：执行 `npm run build` 后，所有静态文件位于 `public/dist` 目录。您可以将该目录内容上传至任意静态托管服务，如 GitHub Pages、Cloudflare Pages 或 Nginx 服务器。推荐使用 GitHub Actions 自动化构建部署，相关配置示例位于 `.github/workflows/deploy.yml`（需自行启用）。

**问：资源清单中能否包含非 HTTP 协议的资源，例如 magnet 链接或 FTP 地址？**

答：可以。本工具对 URL 协议不做强制校验，但健康检查脚本仅对 `http://` 及 `https://` 链接执行探测。对于其他协议，条目仍可正常显示在导航页中，只是检查结果会标记为 `skipped`。您可在描述字段中注明访问方式。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:04
