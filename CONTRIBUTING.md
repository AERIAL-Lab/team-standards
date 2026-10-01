# CONTRIBUTING — 提交与审批流程

提交前确认任务、改动范围和验证方式。

---

## 第一部分：先学会基本操作

Git 基本操作见 [git-github-basics.md](git-github-basics.md)，首次贡献请在练习仓库按 [练习流程](practice-walkthrough.md) 走一遍。可以借助 AI 理解操作，提交前仍要检查改动。

> **一个分支只做一件事。** 做完、合并、删分支，下一件事开新分支。


---

## 第二部分：分支与提交规范

### 分支命名

| 前缀 | 用途 | 示例 |
|---|---|---|
| `feature/` | 新功能 | `feature/login-page` |
| `fix/` | 修 bug | `fix/order-total-rounding` |
| `docs/` | 只改文档 | `docs/update-readme` |
| `chore/` | 构建、依赖、杂务 | `chore/upgrade-jest` |
| `refactor/` | 重构（不改行为） | `refactor/split-user-module` |

### Commit message（简化版 Conventional Commits）

格式：`<类型>: <一句话说明>`，中文英文都可以，说清楚即可。

```
feat: 登录页增加验证码
fix: 修复订单金额四舍五入错误
docs: 补充部署说明
test: 为支付模块补单元测试
chore: 升级 eslint 到 9.x
```

每次 commit 应表达一个清晰的小步骤。及时提交和同步，便于追踪、审查和处理冲突。

---

## 第三部分：PR 流程（核心）

### 任务认领

开工前在对应 Issue 留言，确认负责人并更新 Assignee，避免重复开发；没有设置权限时请维护者协助。暂时不做或需要转交时，说明已完成内容、剩余事项和相关分支或 PR，再调整负责人。Discussions 中形成的明确改动，应建立并链接对应 Issue。

### 规则

1. **一个 PR 只做一件事**，尽量保持小规模，参考 **400 行有效改动**（不含测试 fixture、自动生成的锁文件）；超过时说明不能拆分的原因，由 reviewer 判断。
2. 标题简明说明改动，例如：`feat: xxx`。正文按模板填空。**所有修改先开 Issue，再在 PR 中关联**，小文档修改也一样，帮助新人养成记录和追溯的习惯。
3. **正式申请批准前，完成适用的检查**；CI 失败且无法自行解决时可以求助。可用 Draft PR（草稿）展示未完成的改动，写清卡点并 @需要协助的人；准备好后点 Ready for review 转为正式待审。合并前必需检查仍须通过。
4. **审批规则**：所有改动由审核组中至少一名非作者成员 approve。审核组由管理员组成，成员名单在 GitHub 团队中维护，按实际审核需求调整。审核请求发出后 **24 小时内回应**；未回应就联系组内另一人接手。回应不等于必须一天内审核完毕。批准后 PR 改动内容发生变化，须由审核组中非作者成员重新批准；合并前确认必要检查通过、审核讨论已处理。
5. 合并方式统一用 **Squash and merge**（把一堆零散 commit 压成一条，main 历史保持干净）。
6. 合并后删除分支。

### PR 提交前自查（5 条）

- [ ] 这个 PR 只做一件事
- [ ] 正式待审前已完成适用的本地检查；不适用时说明理由和验证方式（草稿求助可注明尚未完成）
- [ ] 我说得清这个 PR 做了什么、怎么验证（代码可以是 AI 写的，行为我负责）
- [ ] 没有误提交密钥、大文件、构建产物
- [ ] PR 描述按模板填完了，相关 issue 已关联

---

## 第四部分：常见错误速查

| 症状 | 正确做法 |
|---|---|
| 直接推 main 被拒绝 | 正常，所有人都不能直推。开分支走 PR |
| 审核请求 24 小时未回应 | 联系审核组另一位成员接手 |
| 改完发现 main 已更新 | 先确认工作区已保存，在自己的分支执行 `git fetch origin`、`git merge origin/main`，解决冲突后再推 |
| 不小心 commit 了密钥 | **立即**告诉管理员轮换密钥，再清理历史，不要自己悄悄删 |
| PR 太大被退回拆分 | 按功能边界拆成多个 PR，逐个提交 |

---

## 相关文档

- Code review 怎么审：见 [repo-governance.md](repo-governance.md) 的审批细则
- 用 coding agent 写代码：必读 [coding-agent-guide.md](coding-agent-guide.md)
- 写测试：[modular-testing.md](modular-testing.md)
