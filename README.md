# 团队开发规范

原则：**少流程、守底线、把重复劳动交给 AI。**

## 记住这 4 条就能干活

1. **不直推 `main`，改动走 PR**：拉分支干活，PR 统一用 **Squash and merge** 合并，合完删分支。
2. **PR 分级合并**：
   - **简单改动**（改文档、错别字、注释、微调样式/文案）→ 自检通过后**允许自己合并**。
   - **涉及功能**（新功能、修 Bug、改逻辑/接口/依赖/配置）→ **不允许自己合并**，至少找 1 位其他成员 Approve 后再合。
3. **鼓励用 AI 写代码、跑 Git，但人负责结果**：大致理解 Git 流程和需求边界后，实现、测试、提 PR 都可以交给 AI；提交前人要看过 diff、跑过验证，出问题自己兜底。
4. **守住安全底线**：不提交密钥、Token、密码和 >1MB 的大文件；不把敏感信息贴进 AI 对话框。

---

## 文档导航

| 文档 | 给谁看 / 什么时候看 |
|---|---|
| [WORKFLOW.md](WORKFLOW.md) | **日常必读**：PR 分级合并、分支/Commit 习惯、AI 协作边界、验证要求 |
| [GIT-CHEATSHEET.md](GIT-CHEATSHEET.md) | **Git 速查**：5 个核心概念 + 常用命令 + 让 AI 代劳 Git 的注意事项 |
| [REPO-SETUP.md](REPO-SETUP.md) | **建新仓库时看**：新仓库最小配置清单与模板复制指引（平时不用看） |
| [SECURITY.md](SECURITY.md) | 发现漏洞或密钥泄露时的私下处理方式 |

## 开箱即用模板（`templates/`）

- [templates/PULL_REQUEST_TEMPLATE.md](templates/PULL_REQUEST_TEMPLATE.md) — 极简 PR 模板
- [templates/AGENTS.md](templates/AGENTS.md) — AI 协作者通用约定，复制到项目根目录即可使用
