# Nova Index

Nova Index 是一个面向技术内容创作者、本地化团队与数字档案管理者的高密度外链资源整合框架。该项目并非传统的爬虫或采集系统，而是一套基于静态标记与人工审核规则的 URL 治理方案，旨在解决多源、多语言、多时效性外链资源的归类、去重、可用性标记与批量导出问题。Nova Index 适合需要定期整理大量媒体类链接、分发至不同下游系统（如 CMS、自动化测试环境、翻译工作台）的工程团队，亦可用于个人知识库中的链接生命周期管理。

本项目不提供任何形式的代理、破解或盗版内容访问服务，仅对用户主动提交的公开链接执行格式规整、元数据补充与状态监控。所有收录的链接均视为外部参考资源，其可访问性与内容合法性由原始域名持有方负责。

## 功能概览

- **批量链接规整器**：自动检测用户粘贴或文件导入的 URL 列表，去除末尾多余斜杠、统一协议大小写、识别裸域名并保留原始输入格式，输出符合 RFC 3986 的标准化条目。
- **域名状态探活**：对收录的每个域名执行定时 HEAD 请求，记录响应码、DNS 解析耗时与 SSL 证书有效期，生成可用性趋势表格。
- **分类标签引擎**：基于域名关键词（如 shipin、zimu、rihan、wuyefuli）自动打标，支持用户自定义正则规则覆盖，便于后续按主题筛选导出。
- **变更审计日志**：记录每条链接的首次收录时间、最近修改人、状态变更原因，支持回滚至任意历史版本。
- **多格式导出器**：支持将当前索引导出为 JSON、CSV、YAML 或纯文本列表，适配不同下游工具的输入要求。
- **冲突检测与去重**：基于标准化后的主机名与路径进行相似度计算，提示可能重复或高度近似的条目，避免冗余维护。
- **只读镜像发布**：可将当前索引编译为静态 HTML 表格，供内部团队或合作伙伴查阅，不暴露后台管理接口。

## 应用场景

- **内容聚合站点的编辑后台**：编辑团队每日收到数十个新增外链投稿，需在发布前统一核对域名可用性、分类并标记语言属性。Nova Index 的规整器与探活功能可将这一流程从 20 分钟压缩至 2 分钟。
- **本地化翻译项目的术语对照库**：翻译项目经理需要维护术语查询链接、参考视频源与字幕文件地址。Nova Index 的标签引擎可根据域名后缀快速区分中文、日文、双语资源，便于分配给不同语种的译员。
- **个人知识库的“阅读清单”管理**：研究者或开发者收藏了大量在线视频教程与文档站，但经常遇到链接失效。Nova Index 的定时探活与变更日志可帮助定期清理死链，并记录收藏时的上下文备注。
- **自动化测试环境中的测试数据源**：QA 团队需构造包含各类域名格式的测试集，以验证应用对外链的解析鲁棒性。Nova Index 的导出器可快速生成包含正常、不规范、带端口、带路径的多样化样本集。
- **合规审计前的链接盘点**：法务或合规部门要求对业务系统中引用的所有第三方链接进行备案。Nova Index 的审计日志与分类导出能力可协助快速生成台账报告。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，需已安装 Git 与 Node.js 18+。

```bash
# 1. 克隆仓库
git clone https://github.com/novaindex/novaindex.git
cd novaindex

# 2. 安装依赖
npm install

# 3. 运行初始化规整流程（示例数据）
npm run init -- --input ./samples/raw_links.txt --output ./output/normalized.json

# 4. 启动本地探活服务（默认端口 3000）
npm run health:check

# 5. 生成静态镜像站点（输出至 ./dist）
npm run build:mirror
```

如需在 Docker 环境中运行，请参阅 `./deploy/docker-compose.yml` 示例。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Node.js | 18.x LTS 或 20.x | 运行时基础，用于执行规整器、探活脚本与构建工具 |
| npm | 9.x 或 10.x | 依赖管理与任务脚本执行 |
| Git | 2.30+ | 用于克隆仓库与版本回溯 |
| 网络访问 | 出方向 80/443 开放 | 探活功能需对外部域名发起 HTTP/HTTPS 请求 |
| 磁盘空间 | 建议 500 MB 以上 | 用于存储日志、缓存与导出的历史快照 |
| 内存 | 推荐 2 GB 以上 | 处理超过 10 万条链接时需调高 Node.js 内存限制 |

可选依赖：Docker 24+（用于容器化部署）、nginx 或 Apache（用于托管生成的静态镜像）。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user/quick-start.md` | 如何安装、配置、第一次运行规整与探活？ |
| 管理员手册 | `docs/admin/health-check.md` | 如何调整探活超时阈值、配置钉钉/邮件告警？ |
| 规则编写 | `docs/rules/tagging-guide.md` | 如何为正则打标规则增加新的关键词组？ |
| 导出格式 | `docs/export/formats.md` | JSON、CSV、YAML 的字段映射与示例文件在哪？ |
| 故障排查 | `docs/troubleshooting/dns-issues.md` | 部分域名解析失败或超时，如何绕过或重试？ |
| 开发指南 | `docs/dev/architecture.md` | 核心模块（parser、prober、logger）的类图与接口说明 |

## 资源列表

### 视频播放类资源

- <code>zhongwenshipinzaixianguankanf.org.cn</code>
- <code>shipinmianfeizaixianguankanf.org.cn</code>
- <code>rimanzaixianguankanf.org.cn</code>

### 日韩双语字幕类资源

- <code>rihanzaixianmianfeishipinf.org.cn</code>
- <code>zhongwenzimumianfeibofangf.org.cn</code>

### 热门系列与福利类资源

- <code>renqixiliezhongwenzimuf.org.cn</code>
- <code>wuyefulizhibof.org.cn</code>

以上链接均按用户原始输入原样收录，未做任何协议补全或域名规范化改写。实际使用中建议配合 Nova Index 的探活功能定期检查各域名的可访问状态。

## 项目结构

```
novaindex/
├── bin/                          # 可执行入口脚本
│   └── cli.js                    # 命令行主程序 (规整/探活/导出)
├── config/                       # 配置文件目录
│   ├── default.yaml              # 默认超时、重试、并发数设置
│   └── tags.yaml                 # 自定义标签正则规则库
├── src/
│   ├── core/
│   │   ├── parser.js             # 链接解析与规整核心逻辑 (含裸域名处理)
│   │   ├── prober.js             # 基于 node:http 的异步探活模块
│   │   └── deduper.js            # 相似度去重与冲突报告生成器
│   ├── export/
│   │   ├── jsonExporter.js       # JSON 格式化输出 (含元数据)
│   │   └── csvExporter.js        # CSV 扁平化导出，适配 Excel
│   ├── logger/
│   │   ├── audit.js              # 审计日志写入 (JSON Lines 格式)
│   │   └── rotator.js            # 日志按日期轮转与压缩
│   └── mirror/
│       └── generator.js          # 从索引生成静态 HTML 表格
├── samples/                      # 示例数据与测试用例
│   ├── raw_links.txt             # 原始待规整链接样例 (含不规范格式)
│   └── expected.json             # 规整后预期输出 (用于单元测试)
├── tests/                        # 单元测试与集成测试 (Jest)
│   ├── parser.test.js
│   └── prober.test.js
├── deploy/                       # 部署相关文件
│   ├── docker-compose.yml        # 含探活服务 + 静态 Nginx 镜像
│   └── nginx.conf                # 镜像站点的缓存与 CORS 配置
├── docs/                         # 完整文档 (见文档导航章节)
├── .github/
│   └── workflows/                # CI 流水线 (lint + test + build)
│       └── main.yml
├── package.json                  # npm 依赖与脚本定义
├── README.md                     # 本文件
└── LICENSE                       # MIT 许可证
```

## 贡献指南

1. **提出议题**：在 GitHub Issues 中描述你希望增加的功能、发现的缺陷或文档改进点。请使用提供的模板，并附上最小复现步骤或用例链接。
2. **分支开发**：从 `main` 分支签出 `feature/xxx` 或 `fix/xxx` 分支。提交信息请遵循 Conventional Commits 规范（如 `feat: add retry policy for timeout`）。
3. **补充测试**：所有核心逻辑（解析、探活、去重）的改动需在 `tests/` 下增加或更新对应的单元测试，确保覆盖率不低于 85%。
4. **更新文档**：若新增配置项或导出格式，请同步修改 `docs/` 下对应的手册，并在 `README.md` 的文档导航表格中增加条目。
5. **提交拉取请求**：PR 描述中需关联议题编号，并附上本地运行 `npm run test` 与 `npm run lint` 的截图或日志。CI 通过后由至少一位维护者审核。

## 常见问题

**Q: 探活服务频繁超时或返回 503，是否会影响其他正常域名的检测？**

A: Nova Index 的探活模块默认使用并发池控制（默认 10 个并发），并独立捕获每个域名的错误。单个域名超时或 5xx 不会阻塞队列，但会记录失败原因至审计日志。若大量域名集中超时，建议检查网络出口防火墙策略，或调大 `config/default.yaml` 中的 `timeout` 和 `retryDelay` 参数。

**Q: 我提交的原始链接中有的带路径（如 abc.com/path/video），有的带查询参数，规整器会如何处理？**

A: 规整器会保留完整的路径与查询字符串，不会移除或编码。唯一强制处理的是尾部斜杠（统一删除）以及协议大小写（转为小写）。对于裸域名（如 `<code>zhongwenshipinzaixianguankanf.org.cn</code>`），规整器不会补任何协议，完全保留用户原始输入。这一设计是为了确保导出结果与用户预期严格一致。

**Q: 静态镜像站点是否支持搜索或按标签过滤？**

A: 当前生成的静态 HTML 表格仅提供基本的排序与分页功能。如需高级检索，建议将导出的 JSON 文件导入至 Elasticsearch 或 Algolia 等搜索引擎中。Nova Index 本身定位为索引治理工具，而非前端展示平台。

## 许可证

MIT License

Copyright (c) 2026 Nova Index Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:29
