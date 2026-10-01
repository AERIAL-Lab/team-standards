# CI 模板接入说明

**模板用于提供配置起点。维护者须根据项目补齐依赖、命令和权限，实际验证后再设为必需检查。工作流是否启用、运行是否通过，以目标仓库记录为准。**

## 选择模板

| 仓库类型 | 使用方式 |
|---|---|
| 任意项目，包括文档仓库 | `templates/ci.yml` → `.github/workflows/ci.yml`，检查变更文件大小和 PR 提交中的疑似密钥 |
| Node + Jest | 增加 `templates/ci-node.yml` → `.github/workflows/ci-node.yml`，先配齐脚本和依赖 |
| 练习仓库 | 增加 `templates/practice-ci.yml` → `.github/workflows/practice-ci.yml`，它不代替密钥检查 |
| Python、其他框架 | 保留通用检查，根据实际测试命令另配代码检查，不照搬 Jest 参数 |

文件在 templates/ 中不会运行。示例使用 main 为目标分支，其他名称需同步调整。

## 检查范围与配置原则

- 大文件检查用零分隔路径和 Git 对象大小，不拼接 shell、不跟随工作区符号链接。支持空格等特殊文件名；只检查最终变更文件，不声称检查全部历史大对象。
- 密钥扫描改用 Gitleaks CLI 容器，避免 gitleaks-action 的组织许可证依赖，不需要组织 Secret。扫描 PR 提交范围，输出脱敏；不能保证发现所有秘密。
- 覆盖率报告固定为 `coverage/cobertura-coverage.xml`，缺失就失败，生成端需使用相同路径。
- 示例明确工具版本，项目内工具用依赖锁文件安装，避免无版本临时运行 npx。
- 许可证改为报告加人工审查；不按许可简称一律禁止依赖。
- 工作流只读仓库、checkout 不保存凭据；使用 pull_request，不为外部贡献代码改用高权限 pull_request_target。

## Node + Jest 需先准备

1. package.json 定义 `lint`、`test:coverage`、`licenses:ci`。工具放 devDependencies，选明确版本并提交 package-lock.json。
2. test:coverage 示例：`jest --ci --coverage --coverageDirectory=coverage --coverageReporters=text --coverageReporters=cobertura`。Jest 配置明确实际源码的 collectCoverageFrom，避免未导入的新文件漏出统计；TS / ESM 按项目配置。
3. licenses:ci 调用已安装并锁定的报告工具。例如选用 license-checker-rseidelsohn 后，脚本为 `license-checker-rseidelsohn --json`，包含开发依赖供审查。这里不临时安装，也不指定未经验证的最新版本。
4. 70% 是示例门槛，负责人确定实际要求并更新配置与 README。无可统计改动时按不适用处理；缺报告不算不适用。纯文档仓库不启用 Node 工作流。
5. 审计失败要查具体依赖和修复方式，不用 `|| true` 隐藏失败；历史问题需有负责人、记录和处理期限。

## 版本和首次启用

完整版本号是示例，不代表最新或已验证。启用时核对官方发布及兼容性，将 Action 固定为核实后的完整 commit SHA，第三方容器固定为核实后的 digest，不凭记忆填摘要。更新走 PR。

Node / Python 小版本与工具间接依赖仍可能变化，不宣称完整环境锁死；需要更强可复现性时补全工具依赖锁和哈希。

在试点仓库确认正常改动通过、超限文件失败、练习格式错误可定位、覆盖率不足失败、报告缺失失败。扫描测试仅用工具的合成样例，不提交真实密钥。

旧仓库首次接入另做历史秘密排查；PR 范围扫描不是历史安全证明。GitHub Secret scanning / Push protection 按接入清单在平台启用。

最后才把已跑通的任务设为必需检查：repository-checks、Node 仓库的 node-checks、练习仓库的 profile-check，以平台实际显示为准。

参考：[GitHub Actions](https://docs.github.com/en/actions/get-started/understand-github-actions)、[Gitleaks CLI](https://github.com/gitleaks/gitleaks)、[示例版本](https://github.com/gitleaks/gitleaks/releases/tag/v8.24.2)、[diff-cover 示例版本](https://pypi.org/project/diff-cover/9.2.4/)、[Jest 配置](https://jestjs.io/docs/configuration)、[许可证报告工具](https://github.com/plt-software/license-checker)。
