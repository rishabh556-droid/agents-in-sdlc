---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

この数回の演習では、Copilot cloud agent にユーザー エクスペリエンスの改善や機能追加に関する 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に動作しますが、タスクを監視することも重要です。

GitHub.com の[agents ページ][agents-page]など、cloud agent に割り当てたタスクを管理する方法はいくつかあります。この mission control では、オープンなプルリクエスト (PR) があるすべてのエージェント タスクを確認できます。実行内容を調べたり、進行中のセッションに指示を加えたりできます。

このレッスンでは、次のことを行います。

- agents ページで cloud agent のタスクを監視します。
- 進行中のセッションに追加機能を依頼します。

## シナリオ

エージェントに高コントラスト モードの作成を依頼した後、チームはライト モードも追加するよい機会だと考えました。サイトのスタイルを更新し、切り替え機能を追加しているため、エージェントに作業を指示して、ライト モードも高コントラスト モードと一緒に追加してもらいます。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたすべてのタスクの状態を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインの両方に表示されるタスクの一覧を確認します。たとえば、コードのドキュメント更新、ゲームを変更する API の生成、Web サイトへの高コントラスト モードの追加など、Copilot に割り当てたタスクが表示されます。
3. 実行中のタスクを選択し、Copilot が実施した内容を確認します。リポジトリのチェックアウト、作業環境の作成、MCP サーバーのセットアップ、タスクを完了するための各種手順などが含まれます。

> [!NOTE]
> 表示される手順は、Copilot の作業状況や採用したアプローチによって異なります。

4. 右側に表示されるプルリクエスト (PR) ペインも確認します。PR と変更されたファイルを表示し、作業をさらに監視できます。

## cloud agent に追加の指示を出す

現在実行中のタスクを確認できたので、高コントラスト モードの作業中にライト モードも追加するよう Copilot に依頼します。

1. 高コントラスト モードの追加に関連するセッションを選択します。表示されるタイトルは、Copilot が付けた名前や作業状況によって異なります。

    ![mission control に表示されたアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了し、作業が始まったことを示すメッセージが表示されるまで、数分間セッションを確認します。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![agents ページにある cloud agent タスクの画面で、作業中のアクティブ セッションに指示するダイアログを強調表示したスクリーンショット](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業に取り込むことを確認します。

## Copilot の作業を待つ

前回と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で作業していた手順が終わると、新しい要望を作業に組み込みます。

これにも数分かかります。その間に、ここまで学んだことを振り返ってみましょう。

## まとめと次の手順

このレッスンでは、GitHub Copilot cloud agent のタスクを監視・誘導するための中心的な場所である Copilot agents ページについて学びました。mission control を使うと、実行中・完了済みのタスクを追跡し、作業内容を確認し、進行中のタスクに追加の指示を出せます。

次のことを確認しました。

- mission control と agents ページで cloud agent のタスクを監視する方法
- 進行中のセッションに追加機能を依頼する方法

Copilot がアクセシビリティ機能を実装している間に、作成されたプルリクエストを[反復的に改善][next-lesson]しましょう。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復的に改善 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
