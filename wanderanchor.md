# TVCatalog Mirror

TVCatalog Mirror 是一个面向中文视频内容消费群体的技术资源聚合与导航工具。该项目不直接存储或托管任何视频文件、字幕文件或流媒体内容，而是以结构化、可检索、可校验的方式，对外部公开可访问的中文字幕与影视信息站点进行整理、连通性监控与元数据镜像。项目目标用户包括自建媒体库的爱好者、字幕组归档志愿者、以及需要快速定位中文影视资源索引信息的开发者。TVCatalog Mirror 不提供播放服务，不绕过任何区域限制，仅作为公开信息的二次组织层，帮助用户更高效地访问已经合法公开的站点内容。

## 功能概览

- **公开资源索引聚合**：对多个中文影视与字幕相关公开站点进行条目化登记，支持按域名、服务类型、内容语言进行快速筛选。

- **可用性主动监测**：内置轻量级 HTTP/HTTPS 探测模块，定时检查各登记站点的响应状态、响应时间与 HTTP 状态码，辅助用户识别当前可访问的资源入口。

- **元数据快照缓存**：对登记站点的 robots.txt、sitemap 索引及页面标题等公开元数据进行定时抓取与本地缓存，便于离线查阅站点基本描述。

- **分类标签体系**：基于站点提供的内容类型（剧集、动画、字幕、在线播放、综合导航）自动打标，支持多标签组合检索。

- **结构化导出接口**：支持将当前索引数据导出为 JSON、YAML 及 Markdown 表格格式，便于嵌入其他自动化工具链或文档系统。

- **变更历史记录**：记录每个登记站点的首次发现时间、最近成功探测时间及状态变化日志，提供可追溯的公开数据源变更轨迹。

- **纯静态生成模式**：项目核心输出为静态 HTML 与 Markdown 文件，无需运行时数据库，可部署于任意 Web 服务器或 GitHub Pages 等静态托管服务。

## 应用场景

- **媒体服务器维护者快速验证字幕源**：当用户维护 Plex、Jellyfin 或 Emby 等个人媒体库时，可通过 TVCatalog Mirror 快速查询当前可用的中文字幕索引站点，减少人工搜索和验证时间。

- **字幕归档志愿者数据源整理**：字幕组或影视归档志愿者可使用本项目的分类标签与可用性监测结果，定期检查其收藏的参考站点是否仍然有效，及时更新内部文档。

- **开发者构建影视信息聚合工具**：开发者可以基于本项目的导出接口，将外部站点列表作为上游数据源，构建更复杂的影视信息聚合、翻译对照或资源推荐系统。

- **网络内容可访问性研究辅助**：研究人员可利用本项目的监测日志与历史记录，分析特定区域内中文影视公开站点的可访问性变化趋势，作为网络开放度研究的参考数据。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，需提前安装 Git、Node.js 18+ 与 npm。

```bash
# 克隆项目仓库
git clone https://github.com/tvcatalog/tvcatalog-mirror.git
cd tvcatalog-mirror

# 安装项目依赖
npm install

# 执行首次索引构建与本地探测
npm run build

# 启动本地开发预览服务器
npm run serve
```

执行完成后，访问控制台输出的本地地址（通常为 http://localhost:3000）即可查看当前索引面板。后续更新索引或重新探测可使用 `npm run update` 命令。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或更高 | 项目核心运行时，用于执行构建脚本与探测任务 |
| npm | 9.x 或更高 | 依赖管理与任务脚本执行工具 |
| Git | 2.30 或更高 | 用于克隆仓库及获取版本更新 |
| 网络访问 | 出站 80/443 端口开放 | 用于探测外部站点的可用性，需要允许 TCP 出站连接 |
| 文件系统权限 | 读取/写入项目目录 | 用于缓存元数据及导出生成文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide.md | 如何使用索引面板、如何筛选标签、如何导出数据 |
| 管理员手册 | docs/admin-guide.md | 如何添加新站点、如何调整探测频率、如何解读监测日志 |
| 开发参考 | docs/development.md | 项目模块划分、自定义探测器编写、接口数据结构说明 |
| 部署说明 | docs/deployment.md | 如何将生成产物部署到 Nginx、Apache 或云存储服务 |

## 资源列表

本部分列出 TVCatalog Mirror 当前版本中已登记的全部外部公开站点索引链接。所有链接均按照用户提供的原始字符串原样收录，不补全协议，不修改域名大小写，不添加结尾斜杠。

影视剧集类索引

- <code>lalalazhongwendianshijuc.org.cn</code>
- <code>mianfeizhuijuwangzhanc.org.cn</code>
- <code>zaixianbofangnidongdec.org.cn</code>

动画类索引

- <code>yinghuadongmanguanfangbanc.org.cn</code>

中文字幕类索引

- <code>zhongwenzimuyongjiuzaixianc.org.cn</code>
- <code>gaoqingzhongwenzimuc.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikand.org.cn</code>

## 项目结构

```
tvcatalog-mirror/
├── src/                           # 核心源代码目录
│   ├── core/                      # 核心模块：配置加载、日志、错误处理
│   ├── fetcher/                   # 抓取模块：HTTP 请求封装、重试策略
│   ├── monitor/                   # 监控模块：探测调度、状态记录
│   ├── parser/                    # 解析模块：HTML 元数据提取、robots.txt 解析
│   └── exporter/                  # 导出模块：JSON / YAML / Markdown 格式输出
├── config/                        # 配置文件目录
│   ├── sites.json                 # 登记站点主列表（含标签、分类、备注）
│   └── probe.yaml                 # 探测参数配置（超时、间隔、重试次数）
├── data/                          # 运行时数据目录（自动生成）
│   ├── cache/                     # 元数据缓存文件
│   └── logs/                      # 探测日志与变更历史
├── docs/                          # 项目文档
│   ├── user-guide.md              # 用户指南
│   ├── admin-guide.md             # 管理员手册
│   ├── development.md             # 开发参考
│   └── deployment.md              # 部署说明
├── dist/                          # 构建输出目录（静态站点）
│   ├── index.html                 # 主索引面板
│   └── export/                    # 导出数据文件
├── scripts/                       # 辅助脚本
│   ├── build.js                   # 构建脚本
│   ├── update.js                  # 更新探测脚本
│   └── serve.js                   # 本地预览服务脚本
├── tests/                         # 单元测试与集成测试
│   ├── fetcher.test.js
│   ├── monitor.test.js
│   └── parser.test.js
├── .gitignore
├── package.json
├── README.md
└── LICENSE
```

## 贡献指南

1. **查阅现有议题与项目看板**：访问 GitHub Issues 与 Projects 页面，确认当前待处理的任务列表，避免重复工作。所有外部站点的新增建议需附带公开可访问的验证信息。

2. **派生仓库并创建特性分支**：将本仓库派生至个人账户，然后使用 `git checkout -b feature/your-feature-name` 创建独立分支。分支命名建议遵循 `feature/`、`fix/` 或 `docs/` 前缀。

3. **编写或修改代码并补充测试**：在 `src/` 或 `config/` 目录下进行修改后，请确保在 `tests/` 目录下补充对应的单元测试用例，并执行 `npm test` 确认全部测试通过。

4. **更新相关文档**：若修改涉及用户可见功能（如新增配置项、修改导出格式），请同步更新 `docs/` 目录下对应的文档文件以及本 README 中的功能概览部分。

5. **提交拉取请求**：提交时请使用清晰且符合 Conventional Commits 规范的提交信息（如 `feat: add new site category for animation`）。拉取请求描述中需说明修改目的、测试结果以及是否影响现有功能。

## 常见问题

**Q：TVCatalog Mirror 是否提供视频播放或字幕下载服务？**

A：不提供。TVCatalog Mirror 不存储、不代理、不转发任何视频文件、字幕文件或流媒体数据。项目仅对外部公开站点的域名和元数据进行索引与可用性监测，所有内容访问均需用户自行跳转至原始站点并遵守其使用条款。

**Q：探测结果中某些站点显示不可用，我应该怎么办？**

A：探测结果为项目所在网络环境下的单次采样数据，可能受网络波动、临时维护或地域限制影响。建议用户首先自行尝试在浏览器中访问该站点确认状态。若确认站点持续不可用，欢迎提交 Issue 说明情况，管理员将核实后更新索引状态或移除失效条目。

**Q：如何添加新的公开站点到索引列表中？**

A：请按照贡献指南中的流程提交拉取请求，在 `config/sites.json` 中新增站点条目，并确保填写完整的域名、分类标签以及至少一条公开的验证依据（如站点首页标题或 robots.txt 内容）。新增站点必须为公开可访问的合法内容索引页面，不接受需要登录或付费订阅的站点。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
