---
layout: post
categories: git
---
Question:

Reply in Chinese (Simplified).
The following is a search input in a search engine, giving useful content or solutions and as much information as you can related to it, use markdown syntax to make your answer more readable, such as code blocks, bold, list:
--reapply-cherry-picks

Answer:

您好，这是必应。我将用简体中文回复您。

--reapply-cherry-picks 是一个 git 命令的选项，它可以在 rebase 的过程中重新应用所有干净的 cherry-pick，而不是预先丢弃它们。<sup>1</sup> cherry-pick 是指从一个分支选择一个提交，并将其应用到另一个分支。<sup>2</sup> 这与其他方式，如合并和变基，它们通常将多个提交应用到另一个分支，有所不同。cherry-pick 就像变基一样，是一个高级的概念和强大的命令。

--reapply-cherry-picks 可以提高 rebase 的性能，因为它可以避免读取所有上游的提交。<sup>1</sup> 如果这些 cherry-pick 在变基后变为空，因为它们包含了已经在上游的部分更改，那么对它们的处理由 --empty 选项控制。<sup>1</sup>

--reapply-cherry-picks 的用法示例：

- `git rebase origin/main --reapply-cherry-picks`：将当前分支变基到 origin/main，并重新应用所有干净的 cherry-pick。
- `git rebase --reapply-cherry-picks -i HEAD~3`：交互式地变基当前分支的最近三个提交，并重新应用所有干净的 cherry-pick。

您可以参考以下网址了解更多关于 --reapply-cherry-picks 和 cherry-pick 的信息：

- <sup>1</sup> https://stackoverflow.com/questions/61905448/git-cherry-pick-and-then-rebase
- <sup>2</sup> https://www.geeksforgeeks.org/git-cherry-pick/
- <sup>3</sup> https://git-scm.com/docs/git-cherry-pick
- <sup>4</sup> https://github.com/magit/magit/issues/4618

希望这些信息对您有帮助。😊

\-
\[1]: [Git cherry pick and then rebase - Stack Overflow](https://stackoverflow.com/questions/61905448/git-cherry-pick-and-then-rebase)
\[2]: [Git - Cherry Pick - GeeksforGeeks](https://www.geeksforgeeks.org/git-cherry-pick/)
\[3]: [Git - git-cherry-pick Documentation](https://git-scm.com/docs/git-cherry-pick)
\[4]: [Add --reapply-cherry-picks option to rebase menu #4618 - GitHub](https://github.com/magit/magit/issues/4618)

<hr/>

