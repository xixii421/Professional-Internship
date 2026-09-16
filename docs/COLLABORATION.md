# 三人协作与审核记录

本文档规定本仓库的开发、审核和合并流程。GitHub 的 Commit、Pull Request、Review、Actions 记录作为协作过程的原始证据。

## 成员与审核关系

| 代号 | GitHub 账号 | 主要职责 | 必须审核 |
| --- | --- | --- | --- |
| A | @xixii421 | 项目协调、集成与开发 | B 提交的 PR |
| B | @BreezeMira | 功能开发与性能验证 | A 提交的 PR |
| C | @RiceXi | 测试、实验、文档及功能开发 | 由 A、B 轮流审核 C 的 PR |

具体任务以 Issue 和 PR 描述为准，三人都应提交可识别的代码或文档变更。

## 分支策略

- `main`：稳定分支，只通过 Pull Request 合入，不直接提交。
- 每项任务建立一个短期分支，不建立长期个人分支。
- 分支命名：`feat/<成员>-<任务>`、`fix/<成员>-<问题>`、`test/<成员>-<范围>`、`docs/<成员>-<主题>`。
- 示例：`feat/a-prefix-sharing`、`feat/b-qwen-runtime`、`test/c-swap-benchmark`。
- PR 合并后删除短期分支；新任务重新从最新 `main` 建分支。

## 标准流程

1. 在 Issue 或任务清单中写清负责人、验收条件和审核人。
2. 开发者从最新 `main` 创建短期分支并分次提交。
3. 推送分支并创建 PR，完整填写 PR 模板。
4. A 的 PR 指定 B，B 的 PR 指定 A；C 的 PR 由 A、B 轮流审核。
5. 审核人至少检查实现、边界条件、测试结果和文档，并使用 Review 留下意见。
6. 作者根据意见继续提交到同一分支，在 PR 中说明修改位置。
7. 自动测试通过、讨论全部解决且至少一名他人批准后，使用 Squash and merge 合入。
8. 删除已合并分支，开始下一项任务。

## 提交与审核要求

- 提交信息使用 `feat:`、`fix:`、`test:`、`docs:`、`refactor:` 或 `chore:` 前缀。
- 禁止多人共用同一个 GitHub 账号提交；每人配置自己的 Git 用户名和邮箱。
- 审核人不得只口头确认，应在 GitHub 上执行 Approve 或 Request changes。
- 发现问题时先留下具体评论，作者修改后再解决讨论，形成“意见—修改—确认”的证据链。
- 作者不得批准自己的 PR，不得绕过 `main` 保护规则。

## 建议任务分配

| 工作包 | 建议负责人 | 审核人 | 主要目录 |
| --- | --- | --- | --- |
| 分页、COW、换页核心 | A | B | `src/memory/`、`src/data/` |
| 推理接入与性能路径 | B | A | `src/control/`、`src/compute/`、`run.py` |
| 测试、实验与说明 | C | A/B 轮流 | `test/`、`bench/`、`docs/`、`scripts/` |

任务分配可调整，但调整必须记录在对应 Issue 或 PR 中。

## 可核验的协作证据

提交材料时建议同时导出或截图：

- 仓库 Contributors/Insights 页面，证明三人各自提交；
- 已合并 PR 列表，证明任务通过分支完成；
- A 审核 B、B 审核 A 的 Review 页面；
- Request changes 后作者追加提交、审核人再批准的过程；
- Actions 自动测试通过记录；
- 本文档与各 PR 模板中的分工、测试和审核结论。
