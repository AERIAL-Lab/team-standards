# 新仓库配置清单

本页仅在**新建仓库**时看一次，平时开发不需要看。

---

## 1. 建仓基本约定

- **无需填审批表**：十余人团队在群里同步一声、确认负责人即可建仓。
- **命名与说明**：全小写 + 连字符（如 `order-service`、`admin-web`），必填一句话 `Description` 说明用途。
- **可见性与协议**：按需选 Public / Private；自有代码新项目默认采用 **MIT** 协议（根目录放 `LICENSE`）。引入外部代码或依赖时注意看清原协议，不使用来源不明或无授权的内容。

---

## 2. 复制最小模板

从本仓库按需复制到新仓库，去掉不需要的部分：

| 源文件 | 复制到目标仓库 | 是否必选 |
|---|---|---|
| `templates/PULL_REQUEST_TEMPLATE.md` | `.github/PULL_REQUEST_TEMPLATE.md` | 推荐 |
| `templates/AGENTS.md` | `AGENTS.md`（根目录） | 推荐（用 AI 协作时） |
| `LICENSE` | `LICENSE`（改成对应年份与版权人） | 开源/自有项目推荐 |
| `SECURITY.md` | `SECURITY.md` | 公开仓库推荐 |

再补齐项目自己的 `README.md`（写清项目是什么、怎么本地启动和测试）和对应技术栈的 `.gitignore`。

---

## 3. GitHub 仓库最小配置（Settings）

### Branches / Rulesets（保护 `main`）
- 保护 `main` 分支：**禁止直接推送、禁止 force push、禁止删除 `main`**。
- 要求通过 Pull Request 合并。
- **关于审批人数**：
  - **推荐（默认）**：不在平台强制勾选“所有 PR 必须 Approve”，以便成员**简单改动可以直接自合**；**涉及功能的改动**靠团队规则与 PR 模板勾选，必须 @他人 Approve 后再点合并。
  - **核心/高风险仓库**：如需平台硬卡，可勾选 `Require a pull request before merging` → `Require approvals (1)`，并按需为维护者开启 bypass。

### General（合并习惯）
- 只勾选 **Allow squash merging**（保持 `main` 历史干净）。
- 勾选 **Automatically delete head branches**（PR 合并后自动删分支）。

### Code security（防泄密）
- 开启 GitHub 自带的 **Secret scanning** 和 **Push protection**，推送前自动拦截疑似密钥。
