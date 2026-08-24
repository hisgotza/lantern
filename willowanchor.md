# ReelFlow 技术资源导航站

ReelFlow 是一个面向开发人员、技术研究人员及内容分析工程师的轻量级外链资源聚合与导航系统。项目定位于技术信息的中转枢纽，通过结构化分类与极简交互，帮助用户从海量网络资源中快速定位高价值技术文档、视频素材、在线工具与社区讨论入口。本项目不生产内容，不存储数据，仅提供经过人工筛选与稳定性测试的外部链接索引，适用于构建个人或团队内部的技术收藏夹、自动化资源监控系统的数据源，以及各类自动化测试脚本的种子 URL 集合。

ReelFlow 解决了技术研究过程中资源分散、链接失效快、检索成本高的问题。通过统一的门户页面与机器可读的配置输出，用户可将本项目作为信息获取的起点，配合定期链接健康检查机制，显著降低维护外部资源列表的负担。

## 功能概览

- 按技术领域分类的资源索引：将外链按开发语言、视频编码、在线播放器调试、字幕工程、流媒体协议测试等维度进行归类，支持快速筛选。

- 链接状态自动检测集成：项目内置周期性 HTTP 状态码检查脚本，可标记异常链接并生成健康报告，便于管理员及时更新或下线失效资源。

- 轻量级 Web 展示面板：提供纯 HTML/CSS 响应式前端页面，展示所有分类链接，支持关键字模糊搜索和按标签过滤。

- 机器可读数据输出：支持将资源列表导出为 JSON、YAML 或 CSV 格式，方便其他自动化工具或监控平台调用。

- 链接变更历史记录：每次更新资源列表时自动生成变更日志（Change Log），记录新增、删除或修改的 URL，便于团队审计。

- 自定义分类标签管理：允许管理员通过配置文件动态添加、删除或重命名分类标签，无需修改核心代码。

- 嵌入外部页面预览模式：通过 iframe 或 WebView 方式，在导航站内直接预览目标页面内容（需目标站点允许同源策略或配置代理）。

## 应用场景

- 技术文档收藏与分发：开发团队可将日常高频使用的 API 文档、框架教程、视频教学资源统一收录于 ReelFlow，新成员入职时通过导航站即可获得完整学习路径，无需反复询问。

- 在线视频播放测试环境：测试工程师可使用项目中收录的在线视频播放链接（如各类流媒体测试页面），验证播放器的兼容性、字幕加载速度和多码率切换功能。

- 自动化监控脚本的数据源：运维人员可编写定期爬取脚本，以 ReelFlow 输出的 JSON 资源列表为基础，对每个链接进行可达性、响应时间和内容哈希值检查，实现外部依赖的主动监控。

- 学术研究与内容分析：研究人员可利用导航站中的字幕资源链接与视频播放链接，构建小规模语料库，用于自然语言处理或视频内容元数据分析实验。

## 快速开始

以下命令适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 1. 克隆项目仓库
git clone https://github.com/your-org/reelflow-navigator.git
cd reelflow-navigator

# 2. 安装依赖（Python 3.9+ 环境）
pip install -r requirements.txt

# 3. 初始化配置文件
cp config/default.yaml config/production.yaml
# 编辑 production.yaml 填写项目根路径、监听端口、资源更新周期等

# 4. 运行本地开发服务器
python app.py --port 8080

# 5. （可选）执行首次链接健康检查
python scripts/health_check.py --config config/production.yaml --output report.html
```

## 安装要求

| 依赖项目 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心后端运行环境，用于提供 Web 服务及脚本工具 |
| Flask | 2.2.x | Web 框架，用于呈现导航面板和 REST API 接口 |
| PyYAML | 6.0 | 用于解析 YAML 格式的配置文件及资源列表 |
| requests | 2.31.x | 发送 HTTP 请求，用于链接健康检查与状态码获取 |
| beautifulsoup4 | 4.12.x | 可选依赖，用于解析外部页面标题和描述，增强链接预览信息 |
| schedule | 1.2.x | 可选依赖，用于定时触发链接健康检查任务 |
| pytest | 7.4.x | 仅开发环境需要，用于运行单元测试和集成测试 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide/getting-started.md | 如何配置首次启动、如何添加第一个资源链接、如何访问 Web 面板 |
| 管理员手册 | docs/admin/configuration.md | 所有配置项的含义、默认值、修改方式，以及如何调优健康检查参数 |
| 开发参考 | docs/developer/api-endpoints.md | REST API 的完整端点列表、请求/响应格式、鉴权方式（如有） |
| 运维指南 | docs/ops/deployment.md | 使用 Docker、Nginx 或 Systemd 进行生产环境部署的详细步骤 |
| 贡献规范 | docs/contributing/coding-standards.md | 代码风格、提交信息格式、Pull Request 流程和测试覆盖率要求 |
| 故障排除 | docs/troubleshooting/common-issues.md | 常见启动错误、链接检查超时处理、端口冲突解决方法 |

## 资源列表

本导航站收录的外部链接均按功能与内容主题进行分组。所有链接均来自用户原始数据，原样列出。

视频播放与字幕资源

- <code>zaixianshipinzhongwenzimud.org.cn</code>

- <code>zaixianbofangzhongwenzimud.org.cn</code>

- <code>zhongwenshipinzaixianguankand.org.cn</code>

- <code>shipinmianfeizaixianguankand.org.cn</code>

- <code>rimanzaixianguankand.org.cn</code>

- <code>rihanzaixianmianfeishipind.org.cn</code>

- <code>zhongwenzimumianfeibofangd.org.cn</code>

## 项目结构

```
reelflow-navigator/
├── app.py                      # 主入口，Flask 应用实例及路由注册
├── config/                     # 配置文件目录
│   ├── default.yaml            # 默认配置（端口、日志级别、检查间隔）
│   ├── production.yaml         # 生产环境覆盖配置（不提交至仓库）
│   └── schema.json             # 配置文件 JSON Schema，用于 IDE 校验
├── resources/                  # 资源列表存储目录
│   ├── links.yaml              # 主资源列表，按分类组织 URL
│   ├── links.json              # 由 YAML 转换生成的 JSON 缓存，供 API 调用
│   └── changelog.txt           # 资源变更历史（手动或自动追加）
├── scripts/                    # 工具脚本目录
│   ├── health_check.py         # 链接健康检查主脚本，支持并发请求
│   ├── export_json.py          # 导出资源列表为 JSON 文件
│   ├── import_csv.py           # 从 CSV 批量导入链接，支持去重
│   └── scheduler.py            # 定时任务调度器，调用健康检查并发送告警
├── templates/                  # Jinja2 前端模板目录
│   ├── index.html              # 导航首页，展示所有分类及链接卡片
│   ├── detail.html             # 单个链接详情页（含历史状态）
│   └── report.html             # 健康检查报告展示页
├── static/                     # 静态资源目录
│   ├── css/
│   │   └── style.css           # 响应式布局与暗色主题样式
│   ├── js/
│   │   ├── search.js           # 前端模糊搜索与标签过滤逻辑
│   │   └── chart.js            # 使用 Chart.js 绘制链接可用率趋势图
│   └── favicon.ico             # 站点图标
├── tests/                      # 单元测试与集成测试目录
│   ├── test_health_check.py    # 模拟 HTTP 响应，测试检查脚本逻辑
│   ├── test_api.py             # 测试 REST API 返回数据结构与状态码
│   └── fixtures/               # 测试用固定数据（模拟 links.yaml）
├── docs/                       # 文档目录（结构见上述文档导航）
│   ├── user-guide/
│   ├── admin/
│   ├── developer/
│   ├── ops/
│   ├── contributing/
│   └── troubleshooting/
├── requirements.txt            # 生产环境依赖清单
├── requirements-dev.txt        # 开发环境额外依赖（测试、代码检查工具）
├── Dockerfile                  # 多阶段构建 Docker 镜像文件
├── docker-compose.yml          # 本地开发或简易部署的 Compose 配置
└── README.md                   # 本文件
```

## 贡献指南

1. 提交问题或改进建议前，请先在 Issues 页面搜索是否已有类似讨论。若未找到，可创建新 Issue 并按照模板填写问题描述、复现步骤和预期行为。

2. 若要添加新的外链资源或修改现有分类，请先 Fork 本仓库，在本地 resources/links.yaml 文件中进行修改，并运行 scripts/health_check.py 验证新增链接的可达性。

3. 所有代码变更必须附带相应的单元测试。新增功能需在 tests/ 目录下创建或补充测试用例，确保覆盖率不低于 80%。

4. 提交 Pull Request 前，请确保本地通过全量测试（pytest tests/）且代码风格符合 PEP 8 规范（可使用 black 或 flake8 检查）。PR 描述中需关联相关的 Issue 编号。

5. 若仅更新资源列表而不涉及代码改动，可直接在 PR 中说明链接来源和分类依据，项目维护者会定期审核并合并此类更新。

## 常见问题

Q: 健康检查脚本报告某些链接为异常，但我通过浏览器可以正常访问，为什么？

A: 可能原因包括：目标站点启用了反爬机制（如 User-Agent 校验或 JavaScript 渲染依赖）；健康检查脚本所在的网络环境与您本地不同（例如服务器位于特定地域，遭目标站点防火墙限制）；目标站点临时性故障，但浏览器缓存了旧页面。建议调整 scripts/health_check.py 中的请求头（如增加 User-Agent 或 Referer），或使用 --timeout 参数延长等待时间。

Q: 如何批量导入我自己的收藏夹链接，而不需要逐条手动编辑 YAML 文件？

A: 项目提供了 scripts/import_csv.py 工具。您可将链接、标题、分类标签按列整理为 CSV 文件，然后运行 python scripts/import_csv.py --input bookmarks.csv --output resources/links.yaml，该脚本会自动合并去重并保留原有格式。CSV 首行需包含 url, title, category 三个字段。

Q: 前端搜索框无法找到我新增的链接，即使我已经更新了 links.yaml 并重启了服务。

A: 请检查是否清空了浏览器缓存或使用了无痕模式。另外，前端搜索索引基于 resources/links.json 缓存文件，您需要手动触发一次 export_json.py 脚本生成最新 JSON，或调用 API /api/v1/refresh 端点刷新缓存。如果问题依然存在，请查看静态目录下的 js/search.js 中是否定义了正确的数据源路径。

## 许可证

MIT License

Copyright (c) 2026 ReelFlow Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
