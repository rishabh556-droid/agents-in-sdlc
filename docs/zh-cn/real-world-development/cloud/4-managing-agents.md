---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前几项练习中，你让 Copilot 云智能体处理了三个改进用户体验和添加功能的任务。云智能体虽然会异步自主工作，但仍需监控这些任务。

可以通过多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个 mission control 中，可以查看所有拥有未关闭拉取请求 (PR) 的智能体任务，了解它们执行的操作，也可以引导正在运行的会话。

本课将完成以下任务：

- 查看智能体页面，监控云智能体任务。
- 在会话运行期间提出新要求。

## 场景

将高对比度模式任务分配给智能体后，团队意识到也可以同时添加浅色模式。既然正在更新网站样式并添加切换功能，就可以将这项功能一并实现。你将引导智能体，在添加高对比度模式的同时也实现浅色模式。

## 查看 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主区域和左侧区域中的任务列表。列表中应包含你分配给 Copilot 的任务，例如：
   - 更新代码库文档。
   - 为游戏管理功能生成 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 创建 Copilot 的工作环境。
   - 设置 MCP 服务器。
   - 执行完成任务所需的其他步骤。

> [!NOTE]
> 具体步骤会因 Copilot 的工作进度和采用的方法而异。

4. 同时查看右侧显示的 PR 区域，了解 PR 和已更改文件，以便进一步监控。

## 引导云智能体

了解当前运行的任务后，请求 Copilot 在实现高对比度模式的同时添加浅色模式。

1. 选择正在添加高对比度模式的会话。会话标题会因 Copilot 使用的名称和当前进度而异。

    ![Mission control 中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到设置完成并开始执行任务。出现类似下方的消息时，就表示已开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示词：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面中的云智能体任务，以及突出显示的“Steer active session while Copilot is working”对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示词。
5. 注意 Copilot 会确认收到提示词，并将其纳入工作流程。

## 让 Copilot 继续工作

与之前一样，Copilot 会继续处理更新后的任务。在收到消息时，它会先完成当前步骤，然后将新要求纳入工作流程。

这同样需要几分钟，可以利用这段时间回顾已学内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot 云智能体任务的中心位置。在这里可以跟踪所有正在进行和已完成的任务、审查已执行的工作，也可以重定向正在运行的任务以调整范围或补充指导。

你探索了以下概念：

- 使用 mission control 和智能体页面监控云智能体任务。
- 重定向正在运行的会话，要求添加功能。

Copilot 正在完成无障碍功能。接下来，[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
