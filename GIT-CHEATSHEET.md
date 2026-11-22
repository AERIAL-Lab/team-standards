# Git 与 GitHub 一页速查

> **先说重点：你不需要死记硬背这些命令！**
> 建议花 3 分钟大致理解下面的核心概念，知道每一步在干什么；日常的建分支、写 commit、解简单冲突、提 PR，**完全可以直接交给 AI（Coding Agent）来操作**，你负责定方向和把关即可。

---

## 一、5 个必懂概念

| 概念 | 一句话理解 |
|---|---|
| **仓库（Repo）** | 项目的总文件夹 + 所有历史存档 |
| **`main` 分支** | 团队共享的稳定主线，**不直接往上面写代码** |
| **工作分支（Branch）** | 从 `main` 拉出来的“草稿副本”，改坏了也不影响别人 |
| **Commit（提交）** | 本地打一个存档点，附一句说明改了什么 |
| **PR（Pull Request）** | “我改好了，申请合回 `main`”——简单改动可自合，功能改动找人看一眼再合 |
| **冲突（Conflict）** | 你和别人改了同一个文件的同一行，需要人工（或让 AI 辅助你确认）决定留哪版 |

记住两个方向：**`pull` 是把最新代码拉回本地，`push` 是把本地改动推到 GitHub。**

---

## 二、日常 5 步走（标准流程）

```bash
# 1. 切回 main 并拉取最新代码（每次开新任务前都做）
git switch main
git pull --ff-only origin main

# 2. 拉一条自己的工作分支
git switch -c feat/my-task

# 3. 改代码（或让 AI 改），然后检查改了什么
git status
git diff

# 4. 暂存并存档（commit）
git add <你改的文件>
git commit -m "feat: 一句话说明改了什么"

# 5. 推到 GitHub，去网页点 "Compare & pull request" 提 PR
git push -u origin feat/my-task
```

### 偶尔会用到的 2 个救场命令

```bash
# 干活干一半，main 更新了 / PR 提示有冲突：把最新 main 合并进来
git fetch origin
git merge origin/main
# （如果有冲突，解完冲突后 git add . && git commit && git push）

# 改了一半临时要切分支修急事：先收进口袋，忙完再倒出来
git stash
# ...切分支处理完回来...
git stash pop
```

---

## 三、把 Git 交给 AI 做时，你只需要盯住 3 件事

日常可以直接对 AI 说：“帮我从最新 main 拉个分支 `fix/xxx`，提交刚才的改动并提个 PR”。你只需要确认：

1. **别直接在 `main` 上提交**：确认 AI 已经切到了新分支。
2. **别把不该交的传上去**：提 PR 前扫一眼 `git status` 或改动文件列表，确认没有密钥、`.env`、构建产物或无关大文件。
3. **拦截危险操作**：如果 AI 试图运行 `git push --force`、`git reset --hard` 或删除别人分支，**先停下来确认**，别直接点允许。

---

## 四、常见问题

- **直接 `push` 到 `main` 被拒了？** 正常，分支保护生效了。建个新分支推上去提 PR 就行。
- **改乱了想放弃某个文件的修改？** 运行 `git restore <文件路径>`（或直接让 AI 帮你还原指定文件）。
- **PR 提完发现还要继续改？** 不用重开 PR，在同一个分支上继续改、commit、push，PR 会自动更新。
- **误提交了密钥怎么办？** 立刻通知管理员作废/轮换密钥，再一起清理历史，不要自己悄悄删文件了事。
