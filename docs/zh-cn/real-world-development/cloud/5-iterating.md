---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作成果

在本实验中，你使用 GitHub Copilot 完成了多项改进用户体验和添加功能的任务：为代码添加文档、构建供设计团队迭代的相关游戏功能，以及实现包含高对比度和浅色模式切换开关的无障碍功能。现在来检查代码更改，必要时向 Copilot 提供反馈，进一步改进结果。

### 场景

如前所述，加入生成式 AI 并不会改变软件设计和 DevOps 的基本原则。我们始终需要审查生成的代码，并遵循正常的 DevOps 流程。现在先审查 GitHub Copilot 为文档、相关游戏功能和无障碍功能提出的更改，然后再启用团队其他成员的审查。

## GitHub Copilot 云智能体的安全机制

Copilot 云智能体会在无人监督的情况下异步执行任务，因此设置了一些安全限制：

- Copilot 仅对存储库具有读取权限，只能写入自身用于提交代码的分支。
- 云智能体在 GitHub Actions 中运行，并在单独的临时环境中工作。
- 运行任何 GitHub Actions 工作流前，都必须由人工批准。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，包括 MCP 服务器。

## 审查生成的文档

首先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)，其中包含为代码添加的文档。通过 GitHub.com 上的标准 PR 界面完成审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限访问外部资源，包括外部 MCP 服务器。如果需要，可以[自定义或禁用 Copilot 云智能体的防火墙][agent-firewall]。

1. 在 github.com 上打开存储库。
2. 选择 **Pull Requests**，打开 PR 列表。
3. 打开标题类似 **Add missing documentation** 的 PR。标题也可能更详细。

> [!NOTE]
> 如果 Copilot 尚未完成任务，PR 标题中会包含 **[WIP]**。此时请等待 Copilot 完成，这可能需要几分钟。等待时可以休息一下，或回顾已学内容。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新增的 TSDoc 文档注释及其他文档。具体更改可能有所不同。

    审查时，留意 TSDoc 文档注释、TypeScript 规范和文件注释头。这些要求来自练习 2 中查看的自定义指令文件。

6. 审查完成且结果符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应出现在 PR 的检查区域中。如果一切正常，单体 Astro 应用的项目检查将通过。此步骤可能需要几分钟。

## 请求 GitHub Copilot 修改

与 Copilot 协作处理 PR 并非单向过程。你可以像在 PR 或代码行内评论中提及团队成员一样，提及 Copilot。Copilot 会读取评论并启动新会话来处理请求。由于结果具有非确定性，无法提供适用于所有情况的固定提示词。可以让 Copilot：

- 在每个代码文件开头添加简短注释，说明文件用途。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 为 Astro 应用结构添加 README。

1. 评论并提及 **@copilot**，请求它修改生成的文档。可以使用上述建议，也可以提出其他文档改进要求。
2. 选择 **View Session**，观察 Copilot 如何启动新会话并应用更改。
3. 选择 **Back to pull request** 返回 PR。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中应出现新的提交。
5. 选择 **Files changed** 选项卡，审查更改。

可以继续迭代，直到满意为止。完成后，可以将 PR 从草稿转换为可审查状态，再合并到 main 分支。

![将 PR 转为可审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

现在查看 Copilot 为解决“在游戏详情页显示相关游戏”议题而创建的 PR。

1. 在 GitHub.com 上打开存储库。
2. 选择 **Pull Requests** 选项卡。
3. 打开标题类似 **Show related games on the game details page** 的 PR。标题也可能更详细。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查完成且结果符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流提示。
7. 如果有工作流等待批准，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 工作流应出现在 PR 的检查区域中。如果一切正常，单体 Astro 应用的项目检查将通过。此步骤可能需要几分钟。
9. **可选：** 可以在 Codespace 中切换到该分支，手动测试相关游戏功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已构建相关游戏功能。与之前一样，可以继续让 Copilot 云智能体迭代更新。例如，可以要求它调整显示的相关游戏数量，或添加文件注释头和 TSDoc 文档注释（注意，分配此任务时尚未更新自定义指令）。与之前一样，在 **Conversation** 选项卡中添加评论即可提出请求，Copilot 会读取评论并启动新会话。

## 审查无障碍功能

最后，审查通过无障碍自定义智能体实现的功能。此 PR 应同时包含练习 3 中分配的高对比度模式，以及练习 4 中在 mission control 提出的浅色模式。

1. 在 GitHub.com 上打开存储库。
2. 选择 **Pull Requests** 选项卡。
3. 打开标题类似 **Add high contrast mode to website** 的 PR。标题也可能更详细。

> [!NOTE]
> 如果 Copilot 尚未完成任务，PR 标题中会包含 **[WIP]**。请等待 Copilot 完成，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 检查实现，尤其留意：
   - 用于切换模式的 UI 组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（ARIA 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 审查完成且结果符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流提示。
8. 如果有工作流等待批准，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应出现在 PR 的检查区域中。如果一切正常，单体 Astro 应用的项目检查将通过。此步骤可能需要几分钟。
10. **可选：** 可以在 Codespace 中切换到该分支，手动测试无障碍功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换开关，并确认页面重新加载后仍会保留设置。

无障碍自定义智能体帮助 Copilot 遵循无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可以像处理前面 PR 一样，在评论中提及 **@copilot** 并请求修改。

## 可选练习 — 继续委派任务

云智能体最适合处理实际待办事项，让你可以先做其他工作。可以在自己的存储库中创建更多议题并分配给 Copilot，逐步培养这种工作方式。以下是一些建议：

- 在游戏详情页添加支持者意向表单。
- 为游戏列表页添加分页。
- 为数据访问 helper 添加输入验证和错误处理。

## 总结

你已完成云智能体学习路径。在这些课程中，你：

- **检查了存储库自带的自定义指令文件**，以便之后观察其对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，观察它设置环境、制定计划并异步执行任务。
- **创建并使用无障碍自定义智能体**，添加高对比度和浅色模式切换开关。
- **使用 Copilot 智能体页面作为 mission control**，监控并引导无障碍功能会话。
- **审查并迭代云智能体创建的拉取请求**，提及 `@copilot` 请求修改并批准工作流。

## 回顾与后续步骤

云智能体学习路径已完成。其他学习路径可以帮助你继续探索 GitHub Copilot：

- 🖥️ **[VS Code 学习路径](../../vscode/)** — 在 IDE 中体验 Copilot Chat 代理模式和 MCP 集成。
- 💻 **[CLI 学习路径](../../cli/)** — 在终端中交付两项经过审查的更改，并使用 Plan 和 Autopilot 模式、智能体技能、QA 自定义智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

也可以在自己的存储库中尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
