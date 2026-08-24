# ResourceHub

ResourceHub 是一个面向开发人员、技术研究者与内容创作者的轻量级技术资源导航与外链聚合平台。该项目旨在解决个人收藏夹混乱、技术文档分散、优质外链难以回溯与共享的问题，通过结构化的资源分类、可定制的标签体系与简洁的全文检索，帮助用户从海量信息中快速定位高价值技术站点。

ResourceHub 的核心目标用户包括：日常维护大量技术书签的全栈工程师、需要持续跟踪行业动态的技术管理者、以及希望系统化整理学习资料的自学者。项目本身不存储任何第三方内容，仅作为索引层与展示层，所有外链均以原始 URL 形式原样呈现，确保来源可溯、版权清晰。

## 功能概览

- **多维度资源分类**：支持按技术领域、资源类型、适用场景对链接进行三级标签分类，便于批量筛选与浏览。
- **原始链接直出模式**：所有收录的 URL 均以文本形式原样展示，不进行重定向包装，不附加追踪参数，保证链接透明可验证。
- **轻量级全文检索**：基于标题、标签、描述字段实现毫秒级关键词匹配，支持模糊搜索与精确匹配模式。
- **可配置的资源显示策略**：管理员可针对不同资源组设置默认排序、置顶规则或隐藏状态，适应团队内部知识库需求。
- **无数据库零依赖运行**：全部资源数据存储于单一 JSON 文件中，启动时加载至内存，降低运维成本。
- **响应式卡片布局**：在桌面端与移动端均提供良好的浏览体验，资源卡片内嵌站点 favicon 与简要元信息。
- **开放数据导出接口**：支持将当前资源列表导出为 CSV 或 Markdown 表格，便于离线备份或嵌入文档。

## 应用场景

- **技术团队内部知识库**：研发团队可将常用依赖库文档、监控面板、CI/CD 控制台等内部链接统一收录至 ResourceHub，作为团队首页，减少上下文切换成本。
- **开源项目 README 外链维护**：开源维护者可将项目依赖的参考文档、社区论坛、示例仓库等链接通过 ResourceHub 集中管理，并在 README 中引用该站点，避免 README 过长。
- **个人学习路径整理**：自学者可按阶段（入门 / 进阶 / 实战）将不同在线课程、API 手册、练习题平台分类存放，配合搜索功能快速复习特定知识点。
- **技术会议或沙龙资料汇总**：活动组织者可将讲师博客、PPT 下载地址、相关论文链接统一收录，生成专属活动资源页，参会者一键访问。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境。

```bash
# 1. 克隆仓库
git clone https://github.com/example/resourcehub.git
cd resourcehub

# 2. 安装依赖（使用 npm）
npm install

# 3. 启动开发服务器
npm run dev
```

默认访问地址为 `http://localhost:3000`。生产环境构建请使用 `npm run build` 后执行 `npm run start`。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | >= 18.12.0 | 运行时环境，用于执行服务端与构建脚本 |
| npm | >= 8.19.0 | 包管理器，用于安装项目依赖 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 官方支持平台，Windows 原生 PowerShell 未充分测试 |
| 内存 | 最低 512 MB 空闲 | 生产环境建议 1 GB 以上，用于加载资源文件 |
| 磁盘空间 | 最低 200 MB | 包含 node_modules 及构建缓存，实际资源数据仅占数十 KB |
| 网络 | 外网访问 | 用于加载资源站点的 favicon 和元信息（非阻塞） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | /docs/user-guide.md | 如何浏览、搜索、筛选资源，如何自定义卡片显示偏好 |
| 管理员手册 | /docs/admin-guide.md | 如何添加 / 编辑 / 删除资源条目，如何管理标签体系，如何调整排序权重 |
| 数据格式规范 | /docs/data-schema.md | resources.json 的完整字段定义、类型约束、示例数据，以及扩展字段说明 |
| API 参考 | /docs/api-reference.md | 对外提供的检索接口、导出接口、元数据查询接口的请求与响应格式 |
| 部署指南 | /docs/deployment.md | 如何部署到 Vercel / Netlify / 自建 Nginx 服务器，环境变量配置项 |

## 资源列表

以下为 ResourceHub 当前收录的全部外链资源，按类别分组呈现。所有 URL 均严格按照用户提供的原始形式输出，未做任何协议、域名或路径的修改。

### 影视与在线播放类

- <code>mianfeizhuijuwangzhana.org.cn</code>
- <code>gaoqingzhongwenzimua.org.cn</code>
- <code>zaixianbofangnidongdea.org.cn</code>
- <code>zhongwenzimuzaixianmianfeikanb.org.cn</code>
- <code>zaixianshipinzhongwenzimub.org.cn</code>
- <code>zaixianbofangzhongwenzimub.org.cn</code>
- <code>zhongwenshipinzaixianguankanb.org.cn</code>

## 项目结构

```
resourcehub/
├── src/
│   ├── core/                    # 核心加载与索引逻辑
│   │   ├── loader.js            # 读取 resources.json 并构建内存索引
│   │   └── search.js            # 全文检索实现（基于字符串匹配）
│   ├── routes/                  # HTTP 路由处理
│   │   ├── api.js               # /api/search, /api/export 等端点
│   │   └── web.js               # 页面渲染路由（首页、分类页）
│   ├── views/                   # 前端模板
│   │   ├── layout.ejs           # 基础 HTML 骨架
│   │   ├── index.ejs            # 资源总览与搜索框
│   │   └── category.ejs         # 按标签筛选后的列表视图
│   ├── public/                  # 静态资源
│   │   ├── css/                 # 响应式样式表（flexbox + grid）
│   │   └── js/                  # 前端交互（搜索防抖、卡片折叠）
│   └── utils/                   # 工具函数
│       └── url-validator.js     # 校验原始 URL 格式，防止注入
├── data/
│   └── resources.json           # 所有资源条目的存储文件（数组结构）
├── docs/                        # 完整文档目录（参见「文档导航」章节）
├── tests/                       # 单元测试（Jest）
├── .env.example                 # 环境变量模版（端口、缓存开关）
├── package.json
├── README.md                    # 本文件
└── LICENSE                      # MIT 许可证
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于新增资源链接、改进搜索算法、完善文档或修复 UI 缺陷。

1. **提交 Issue 进行讨论**：对于较大改动（如数据模型变更、新增依赖），请先在 Issues 中描述你的想法，维护者将在 48 小时内回复可行性评估。
2. **Fork 仓库并创建特性分支**：分支命名请遵循 `feature/xxx` 或 `fix/xxx` 格式，避免在主分支直接提交。
3. **更新资源数据或代码后编写对应测试**：若修改了 `loader.js` 或 `search.js`，请在 `tests/` 目录下补充或更新测试用例，确保覆盖率不低于 80%。
4. **确保文档同步更新**：如果新增了配置项或修改了 API 行为，请同步更新 `/docs` 下的相关文档以及本 README 中的「功能概览」或「安装要求」表格。
5. **发起 Pull Request 并关联 Issue**：PR 描述中请注明所解决的 Issue 编号，并附上本地测试结果（如 `npm run test` 与 `npm run build` 的截图或日志）。

## 常见问题

**Q：ResourceHub 是否存储或缓存第三方网站的内容？**  
A：不存储。ResourceHub 仅保存用户提交的 URL 及其元描述（标题、标签、备注），不抓取、不代理、不缓存任何第三方页面内容。所有外链访问均直接跳转至原始 URL，资源可用性由目标站点自行保证。

**Q：resources.json 中的链接数量有上限吗？**  
A：理论上无硬性上限，但受限于内存大小（单条记录平均约 200 字节，10 万条记录约 20 MB）。实际使用中建议将条目数控制在 2 万以内以维持检索响应速度在 50ms 以下。若需管理更大规模资源，推荐使用 Elasticsearch 版本（见社区扩展项目）。

**Q：如何批量导入或导出资源列表？**  
A：项目启动后访问 `/api/export?format=csv` 可下载 CSV 格式的完整资源列表。导入功能可通过 `/api/import` 端点（POST 请求）上传符合 schema 的 JSON 或 CSV 文件，具体格式请参考 `/docs/data-schema.md` 中的导入章节。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-24 22:42:00
