# 练习仓库：一起走一遍协作流程

目标：每人走完 Issue → 分支 → 草稿 PR → 检查 → 讨论 → 审批 → 合并，再两人一组处理一次冲突。可以分两次玩，不考核速度。

## 管理员准备

- 新建公开练习仓库，放入本流程、功能需求 / 缺陷表单和 PR 模板；不复制规范仓库的仓库申请表单。
- 参与成员有仓库写权限，方便建分支；审核人员名单由管理员维护。
- 保留 main 分支保护、审核组批准和必要检查。练习不需要开放删仓库、改权限、绕过审批或强推 main。
- 将 `templates/practice-ci.yml` 复制为 `.github/workflows/practice-ci.yml`；将 `templates/practice-profile.md` 复制为 `profiles/example.md`。先在 main 放好配置，再让大家开始。
- 配置 `.github/CODEOWNERS` 中的真实审核团队。每人先联系一位审核成员，避免同时找同一个人。

只用自己愿意公开的内容，不提交真实密钥、隐私和大数据文件。个人练习放 `profiles/用户名.md` 和 `sandbox/用户名/`；共享冲突文件由两人事先约好。

## 1. 开一张任务卡（Issue）

在练习仓库进入 Issues → New issue → “功能需求”，将练习写成一个具体改动目标。

- 标题：`练习：用户名完成首次贡献`
- 目标：增加自己的练习介绍，走完协作流程。
- 完成标准：PR 合并，能找到检查日志和审核记录。
- 认领自己为负责人，记下编号，例如 `#12`。

个人介绍和冲突练习都先开 Issue；不用填写真实个人资料。

## 2. 建分支，提交一点改动

可以使用自己熟悉的 Git 客户端。命令行示例：

```bash
# 第一次：点仓库 Code，复制地址，用 git clone 下载后进入仓库
# 开始前确认没有尚未保存的工作
 git status
 git switch main
 git pull --ff-only origin main
 git switch -c docs/你的用户名-intro
```

复制 `profiles/example.md` 为 `profiles/你的用户名.md`，填写昵称。为了体验检查失败，暂时删掉“想练习”那一整行。

```bash
 git diff
 git add profiles/你的用户名.md
 git diff --cached
 git commit -m "docs: 添加我的练习介绍"
 git push -u origin docs/你的用户名-intro
```

把“你的用户名”换成自己的 GitHub 用户名。提交前确认只包含自己的练习文件。

## 3. 创建草稿 PR，试着求助

1. 仓库页面点 Compare & pull request；没有提示时进入 Pull requests → New pull request。
2. `base` 选 main，`compare` 选自己的分支。
3. 填标题和描述，写 `Closes #12`（换成自己的编号），合并到默认分支后会关联关闭 Issue。
4. 点 Create pull request 右侧的小箭头，选 Create draft pull request 并创建。
5. 写“练习检查失败，尚未完成”，评论 @一位伙伴，问一个具体问题，例如“能帮我找到缺少的内容吗？”

草稿公开可见，可以看代码、评论，不能合并。草稿不会自动请求 Code Owners 审查，求助请主动 @对方。

## 4. 看一次失败日志，再修绿

- 在 PR 的 Checks 中打开 `Practice` 工作流的 `profile-check` 日志，也可从 Actions 页面寻找。
- 预期错误：个人练习文件缺少“想练习：”字段。
- 本地补回该字段并填内容，commit、push 到原分支；同一个 PR 自动更新。
- 再看检查结果，应通过。不符合预期时，贴出经检查不含敏感信息的日志求助。

体验的是“失败 → 找原因 → 修改 → 再检查”，不要求学习 CI 配置。

## 5. 体验评论、修改和批准

- 点 Ready for review，转为正式待审。
- 伙伴留一条建议，作者回复和修改；伙伴评论不代替审核组批准。
- 修改仍推到原分支，回复改了什么，确认解决后关闭相应讨论。
- 审核组非作者成员 Approve；之后若改动内容变化，重新申请批准。必要检查通过、审核讨论处理完毕后 Squash and merge。
- 删除已合并的远程分支；本地回到 main，`git pull --ff-only origin main`，确认能看到自己的文件。
- 打开 Issue 查看 PR 和关闭记录。没自动关闭时，说明原因后手动关闭。

发出审核请求后 **24 小时内回应**；未回应就联系组内另一人。回应可以是接下、说明没空或给出预计时间，不要求一天内完成所有修改。

## 6. 两人一组，体验冲突

1. 开一个冲突练习 Issue。一人先通过 PR 新建 `sandbox/两人的组名/message.txt`，内容为 `共同消息：你好`，合并 main。
2. 两人都同步 main，确认拿到同一文件，再各自建分支。
3. 各自把同一行改成不同内容，各提交 PR，关联同一个练习 Issue；第一份先不写 Closes。
4. 审核合并第一份 PR，另一份通常会显示冲突。第二位成员在自己的分支执行：

```bash
 git status
 git fetch origin
 git merge origin/main
```

5. 打开文件，看 `<<<<<<<`、`=======`、`>>>>>>>`。一起商量最终文字，保留所需内容并删掉标记。
6. 只暂存解决后的文件，commit、push，通过检查和审核后合并，最后关闭练习 Issue。

需要退出仍在进行中的合并时，可以 `git merge --abort`。不要通过强推 main 或删除别人的分支解决冲突。

## 7. 可选：体验撤销

在自己的目录里通过 PR 合并一句练习文字，再开 Issue，用新分支、新 PR 撤销这次改动。可以手动恢复原文，也可请伙伴演示 `git revert`。观察撤销记录，不需要重写 main 历史。

## 玩完自查

- [ ] 找得到 Issue、PR、检查日志和合并记录
- [ ] 知道草稿如何转正式待审、原 PR 如何更新
- [ ] 体验过失败检查、评论回复和批准
- [ ] 和伙伴处理过冲突
- [ ] 知道卡住时 @谁、24 小时无回应时联系另一位审核成员

参考：[创建 PR](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request)、[草稿转换](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/changing-the-stage-of-a-pull-request)。
