# Yingshi Resource Index

Yingshi Resource Index is a community-driven, curated directory of high-availability streaming and subtitle resources for Chinese-speaking audiences worldwide. Unlike conventional search engines or media aggregators, this project does not host, transcode, or redistribute any copyrighted content. Instead, it maintains a rigorously tested, manually verified list of domain names and online resources that provide Chinese subtitles, high-definition playback, and on-demand streaming for international films, television series, and anime.

This project targets advanced end-users, media center administrators, and developers who require reliable fallback endpoints for media discovery. It solves the fundamental problem of link rot and domain seizure that plagues the online streaming ecosystem by providing a structured, version-controlled index that can be integrated into automation scripts, proxy routing tables, or browser bookmark hierarchies. Every entry in the index undergoes periodic reachability testing, and deprecated entries are removed or flagged within 48 hours of detection. The project is not a search portal, not a player, and not a piracy tool; it is a reference implementation of resilient resource discovery for media-savvy technical operators.

## 功能概览

- **Curated Domain Registry** – Maintains a categorized list of active streaming and subtitle domains, each with last-verified timestamps and geographic accessibility hints.

- **Automated Health Check Scripts** – Includes Python and shell utilities that perform ICMP, TCP, and HTTP HEAD checks against each listed domain, generating machine-readable JSON reports.

- **Plain-Text Export Modes** – Supports output as plain domain lists, hosts-file compatible entries, or dnsmasq upstream configurations for seamless integration with local DNS forwarders.

- **Tag-Based Classification System** – Each resource is tagged with primary language (Simplified/Traditional Chinese), content type (movies, TV, anime, documentaries), and player compatibility (HLS, MPEG-DASH, direct MP4).

- **Historical Archive** – Retains up to six months of domain status snapshots, enabling trend analysis of provider uptime and regional blocking patterns.

- **User-Submitted Endpoint Queue** – Provides a GitHub Issues template for users to suggest new domains, with automated preliminary validation before maintainer review.

- **Offline-Friendly Cache** – Generates a static HTML mirror of the index that can be served locally without external dependencies, suitable for air-gapped media servers.

## 应用场景

- **Home Media Server Administration** – System administrators managing Plex, Jellyfin, or Emby instances can use the domain list to populate external subtitle fetcher plugins, ensuring fallback subtitle sources remain functional even when primary providers go offline.

- **Network Penetration Testing for Media Access** – Security researchers and network engineers can leverage the health-check scripts to verify connectivity to media resources across different ASNs and geographic regions, identifying which endpoints remain accessible under various network conditions.

- **Educational Linguistics Research** – Academics studying subtitle timing, translation quality, or character encoding consistency can use the resource index to discover subtitle sources for corpus collection, with clear provenance and retrieval timestamps for reproducibility.

- **Automated Bookmark Synchronization** – Power users can integrate the plain-text domain exports into browser extension workflows that periodically refresh bookmark folders, removing dead links and adding newly verified entries without manual intervention.

## 快速开始

```bash
# Clone the repository with full history
git clone https://github.com/yingshi-resource-index/yri-core.git
cd yri-core

# Install Python dependencies and verification tools
pip install -r requirements.txt
pip install --editable .

# Run the initial full health scan and generate the latest index report
yri-scan --full --output-dir ./reports
yri-generate --format markdown --input ./reports/latest.json --output ./README.generated.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 或更高 | 核心扫描引擎与数据聚合脚本均基于 Python 开发 |
| pip | 21.0 或更高 | 用于安装 requirements.txt 中声明的全部第三方库 |
| curl | 7.68 或更高 | 部分备用健康检查脚本依赖 curl 进行 HTTPS 探测 |
| git | 2.25 或更高 | 用于克隆仓库、管理提交记录及参与贡献流程 |
| jq | 1.6 或更高 | 命令行 JSON 处理器，用于解析扫描结果和日志文件 |
| Network Connectivity | 出站 80/443 可达 | 所有扫描与验证操作均需对外部域名发起标准 HTTP/HTTPS 请求 |
| cron / systemd-timer | 任意版本（可选） | 用于部署自动化定时扫描任务，非强制但强烈建议 |

## 文档导航

| 层面 | 目录文件 | 回答的问题 |
|---|---|---|
| 用户入门 | <code>docs/quick-start.md</code> | 如何获取最新可用资源列表、如何阅读分类标签、如何提交反馈 |
| 运维部署 | <code>docs/deployment-guide.md</code> | 如何将扫描脚本部署为定时任务、如何配置邮件告警、如何自定义超时阈值 |
| 开发者参考 | <code>docs/api-reference.md</code> | 扫描器 CLI 参数详解、JSON 报告结构说明、插件扩展接口定义 |
| 数据格式规范 | <code>docs/data-schema.md</code> | 资源条目字段含义、标记枚举值、版本兼容性承诺及变更历史 |
| 故障排查 | <code>docs/troubleshooting.md</code> | 常见扫描错误码解释、网络环境调试方法、日志级别调整指引 |

## 资源列表

以下列表包含本项目当前索引的全部原始资源链接。所有条目均按用户提供的原始字符串原样收录，未做任何协议补全、域名规范化或格式转换。

流媒体播放类

- <code>yinghuadongmanguanfangbanf.org.cn</code>
- <code>mianfeizhuijuwangzhanf.org.cn</code>
- <code>zaixianbofangnidongdef.org.cn</code>
- <code>jiureshipinzaixianguankan.org.cn</code>

中文字幕资源类

- <code>zhongwenzimuyongjiuzaixianf.org.cn</code>
- <code>gaoqingzhongwenzimuf.org.cn</code>
- <code>renqizhongwenzimusiwa.org.cn</code>

## 项目结构

```
yri-core/
├── src/                                # 核心源代码目录
│   ├── scanner/                        # 健康检查引擎实现
│   │   ├── __init__.py                 # 模块初始化与导出接口
│   │   ├── tcp_probe.py                # TCP 端口连通性探测类
│   │   └── http_parser.py              # HTTP 响应头与状态码解析
│   ├── formatter/                      # 多格式输出生成器
│   │   ├── markdown.py                 # 生成 Markdown 表格与列表
│   │   ├── json_exporter.py            # 输出结构化 JSON 报告
│   │   └── plaintext.py                # 纯文本域名清单（每行一个）
│   └── cli/                            # 命令行接口与参数解析
│       ├── main.py                     # 入口点，路由子命令
│       └── config.py                   # 配置文件加载与合并逻辑
├── tests/                              # 单元测试与集成测试套件
│   ├── test_probe.py                   # 模拟网络异常的探测测试
│   └── fixtures/                       # 测试用的静态 JSON 样本
├── scripts/                            # 运维与辅助脚本
│   ├── daily-scan.sh                   # 每日定时扫描的包装脚本
│   └── archive-rotator.py              # 按月轮转历史快照文件
├── docs/                               # 完整文档体系（详见文档导航）
├── reports/                            # 运行时生成的扫描报告输出目录
│   ├── latest.json                     # 最新一次全量扫描结果
│   └── archive/                        # 按时间戳命名的历史报告归档
├── requirements.txt                    # Python 依赖固定版本清单
├── setup.py                            # 可安装包元数据与入口点定义
└── README.md                           # 项目首页文档（本文件）
```

## 贡献指南

1.  **Fork 仓库并创建特性分支** – 从主仓库派生个人副本，然后使用 <code>git checkout -b feature/your-contribution</code> 创建新分支，避免直接在主分支上修改。

2.  **更新资源列表或扫描逻辑** – 若新增或移除域名，请编辑 <code>data/sources.yaml</code> 文件并附带最近一次验证时间戳；若修改扫描器行为，请同步更新对应的单元测试用例。

3.  **运行完整测试套件** – 执行 <code>pytest tests/</code> 确保全部测试通过，并检查 <code>reports/latest.json</code> 的生成结果是否符合预期格式。

4.  **提交变更并签署开发者来源声明** – 提交信息应遵循约定式提交格式（如 <code>feat: add new subtitle domain</code>），并在 PR 描述中明确声明所有变更均遵守项目许可证条款。

5.  **发起拉取请求** – 将分支推送至个人远端仓库后，通过 GitHub 界面创建 PR，至少等待一位维护者审阅。若 PR 涉及高风险域名变更，需额外提供可达性截图或日志证据。

## 常见问题

**问：项目是否提供在线搜索界面或播放器嵌入功能？**

答：不提供。本项目严格限定为静态资源索引，不包含任何形式的搜索框、播放器组件或内容代理服务。用户需自行将列表中的域名用于外部播放器或字幕下载工具。项目本身不存储、缓存或转发任何媒体文件。

**问：资源列表的更新频率是多少？我如何获取变更通知？**

答：扫描脚本默认每日 02:00（UTC）执行一次全量检查，并在检测到可用性状态变化时生成差异报告。您可以通过 Watch 仓库的 Release 或 Issues 选项卡获取变更通知，也可以订阅 <code>reports/latest.json</code> 的 RSS 转换服务（需自行部署）。我们不提供邮件列表或即时通讯推送。

**问：我发现某个已收录域名无法访问，应该怎么办？**

答：请先通过您本地的 <code>curl -v</code> 或 <code>telnet</code> 命令确认问题并非由您的网络环境导致。若确认失效，请前往 GitHub Issues 提交错误报告，并附上扫描日志片段或 HTTP 状态码。维护者会在 48 小时内复核并将该条目标记为 <code>deprecated</code>，直至其恢复或从活跃列表中移除。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:07
