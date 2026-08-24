# Nova Index

Nova Index 是一个面向开发人员与技术研究者的高质量外链资源聚合系统。该项目不直接托管或存储任何第三方内容，而是通过结构化目录与人工筛选机制，对互联网上分散的、具有特定领域价值的外部资源进行归类与索引。项目定位为技术信息导航中间件，旨在解决信息过载时代下，研究人员、内容分析者与爬虫开发者难以快速定位特定类型公开数据源的问题。通过提供稳定、可机读的资源链接集合，Nova Index 显著降低了个体与小型团队在公开信息采集与样本构建阶段的时间成本。

## 功能概览

- **结构化资源目录**：提供按内容主题、文件类型与更新频率划分的多级索引目录，便于快速筛选目标资源。
- **公开数据源聚合**：聚合涵盖视频样本、图文素材与字幕语料等多类公开可访问的外部链接，适用于算法测试与模型训练。
- **链接可用性标记**：对收录的外部链接进行基础存活状态标记，辅助用户评估资源有效性。
- **原始格式保留**：所有收录链接均以原始域名或原始协议形式呈现，不做任何改写或伪装，确保引用准确性。
- **批次化管理**：采用批次导入机制，当前为第 23/120 批，便于用户追踪资源更新历史与版本差异。
- **纯静态导航架构**：项目本身为纯静态文档结构，无需数据库或后端服务即可完整运行，降低部署与维护复杂度。
- **机器可读输出**：除人类可读的 Markdown 文档外，提供 JSON 与 YAML 格式的资源索引导出，适配自动化脚本与 CI/CD 流程。

## 应用场景

- **自然语言处理语料构建**：研究人员可利用聚合的字幕与文本类资源链接，快速构建多语言字幕语料库，用于机器翻译或语音识别模型的辅助训练。
- **计算机视觉样本采集**：开发人员可依据视频与图像类资源目录，编写自动化采集脚本，获取公开的视频片段或图像素材，用于目标检测或图像分类算法的测试。
- **内容安全策略研究**：安全分析人员可通过索引中的特定类别资源，分析公开网络中的内容分布特征，辅助制定或验证内容过滤策略。
- **数据爬虫开发调试**：爬虫工程师可使用本索引作为初始种子链接集合，快速搭建爬虫原型，验证请求解析逻辑与反爬对抗策略。

## 快速开始

以下命令适用于 Linux 与 macOS 环境，Windows 用户建议通过 WSL 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/novaindex/novaindex.git
cd novaindex

# 2. 安装基础依赖（仅需 Node.js 与 npm）
npm install -g markdown-link-check@3.11.2
npm install -g yaml-cli@0.0.4

# 3. 运行本地索引生成脚本
./scripts/build_index.sh
```

执行完成后，可在 `./dist` 目录下获得生成的 HTML 导航页面、JSON 索引文件与 YAML 格式资源清单。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 16.x 或更高 | 用于运行索引构建脚本与链接检查工具 |
| npm | 7.x 或更高 | 包管理器，用于安装全局工具依赖 |
| Git | 2.25 或更高 | 用于克隆仓库及版本管理 |
| bash | 4.0 或更高 | 用于执行构建脚本（Windows 需 WSL） |
| curl | 7.68 或更高 | 用于构建过程中的链接存活探测 |
| markdown-link-check | 3.11.2 | 可选，用于本地检查链接有效性 |
| yaml-cli | 0.0.4 | 可选，用于生成 YAML 格式索引 |
| Python | 3.8 或更高 | 可选，用于运行辅助数据分析脚本 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | `docs/guide/getting-started.md` | 如何首次使用索引系统、如何理解资源分类体系 |
| 维护指南 | `docs/maintainer/link-update.md` | 如何新增或移除资源链接、如何更新可用性标记 |
| 脚本参考 | `docs/developer/script-api.md` | 构建脚本的输入输出格式、各环境变量含义 |
| 数据格式 | `docs/developer/schema.md` | 索引文件 JSON/YAML 结构定义与字段说明 |
| 常见实践 | `docs/examples/usage-patterns.md` | 如何结合爬虫框架（如 Scrapy）使用本索引 |

## 资源列表

### 视频素材类

<code>mianfeizipaishipin.net.cn</code>

<code>diguashipin.net.cn</code>

<code>chengzishipin.net.cn</code>

### 漫画图像类

<code>xiuxiumanhuaw.net.cn</code>

<code>meinvmanhua.net.cn</code>

<code>xiuxiumanhuazaixianguankan.net.cn</code>

### 字幕语料类

<code>zhongwenzimuzaixianmianfeikana.org.cn</code>

## 项目结构

```
novaindex/
├── README.md                       # 项目总体说明与导航
├── LICENSE                         # MIT 许可证文件
├── .gitignore                      # Git 忽略规则
├── config/
│   ├── categories.yaml             # 资源分类层级定义
│   └── batch_23.json              # 第 23 批原始链接数据
├── scripts/
│   ├── build_index.sh             # 主构建脚本，调用各子模块
│   ├── check_links.py             # Python 链接存活检查脚本
│   └── export_yaml.js             # 将 JSON 转换为 YAML 格式
├── src/
│   ├── templates/
│   │   ├── page.template.html     # HTML 导航页模板
│   │   └── index.template.md      # Markdown 索引模板
│   └── parsers/
│       ├── url_normalizer.py      # URL 规范化工具（强制保留原格式）
│       └── batch_processor.py     # 批次数据合并处理器
├── dist/                          # 构建输出目录（自动生成）
│   ├── index.html
│   ├── index.json
│   ├── index.yaml
│   └── status_report.txt
├── docs/
│   ├── guide/
│   ├── maintainer/
│   ├── developer/
│   └── examples/
└── tests/
    ├── test_url_format.py         # 检查 URL 是否被错误改写
    └── test_schema_validator.py   # 验证索引 JSON 结构合法性
```

## 贡献指南

1. 复刻本仓库至个人账户，并在本地新建功能分支，分支命名遵循 `feature/batch-{批次号}-{简短描述}` 格式。
2. 在 `config/batch_{批次号}.json` 中按照既定 JSON Schema 追加新的资源链接条目，注意必须保留原始域名或原始协议，不得添加 `www.` 或更改协议头。
3. 运行 `./scripts/check_links.py --batch {批次号}` 对新加入的链接进行基础连通性测试，并确保测试报告通过。
4. 提交包含清晰提交信息的 commit，信息格式为 `add(batch): {批次号} 新增 {数量} 条资源`，并附上链接可用性报告摘要。
5. 发起 Pull Request 至主仓库的 `main` 分支，等待维护者审核。审核通过后，您的变更将被合并，并在下一轮构建中生效。

## 常见问题

**问：为什么我看到的链接是裸域名，不带 http 或 https 前缀？我应该如何使用它们？**

答：本索引严格遵循资源原始记录格式，不添加任何额外前缀。使用前，请根据目标资源的实际部署情况，自行在请求时添加适当的协议头（如 `http://` 或 `https://`）。这有助于避免因协议改写导致的访问失败，并给予使用者最大控制权。

**问：某些链接无法访问或返回错误状态码，项目是否会主动清理失效链接？**

答：项目会定期（每批次更新时）通过自动化脚本对收录链接进行基础连通性探测。对于持续不可达的链接，会在 `status_report.txt` 中标记为“疑似失效”，但不会立即删除。失效链接的移除决策将综合参考多个探测周期（至少 3 个周期）的结果，并保留至少 30 天的观察期，以规避临时网络波动。

**问：我能否直接使用本索引中的数据用于商业项目或闭源产品？**

答：本索引项目本身采用 MIT 许可证，这意味着索引的目录结构、分类逻辑与构建脚本均可自由使用、修改与分发。但请注意，索引中所列的外部资源链接，其各自的内容版权与使用条款均属于原始提供方。在将外部链接用于商业用途前，您需要自行确认相应外部网站的 robots.txt 协议及服务条款。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
