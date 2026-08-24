# ResourceBridge

ResourceBridge 是一个面向开发者与技术内容创作者的开源外链资源整理与聚合工具。项目本身不生产内容，而是通过结构化方式将分散在网络各处的优质技术文档、视频字幕资源、在线播放工具等外部链接进行归集、分类与版本追踪，帮助技术团队和个人快速定位所需的外部参考资料。项目目标用户包括开源社区维护者、技术博主、在线教育内容运营人员以及需要频繁查阅多源技术资料的全栈工程师。

## 功能概览

- **多源链接归集管理** 支持将外部 URL 按自定义类别、标签和来源批次进行录入与存储，并提供基础的查重与失效链接标记能力。

- **结构化资源导航** 基于 Markdown 表格与分类小节，将大量裸域名或带协议链接组织为层级清晰的资源目录，便于人工审阅与自动化脚本解析。

- **批次追踪与版本记录** 每个资源入库时记录所属项目批次（如第 43/120 批），支持按批次维度筛选和导出链接清单，方便周期性更新。

- **ASCII 目录树自动生成** 项目维护脚本可根据实际文件结构生成树状图，并在 README 中展示，降低新贡献者的理解成本。

- **依赖环境一键检测** 通过安装要求表格与快速开始脚本，帮助用户在 5 分钟内完成 Node.js、Python 或纯静态环境的前置检查与运行。

- **文档导航映射** 将常见问题（如如何新增链接、如何报告失效）直接映射到对应文档或章节，减少重复性 issue 提问。

- **裸域名与带协议链接兼容处理** 资源列表章节严格保留用户提供的原始 URL 格式（包括裸域名、http、https 及 www 前缀），不做任何自动补全或改写。

## 应用场景

- **开源项目外部依赖清单维护** 当项目需要引用大量第三方教程、视频字幕站或在线播放工具时，维护者可将这些外部链接统一整理至 ResourceBridge 的资源列表中，并在版本发布时同步导出校验。

- **技术培训课程参考资料包** 在线教育机构可将每期课程涉及的所有扩展阅读链接、视频资源地址按批次录入，学员通过查看资源列表即可获取完整参考资料，无需在课程视频中手动记取。

- **个人知识库外链备份与分类** 开发者可将日常积累的技术文章、字幕站、在线播放网站等链接按功能类别整理进项目仓库，配合版本控制追溯链接的增删历史，避免书签丢失后重新搜集。

- **团队协作时的统一入口** 技术团队可将内部常用的工具站、文档镜像、字幕下载站等链接汇总于 ResourceBridge，新成员通过 README 的资源列表即可快速获得团队认可的权威外部资源集合。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，确保系统已安装 Git 与 Node.js 16+。

```bash
# 克隆项目仓库
git clone https://github.com/resource-bridge/resource-bridge.git
cd resource-bridge

# 安装项目依赖（用于本地预览和链接格式校验）
npm install

# 运行本地开发服务器，默认监听 3000 端口
npm run dev
```

访问 `http://localhost:3000` 即可查看当前批次的资源导航页面。如需仅生成静态 README 章节，可执行：

```bash
npm run build:readme
```

该命令会根据 `data/resources.json` 中的记录自动更新 README 的「资源列表」章节，并校验每个 URL 格式是否与原始输入一致。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 16.0.0 或更高 | 运行本地预览服务器及构建脚本 |
| npm | 8.0.0 或更高 | 安装前端依赖与命令行工具 |
| Git | 2.25.0 或更高 | 克隆仓库并管理版本历史 |
| 操作系统 | Linux / macOS / Windows WSL2 | 开发环境推荐 Unix-like 系统 |
| 网络访问 | 可访问公网 | 用于初次安装 npm 包及校验外部链接可达性（可选） |
| 磁盘空间 | 至少 200 MB | 存放代码、依赖及资源缓存 |
| 浏览器 | Chrome 90+ / Firefox 88+ | 预览导航页面（仅开发时需） |

## 文档导航

| 层面 | 目录/章节 | 回答的问题 |
|------|-----------|------------|
| 项目入门 | README（本文档） | 项目是什么、如何快速启动、依赖与结构 |
| 链接维护 | `docs/MAINTAIN.md` | 如何新增链接、如何修改已有链接的类别、如何标记失效 |
| 脚本工具 | `scripts/` 目录下的源码注释 | 链接格式校验规则是什么、如何批量导出指定批次的链接 |
| 贡献流程 | `CONTRIBUTING.md` 与 `docs/REVIEW.md` | PR 审核标准是什么、如何提交新批次资源、issue 模板如何填写 |
| 常见问题 | 本文档「常见问题」章节 + `docs/TROUBLESHOOT.md` | 链接无法访问怎么办、URL 格式被脚本拒绝如何处理 |

## 资源列表

以下为第 43/120 批次的全部原始资源链接，按功能类别分节列出。每个链接均保留用户提供的原始格式，未做任何协议补全、域名改写或路径修改。

### 中文字幕相关资源

- <code>gaoqingzhongwenzimua.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikanb.org.cn</code>
- <code>zaixianshipinzhongwenzimub.org.cn</code>
- <code>zaixianbofangzhongwenzimub.org.cn</code>
- <code>zhongwenshipinzaixianguankanb.org.cn</code>

### 在线视频播放资源

- <code>zaixianbofangnidongdea.org.cn</code>
- <code>shipinmianfeizaixianguankanb.org.cn</code>

## 项目结构

```
resource-bridge/
├── data/                               # 数据存储目录
│   ├── resources.json                  # 所有批次的链接主数据（含批次号、类别、录入时间）
│   └── schemas/                        # JSON Schema 校验文件
│       └── resource-schema-v1.json     # 链接字段格式约束定义
├── scripts/                            # 维护与构建脚本
│   ├── validate-urls.js                # 校验每个 URL 是否与原始输入严格一致（不补协议、不改大小写）
│   ├── export-by-batch.js              # 按批次号导出 Markdown 列表片段
│   └── generate-tree.js                # 自动生成 ASCII 目录树用于 README
├── docs/                               # 扩展文档
│   ├── MAINTAIN.md                     # 链接增删改操作指南
│   ├── REVIEW.md                       # PR 审核清单与质量标准
│   └── TROUBLESHOOT.md                 # 常见环境问题与 URL 解析故障排查
├── templates/                          # README 与文档模板
│   ├── readme-head.md                  # README 前半部分固定内容（简介、功能、场景）
│   └── resource-list-template.md       # 资源列表章节的占位模板，脚本会替换其中内容
├── tests/                              # 单元测试
│   ├── url-format.test.js              # 测试 URL 格式保留逻辑（裸域名、带协议、www 等）
│   └── batch-export.test.js            # 测试批次导出是否遗漏链接
├── .github/                            # GitHub 社区文件
│   ├── ISSUE_TEMPLATE/                 # 问题报告模板（链接失效、新增请求等）
│   └── workflows/                      # CI 工作流（自动校验 PR 中的 URL 格式）
├── package.json                        # npm 项目配置，包含 dev / build:readme 等脚本
├── .gitignore                          # 忽略 node_modules / dist / 临时缓存
└── README.md                           # 当前文档，包含所有固定章节与动态生成的资源列表
```

## 贡献指南

1. **查阅现有资源列表与维护文档**  
   在新增或修改链接之前，请先阅读 `docs/MAINTAIN.md` 了解类别命名规范与批次号分配规则。确认待添加的链接尚未存在于当前或历史批次中。

2. **克隆仓库并创建特性分支**  
   使用 `git checkout -b feature/add-batch-43` 创建独立分支，避免直接在主分支上修改数据文件。

3. **编辑 `data/resources.json` 并运行校验脚本**  
   按照 JSON Schema 添加新链接对象，务必保留用户提供的原始 URL 字符串（不补协议、不改域名大小写）。随后执行 `npm run validate` 确保格式合规。

4. **更新 README 资源列表章节**  
   执行 `npm run build:readme` 自动将最新数据同步至 README 的「资源列表」章节。人工检查生成的列表是否与原始输入完全一致。

5. **提交 Pull Request 并等待审核**  
   提交 PR 时请填写对应模板，说明本次批次编号、链接数量及类别分布。审核者将对照原始数据逐条核对 URL 格式，确认无误后合并。

## 常见问题

**Q：为什么资源列表中的某些链接是裸域名（如 abc.com），没有带 http:// 或 https://？**  
A：这是为了严格遵循用户提供的原始输入格式。ResourceBridge 的设计原则是不对来源 URL 做任何隐式补全或改写，因为部分资源站可能仅支持特定协议，或管理员希望使用协议相对路径。浏览器访问时请根据实际情况手动添加协议前缀。

**Q：运行 `npm run validate` 时报错提示某个链接格式不符合要求，但我在浏览器中能正常打开。**  
A：校验脚本仅检查字符串层面的格式一致性（例如是否与原始记录完全相等、是否包含非法空白字符），并不校验链接是否可访问。如果报错，请检查该链接是否被无意中修改了大小写、增加了尾部斜杠或改变了协议前缀，确保与用户原始数据逐字符相同。

**Q：我想提交新批次，但不会编辑 JSON 文件，有没有更简单的界面？**  
A：目前项目使用 JSON 文件作为唯一数据源，但您可以在 GitHub 上先创建 issue 说明新批次链接列表，由维护者协助转换。后续版本计划提供基于 Web 的简易表单，请关注 `docs/ROADMAP.md` 的更新。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
