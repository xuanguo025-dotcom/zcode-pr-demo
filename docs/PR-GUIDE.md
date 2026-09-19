# PR 工作参考（PR Workflow Guide）

本仓库（`zcode-pr-demo`）是 PR 工作流试验场：main 受保护，一切改动通过 PR 合入。本文是流程规范唯一来源，AI 与人共同遵守。

## 分支模型

| 分支 | 用途 | 约束 |
|---|---|---|
| `main` | 稳定主干 | 保护：禁直推、禁强推/删除、线性历史、改动仅经 PR |
| `<类型>/<主题>` | 功能分支 | 从最新 `main` 拉出，合并后删除 |

分支命名：`feature/xxx`（新功能）、`fix/xxx`（修复）、`docs/xxx`（文档）、`chore/xxx`（杂务）。主题用短横线小写英文，如 `docs/pr-workflow-guide`。

## Commit 与 PR 规范

- 标题：祈使句一行（约 50 字符内），如 `Add PR workflow guide`；squash 合并后它就是 main 上的提交标题。
- 一个 PR 只做一件事；大改动拆成多个 PR。
- PR 描述按仓库模板四段：改了什么 / 为什么改 / 怎么验证 / 影响面。
- 合并策略默认 **squash**（一个 PR = main 上一个提交）；需保留逐提交历史时用 merge 并在 PR 里说明。

## 标准流程

1. 从 main 建分支
2. 提交改动
3. 开 PR，打标签（见下）
4. 对照模板自查四段是否写清
5. 评审：评论 / 变更请求，有分歧先讨论后改码
6. **合并须用户在聊天中明确确认**——AI 只备好 PR 并给摘要，不得自主合并；确认后打 `approved` 标签、squash 合并
7. 删除功能分支

## 标签约定

| 标签 | 含义 |
|---|---|
| `needs-review` | 待评审 |
| `approved` | 用户已在聊天确认，可以合并 |
| `ai-generated` | AI 产出的改动 |
| `chore` / `documentation` / `bug` / `enhancement` | 常规分类 |

## AI（ZCode）工具序列

MCP 工具（会话已连接 github 服务器时优先用）：

- 只读：`list_pull_requests`、`pull_request_read`（get / get_diff / get_files / get_commits / get_reviews / get_review_comments / get_check_runs）、`search_pull_requests`
- 写入：`create_branch` → `push_files` → `create_pull_request` → `add_issue_comment` / `pull_request_review_write` → `merge_pull_request`
- MCP 未覆盖的端点（分支保护、标签、仓库设置等）走 REST API：`https://api.github.com`，同令牌放 `Authorization: Bearer` 头。

典型建 PR 序列（本仓库验证过）：建分支 → 推文件 → 建 PR → 打标签 → 评论 → squash 合并 → 删分支。

## 红线（用户政策，2026-09-18 确认）

- **范围**：AI 仅操作本仓库；其他仓库（用户的、第三方的）一律不动，除非用户明示授权。
- **合并**：一律用户确认制——AI 备好 PR 并给摘要，用户在聊天里同意后才执行合并。
- **语言**：commit/PR 标题用英文祈使句，正文用中文（按模板四段）。
- 不 force push、不改分支保护/规则，除非用户明确要求。
- 令牌不进任何提交内容；发现泄露立即撤销换新。
- 对他人开的 PR：可以评论、可以提变更请求，合并与否由作者/维护者决定。
