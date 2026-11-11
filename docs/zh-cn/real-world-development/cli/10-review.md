---
title: "第 10 课 - 总结与后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用的自定义配置和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你已在一套连续的 Tailspin Toys 工作流中使用 GitHub Copilot CLI。你：

- 准备了 Codespace、安装 Copilot CLI、探索项目，并找到已创建的筛选功能议题。
- 添加了星级评分，在转发的浏览器中检查结果，并手动合并了第一个拉取请求 (PR)。
- 从筛选功能议题开始，在 Plan 模式中确定方案，在 Autopilot 模式中构建，并在 Interactive 模式中审查。
- 使用自定义指令引导智能体，再自定义现有的 `quality-checks` 技能，用它运行单元测试、lint 和类型检查。
- 添加 Playwright 模型上下文协议 (MCP) 服务器，并用它在真实浏览器中体验筛选功能。
- 创建并选择质量保证 (QA) 自定义智能体，以评估需求、覆盖范围、技能结果和浏览器证据。
- 审查完整的筛选功能更改，并授权 Agent Merge 合并筛选功能 PR。
- 探索用于管理上下文、模型、共享和可选云端委派的斜杠命令。

## 交付的内容

本研讨会有两个 PR 里程碑，每个里程碑都从更新后的 `main` 使用自己的分支：

1. **星级评分**：在游戏卡片上显示现有的 `starRating`，并明确显示未评分状态。
2. **筛选功能及质量工作流**：实现筛选功能，更新指令并将其应用到该功能，自定义 `quality-checks` 报告，创建 QA 配置文件，并添加相关测试。

从规划筛选功能到创建其 PR，你一直使用同一对话和分支。为简化研讨会流程，我们将这些工作合并到一个 PR 中。

## 不同类型的验证

你通过多种方式检查代码：自动化测试、自己的浏览器检查，以及 Copilot 通过 MCP 进行的浏览器探索。`quality-checks` 技能运行单元测试、lint 和类型检查，并按新的格式报告结果。创建 PR 前，QA 将这些结果与需求和测试覆盖情况的审查结合起来。

新增测试应填补真实缺口；QA 运行不需要添加测试也可能完全正确。授权合并前请审查代码和证据，并在更改后更新受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响其工作。在本研讨会中，你更新了指令、自定义了技能、创建了 QA 配置文件并配置了 MCP 服务器。应在不同对话中复用这些自定义项，并根据团队需求调整。指令设定标准，技能描述可重复执行的任务，自定义智能体定义专业角色，MCP 服务器连接外部工具。请审查实际更改和工具结果，而不只是智能体的摘要。

根据任务选择适合的**模式和模型**。使用 **Plan** 在构建前思考方案，使用 **Interactive** 参与范围明确的更改，并对范围明确的任务使用 **Autopilot**。日常工作可选择更快的模型；复杂工作则选择能力更强的模型。

上下文与基础设施同样重要。清楚说明要构建*什么*、*为什么*构建以及*如何*构建，会显著影响输出。

## 更多探索内容

你已了解核心工作流。还有一些值得探索的 CLI 功能：

- `/review`：让代码审查智能体分析更改。
- `/rubber-duck`：讨论问题并获得另一种观点。
- `/fleet`：并行协调相互独立的子任务。
- `/worktree`：隔离处理另一项任务。
- `/delegate`：将任务交给 Copilot 云智能体。

## 后续步骤

熟练使用任何工具的最佳方式都是持续使用。可将其用于生产代码、业余项目，或那个构思多年却始终没有动手构建的小应用。与团队分享经验，也向团队学习，并一如既往地探索文档。

若要从终端扩展 Tailspin Toys，请继续学习可选的 [Foundry Backer Concierge 系列课程][foundry]。若要比较其他环境，请查看 [VS Code 研讨会][vscode]、[GitHub Copilot app 研讨会][app]或 [Copilot 云智能体研讨会][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
