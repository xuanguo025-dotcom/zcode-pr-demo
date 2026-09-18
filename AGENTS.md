# AGENTS.md — zcode-pr-demo

本仓库是 GitHub PR 工作流试验场，面向 AI（ZCode）与人工协作。

## 铁律

1. main 受保护，一切改动必须走 PR；不绕过（不用 bypass、不改保护规则，除非用户明示）。
2. 破坏性操作（关闭他人 PR、force push、删分支、删仓库、改保护/规则）先向用户确认。
3. 令牌、密钥不进仓库、不进提交、不进日志。
4. 合并默认 squash；合并后删除功能分支。

## 工作参考

分支命名、commit/PR 规范、标签约定、AI 工具序列：见 `docs/PR-GUIDE.md`。
