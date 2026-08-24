# NovaLink 资源导航系统

NovaLink 是一个专为技术社区、内容创作者及研究机构设计的轻量级资源导航与外部链接聚合平台。该项目定位于解决信息碎片化环境下的高效资源索引问题，通过结构化的分类体系与极简的部署方式，帮助用户在特定垂直领域内快速定位高价值外部内容。

NovaLink 并非一个传统的内容管理系统（CMS），而是一个基于静态文件与配置驱动的链接枢纽站。其核心目标用户包括开源项目维护者、技术文档撰写人、在线教育平台运营方以及需要频繁整理并共享外部参考链接的团队。系统通过清晰的目录树与标签机制，将分散的优质资源归入统一入口，显著降低团队内部或公开社区中的信息检索成本，同时避免重复造轮子，将精力聚焦于资源筛选与质量把控之上。

## 功能概览

- **分级分类索引**：支持按照语种、题材、热度等多维度对链接进行一级与二级分类，便于构建层次分明的导航体系。

- **配置化链接管理**：所有外链资源通过单一配置文件或目录树中的 Markdown 文件进行管理，无需操作数据库，修改即可生效。

- **静态站点生成适配**：项目结构天然适配主流静态站点生成器（如 Hugo、VuePress），可一键导出为纯静态 HTML，便于托管于任何 Web 服务器或 CDN。

- **资源状态自动检查**：内置轻量级链接可用性检测脚本，可定期扫描已收录 URL 的响应状态，辅助维护者清理失效资源。

- **快速关键词过滤**：前端集成即时搜索与标签过滤功能，用户可在当前分类下按关键词快速筛出匹配链接，提升查找效率。

- **外部链接安全跳转提示**：对于所有指向外部的 URL，系统默认生成中间提示页，告知用户即将离开本平台，增强安全性与透明性。

- **多实例部署支持**：支持通过环境变量切换不同配置文件，允许同一套代码运行多个独立导航实例，适用于多项目或多团队场景。

## 应用场景

1. **开源项目官方资源附录**：开源软件维护者可使用 NovaLink 构建项目官网的“生态工具”或“相关项目”页面，集中陈列周边库、插件、示例代码等外部链接，方便社区贡献者快速了解全貌。

2. **技术培训课程外链手册**：在线教育机构或企业培训部门可将每期课程涉及的所有参考文档、视频源、在线编译器地址汇总于一个 NovaLink 实例中，作为学员的常驻浏览器起始页或课程首页附属模块。

3. **行业资讯聚合看板**：研究团队或媒体编辑可利用 NovaLink 搭建内部资讯看板，将每日必读的新闻源、数据平台、趋势报告站点按主题分区陈列，配合状态检查功能及时发现访问异常。

4. **本地开发环境导航页**：开发人员可将个人常用的内网服务地址（如 Jenkins、SonarQube、Nexus）、云平台控制台、测试环境入口等集中配置为本地 NovaLink 实例，替代浏览器书签栏，实现跨设备同步。

5. **社区共建资源目录**：技术社区可部署公开的 NovaLink 实例，允许成员通过 Pull Request 方式提交新链接，维护者审核合并后自动更新在线导航，形成社区驱动的知识图谱。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，请确保已安装 Git 与 Node.js（建议 v18 或更高版本）。

```bash
# 克隆项目仓库
git clone https://github.com/novalink-dev/novalink-core.git
cd novalink-core

# 安装项目依赖（使用 npm 或 yarn）
npm install

# 使用开发模式启动本地预览服务
npm run serve
```

执行上述命令后，终端会输出本地访问地址（通常为 http://localhost:8080）。打开浏览器即可看到默认导航界面。如需构建生产环境静态文件，请执行 `npm run build`，生成内容位于 `dist/` 目录下。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | v18.0.0 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | v8.0.0 或更高 | 包管理器，用于安装依赖包 |
| Git | v2.25.0 或更高 | 版本控制工具，用于克隆仓库及提交变更 |
| 现代浏览器 | 最新两个主要版本 | 前端界面运行环境，支持 ES6+ 及 CSS Grid/Flexbox |
| 操作系统 | Linux / macOS / Windows 10+ | 支持主流操作系统，Windows 下建议使用 WSL2 或 PowerShell 7 |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|-----------|------------|
| 用户入门 | `docs/quick-start.md` | 如何快速部署一个实例并添加第一批链接？ |
| 配置参考 | `docs/configuration.md` | 分类结构、链接字段、主题选项如何配置？ |
| 开发指南 | `docs/development.md` | 如何二次开发、自定义主题或扩展检测脚本？ |
| 运维手册 | `docs/operations.md` | 如何做链接健康检查、日志监控及备份恢复？ |
| 设计理念 | `docs/philosophy.md` | NovaLink 的分类模型与信息架构设计原则是什么？ |

## 资源列表

以下列出本导航系统初始收录的外部资源链接，按类别分组展示。所有 URL 均严格遵循用户原始数据，未做任何改动。

**在线视频资源分类（中文）**

- <code>zhongwenshipinzaixianguankanc.org.cn</code>

- <code>shipinmianfeizaixianguankanc.org.cn</code>

**在线视频资源分类（日文及综合）**

- <code>rimanzaixianguankanc.org.cn</code>

- <code>rihanzaixianmianfeishipinc.org.cn</code>

**字幕与衍生内容分类**

- <code>zhongwenzimumianfeibofangc.org.cn</code>

- <code>renqixiliezhongwenzimuc.org.cn</code>

**特别收录**

- <code>wuyefulizhiboc.org.cn</code>

## 项目结构

```
novalink-core/
├── config/                           # 全局配置目录
│   ├── default.yaml                  # 默认导航配置（分类、链接、主题）
│   └── schema.json                   # 配置文件的 JSON Schema 校验定义
├── src/                              # 前端源代码目录
│   ├── assets/                       # 静态资源（图片、字体、全局样式）
│   ├── components/                   # Vue 可复用组件（导航卡、搜索框、标签列表）
│   ├── views/                        # 页面级组件（首页、分类详情、跳转提示页）
│   ├── router/                       # 前端路由配置（history 模式）
│   ├── store/                        # Vuex 状态管理（当前分类、搜索关键词、链接缓存）
│   └── main.js                       # 应用入口文件，挂载 Vue 根实例
├── scripts/                          # 工具脚本目录
│   ├── check-links.js                # 链接可用性检测脚本（基于 node-fetch）
│   ├── generate-sitemap.js           # 动态生成 sitemap.xml 供搜索引擎爬取
│   └── migrate-config.js             # 配置版本升级迁移辅助脚本
├── public/                           # 公共静态目录（不经过构建管道）
│   ├── favicon.ico                   # 站点图标
│   └── robots.txt                    # 搜索引擎爬虫规则
├── dist/                             # 构建输出目录（git 忽略，仅生产环境生成）
├── docs/                             # 项目文档（用户手册、API 参考、架构说明）
├── tests/                            # 单元测试与集成测试脚本（Jest + Vue Test Utils）
├── .env.example                      # 环境变量示例文件（用于配置不同实例）
├── package.json                      # npm 依赖清单与脚本定义
├── README.md                         # 项目主说明文档（即本文档）
├── LICENSE                           # MIT 许可证文本
└── .gitignore                        # Git 版本控制忽略文件规则
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于提交新链接分类建议、改进前端界面、完善文档或报告问题。请遵循以下步骤参与本项目：

1. **查阅现有议题**：在提交 Pull Request 之前，请先浏览 GitHub Issues 列表，确认是否存在相关讨论或已有进行中的工作，避免重复劳动。

2. **Fork 仓库并创建特性分支**：从主仓库 Fork 一份副本到个人账户，然后基于 `main` 分支创建新的特性分支，分支命名建议使用 `feat/` 或 `fix/` 前缀加简要描述。

3. **编写或修改代码并遵守编码规范**：项目使用 ESLint 与 Prettier 统一代码风格，提交前请运行 `npm run lint` 确保无格式错误。对于链接配置的新增或修改，请同步更新 `config/default.yaml` 中的对应分类。

4. **撰写清晰的提交信息**：提交信息请使用英文或中文简明描述变更内容，采用“类型: 简短说明”格式（例如 `feat: add new category for Japanese video resources`）。

5. **发起 Pull Request 并等待审核**：将特性分支推送到个人 Fork 仓库后，在主仓库发起 Pull Request，填写模板中的检查项。维护者会在 3 个工作日内进行审核，可能提出修改意见，请保持关注。

## 常见问题

**Q: 我不想使用 Vue 或 Node.js，能否将 NovaLink 纯静态化部署到 Nginx 或 Apache？**

A: 完全可以。NovaLink 的设计目标之一就是支持静态导出。您只需执行 `npm run build`，系统会将所有动态路由预渲染为静态 HTML 文件，并生成对应的 CSS 与 JavaScript 打包文件。将这些产物复制到任意 Web 服务器的根目录下即可直接访问，无需 Node.js 运行时。您甚至可以进一步使用 `scripts/generate-sitemap.js` 生成站点地图，便于 SEO 优化。

**Q: 系统内置的链接状态检查脚本是如何工作的？误报如何处理？**

A: 检查脚本 `check-links.js` 通过发送 HTTP HEAD 请求来检测每个 URL 的响应码，默认将 200-399 范围内的状态视为有效，其余状态（包括超时、DNS 解析失败、SSL 证书错误）均标记为异常。检查结果会输出到控制台并生成一份 `broken-links.json` 报告。由于部分网站可能拒绝 HEAD 请求或存在临时维护，您可以通过修改脚本中的 `VALID_STATUSES` 数组或增加 `timeout` 参数来调整判定逻辑。建议将脚本加入 CI 流水线，定时执行并仅人工复核持续异常的链接。

**Q: 我能否在一个 NovaLink 实例中管理多套独立的链接集合，并为不同用户展示不同内容？**

A: 当前版本通过环境变量 `VUE_APP_CONFIG_PATH` 支持加载不同的配置文件，您可以在部署时指定路径来切换整站内容。若需要同一域名下按用户身份动态展示不同集合，则属于多租户场景，目前官方并未内置该能力。建议您通过部署多个独立实例（每个实例使用不同配置）并配合反向代理的路由规则来实现，或者二次开发 `src/store` 中的状态管理逻辑，增加基于用户参数的过滤层。

## 许可证

MIT License

Copyright (c) 2026 NovaLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-24 22:41:23
