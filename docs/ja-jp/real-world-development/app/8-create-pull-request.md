---
title: "レッスン 8 - 機能 PR を作成してマージする"
description: "フィルター機能、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、Agent Merge を使って PR を作成します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

フィルター機能の実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストはすべて 1 つのブランチに保存されています。これらをまとめてレビューし、プルリクエストを作成します。星評価のプルリクエスト (PR) は手動でマージしました。今回は **Agent Merge** にプロセスを管理してもらいます。

> [!NOTE]
> 通常は、機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。ワークショップを簡潔にするため、フィルター機能と品質確認の一連の作業を 1 つのセッションとブランチで進め、すべてこの PR にまとめました。

このレッスンでは、次のことを行います。

- Agent Merge と、マージ ライフサイクルを自動化する方法を学びます。
- 機能 PR 全体と検証の根拠を確認します。
- レビューの後にのみ Agent Merge を許可し、PR がマージされたことを確認します。

## シナリオ

フィルター機能のワークフローでは、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys は、マージの許可を開発者の管理下に置いたまま、残りの PR 作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** は、GitHub Copilot app でプルリクエストをマージ可能にするために残っている作業を自動化します。有効にすると、アプリのセッションがプルリクエストを読み込み、CI チェックの失敗への対応、レビュー コメントへの返答、必要に応じた rebase など、マージを妨げている問題を解決します。その後、GitHub が許可するとすぐにマージします。バックグラウンドで実行され、アプリの再起動後も動作を続け、プルリクエストがマージされると自動的に停止します。

これまでは自分で **Merge pull request** を選択していました。Agent Merge に任せることもできますが、コードの編集やマージには引き続き明示的な許可が必要です。マージを許可する前に、Agent Merge が実行できる操作と作業内容をレビューしてください。

## Agent Merge で PR を管理する

コードの作成とレビューが終わったら、Agent Merge に PR の残りの処理を任せます。

1. エージェント ピッカーで **Default agent** を選択します。
2. **Create PR** の横にあるドロップダウンを選択します。
3. **Agent Merge** を選択します。ボタンが **Agent Merge** に変わります。
4. **Agent Merge** ボタンを選択してプロセスを開始します。ドロップダウンの項目を選択しただけでは開始されません。

Agent Merge の処理が始まります。次のことを行います。

- タイトルと説明を付けてプルリクエストを作成します。
- issue からセッションを開始した場合は、説明の本文で関連する issue を参照します。
- rebase を行うか、ターゲット ブランチとのマージ競合に対処します。
- CI を監視し、すべてのチェックが成功することを確認します。
- 他の開発者または Copilot code review からのフィードバックがないか PR を監視し、コメントを解決するために更新します。
- すべてが成功すると、PR を自動的にマージすることもできます。

チェックがすべて成功したら、Agent Merge に PR もマージしてもらいましょう。

5. マージを許可する前に、PR の差分と検証の根拠をレビューします。
6. **Agent Merge** の横にあるドロップダウンを選択します。
7. **Merge pull request** にチェックが付いていることを確認します。
8. エージェントに明示的にマージを依頼します。

    ```plaintext
    Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
    ```

9. 進捗を確認し、報告されたブロッカーに対処します。続行前に PR の状態が **Merged** であることを確認します。マージの許可を有効にしたことやエージェントが実行中であることは、完了の確認にはなりません。

> [!IMPORTANT]
> Agent Merge は、リポジトリの保護や権限不足を回避しません。続行する前に、それらのブロッカーを解消してください。

## まとめと次の手順

コードの生成、テストと検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。次のことを行いました。

- Agent Merge と、マージ ライフサイクルを自動化する方法を学びました。
- 機能 PR 全体と検証の根拠を確認しました。
- レビュー後にのみ Agent Merge を許可し、PR がマージされたことを確認しました。

次は[既存の Canvas を使い、トリアージ Canvas を作成][next-lesson]して、エージェントと一緒に作業を確認、計画、視覚化する方法を学びます。

## リソース

- [GitHub Copilot app で issue とプルリクエストを管理する][managing-issues-prs]
- [GitHub Copilot app について][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
