# 团队开发规范中心

这里是本组织的 GitHub 使用规范、coding agent 使用规范与仓库模板的统一存放处。**组织协作规则以本仓库为准**；规则提议先在 Discussions 交流；形成具体修改后建立 Issue，并通过 PR 审核、记录。

设计目标：**以文档为中心、流程尽量轻、新手可上手、防止项目膨胀、防止 agent 误用。**

## 选择入口

- **查规范**：按下方“从这里开始”阅读对应文档。
- **申请仓库**：进入 Issues → New issue → **仓库申请**，填写独立申请表单。
- **交流、求助和规范讨论**：进入仓库顶部 **Discussions**。
- **练习 GitHub 操作**：在独立练习仓库按 [练习流程](practice-walkthrough.md) 操作，不在本仓库提交练习内容。

本仓库的 Issue 用于仓库申请，以及已明确的规范或模板缺陷、改进。项目开发任务在对应项目仓库跟踪；一般讨论不建立通用任务 Issue。

## 仓库结构

```text
├── git-github-basics.md      # Git / GitHub 入门
├── practice-walkthrough.md   # 新人练习流程
├── CONTRIBUTING.md          # 提交与审批
├── agents-template-guide.md # AGENTS.md 通用模板使用说明
├── coding-agent-guide.md    # AI 使用责任
├── modular-testing.md      # 模块和测试
├── repo-governance.md      # 仓库治理
├── licensing-guide.md      # 许可证说明
├── ci-setup.md             # CI 模板接入说明
├── setup-checklist.md      # 管理员接入清单
├── LICENSE                 # 许可证（MIT）
├── SECURITY.md             # 安全问题私下报告方式
├── .gitignore              # 忽略规则
├── .github/                # Issue / PR 模板、CODEOWNERS、CI 工作流
└── templates/              # CI、CODEOWNERS 等示例，复制映射见落地清单
```

> 使用方式：模板需根据项目接入并验证，再按 [落地清单](setup-checklist.md) 配置平台约束。人员名单、权限和运行结果在对应 GitHub 团队、仓库设置和检查记录中维护。

## 从这里开始

1. [Git 与 GitHub 新手需知](git-github-basics.md) — 零基础入门：Git 是什么、术语黑话、完整提交流程、常见问题
2. [CONTRIBUTING.md](CONTRIBUTING.md) — 提交与审批流程细则：分支规范、commit 规范、PR 规则、自查清单
3. [新人练习流程](practice-walkthrough.md) — 在练习仓库走一次完整协作
4. [Coding Agent 使用规范](coding-agent-guide.md) — AI 使用责任和验证要求

## 五条核心原则（记住这五句就够了）

1. **一切改动走 PR，不许直推 main。**
2. **小步提交**：一个 PR 只做一件事，尽量小（参考值 400 行，不定死——大了要说清为什么不能拆）。
3. **卡住可以提前求助；必要检查通过、审批完成后才合并。**
4. **团队鼓励用 AI 写代码**——提交人要理解关键逻辑、检查最终改动、说明验证方法；不懂的关键部分找有经验的成员共同检查。
5. **模块边界清晰、有说明，改动按项目类型提供适当验证。**

## 三层结构（规范怎么落地）

| 层 | 内容 | 约束方式 |
|---|---|---|
| 第一层：平台约束 | CODEOWNERS、分支保护、必要 CI 检查 | 配置后由平台强制；PR 模板辅助填写，内容由人检查 |
| 第二层：规范文档 | 本仓库的文档集（git 流程、review、agent、测试、仓库治理） | PR 评审时引用 |
| 第三层：新手辅助 | 每份文档末尾的自查 checklist | 提交前自查 |

## 新仓库怎么落地

组织下每一个新仓库创建时，从本仓库 `.github/` 复制适用的 Issue / PR 模板（普通项目不复制仓库申请表单，讨论链接按目标仓库调整），从 `templates/` 复制适用的其他模板，按 [落地清单](setup-checklist.md) 中的映射放到目标仓库的生效位置，并替换组织名、团队名和链接中的占位符，再把相关规范文档链接进新仓库的 README。`templates/` 仅保存模板，不会自动启用 GitHub 配置；分支保护、必需检查和审批要求仍须管理员在 GitHub Settings 中设置。组织仓库统一使用 Public。规范本身也走 PR 流程修改——对规范的开放讨论放在 Discussions；形成修改后关联 Issue 和 PR，保留决定与原因。


## 给 AI 协作者使用

各项目可复制 [AGENTS.md 模板](templates/AGENTS.md)，直接使用共同规则；有特殊约定时，按 [使用说明](agents-template-guide.md) 选补。共同规则保持系统与设备无关，项目命令在各自文档中维护。
