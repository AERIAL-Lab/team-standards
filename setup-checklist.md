# 仓库接入清单（管理员）

新建仓库或接入组织规范时，按本清单配置并记录结果。已有配置应先核对，不必重复创建。

## 1. 明确名称和人员

- 填入真实组织名、项目仓库名，确定审核成员，并在 GitHub 团队中维护名单。
- 建立 reviewers 团队；可用其他名字，但 CODEOWNERS 同步更改。团队可见并显式拥有仓库 write 权限。
- 自有代码新项目默认采用 MIT；特殊情况说明原因并由管理员确认。负责人填写版权人、年份，依据见 [许可证说明](licensing-guide.md)。确认版权人和授权依据后，添加正式许可证文本。

## 2. 复制文件

| 本包源文件 | 目标位置 |
|---|---|
| templates/AGENTS.md | 使用 AI 协作的项目复制为根目录 AGENTS.md；特殊约定按需补充，无需填表 |
| templates/CODEOWNERS.example | .github/CODEOWNERS，替换 your-org/reviewers |
| .github/PULL_REQUEST_TEMPLATE.md | .github/PULL_REQUEST_TEMPLATE.md |
| .github/ISSUE_TEMPLATE/bug_report.yml、feature_request.yml | 普通项目复制到 .github/ISSUE_TEMPLATE/ |
| .github/ISSUE_TEMPLATE/repository_request.yml | 仅组织规范仓库使用，不复制到普通项目或练习仓库 |
| .github/ISSUE_TEMPLATE/config.yml | 按目标仓库配置：启用 Discussions 后填写真实链接，不盲目复制规范仓库地址 |
| templates/SECURITY.md | SECURITY.md，确认私下报告入口可用 |
| templates/ci.yml | .github/workflows/ci.yml，按 CI 说明接入 |
| templates/ci-node.yml | Node + Jest 项目可选，放 .github/workflows/ci-node.yml |
| templates/practice-ci.yml | 练习仓库放 .github/workflows/practice-ci.yml |
| templates/practice-profile.md | 练习仓库放 profiles/example.md |

项目自己补 README、适用的 .gitignore、测试命令和锁文件，并链接组织规范。复制模板不会自动配置平台权限。检查模板中的示例域名、组织名，不能凭空替换为猜测的真实账号。

## 3. 配置 GitHub

- 仓库 Public，按需给项目成员分支写权限；组织管理、删除和改权限仅交给管理员。
- main 要求 PR、至少一名 Code Owner 批准、必要检查通过；保护对管理员生效，禁止 force push 和删除 main。
- 启用 Dismiss stale pull request approvals when new commits are pushed（改动变化后撤销旧批准）；PR 改动内容变化后，由审核组中非作者成员重新批准。
- 必需检查要求分支与最新 main 保持同步（Require branches to be up to date before merging）；启用 Require conversation resolution before merging，合并前处理完审核讨论。
- 仅允许 Squash merge，自动删除已合并分支。
- 开启 Secret scanning / Push protection 和私有漏洞报告；Security 报告入口实际可用后发布 SECURITY.md。
- 规范仓库开启 Discussions，作为交流、求助和开放讨论入口；项目任务仍在各项目仓库跟踪。
- 确认 Issue 标签存在（bug、enhancement 等），运行一次各表单。

审批设置含义见 [GitHub 分支保护说明](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)。

## 4. 最后验证

按 [CI 接入说明](ci-setup.md) 在试点项目跑通对应工作流，再设置必需检查。按 [练习流程](practice-walkthrough.md) 用两名成员体验一次从 Issue 到合并，确认草稿、审核、检查及冲突处理符合预期。

记录实际验证结果；文档或 YAML 可解析不代表工作流已运行通过。

## 5. 后续模板更新

在项目 README 或贡献说明中记录组织规范来源链接、采用模板的版本或提交编号。规范维护者修改模板时，在 PR 中说明受影响的模板和需要各项目跟进的事项。

各项目负责人检查适用变化，通过 PR 同步，并更新采用记录；保留项目自己的命令和补充规则，避免整份覆盖。涉及平台设置的变化，由管理员按本清单同步配置并记录结果。
