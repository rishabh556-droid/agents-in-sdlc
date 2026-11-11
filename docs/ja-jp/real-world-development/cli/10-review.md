---
title: "レッスン 10 - 振り返りと次の手順"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、関連リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys で一連のワークフローを完了しました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールし、プロジェクトを確認して、登録済みのフィルター機能 issue を見つけました。
- 星評価を追加し、転送ブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルター機能の issue を起点に、Plan モードで実装方法を決め、Autopilot モードで作成して、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニット テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルター機能を確認しました。
- 品質保証 (QA) カスタムエージェントを作成して選択し、要件、カバレッジ、スキルの結果、ブラウザーでの根拠を評価しました。
- フィルター機能全体の変更をレビューし、フィルター機能の PR に Agent Merge を許可しました。
- コンテキスト、モデル、共有、cloud agent への任意の委任に使うスラッシュ コマンドを確認しました。

## リリースしたもの

このワークショップでは、更新済みの `main` からそれぞれブランチを作成し、2 つの PR を作成しました。

1. **星評価**: 既存の `starRating` と、評価がない場合の状態をゲーム カードに表示します。
2. **フィルター機能と品質ワークフロー**: フィルター機能を実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

フィルター機能の計画から PR の作成まで、同じ会話とブランチを使いました。ワークショップの手順を簡潔にするため、すべての作業を 1 つの PR にまとめました。

## 異なる方法で検証する

自動テスト、自分でのブラウザー確認、MCP を通じた Copilot のブラウザー確認など、複数の方法でコードを確認しました。`quality-checks` スキルはユニット テスト、lint、型チェックを実行し、追加した形式で結果を報告しました。QA はこれらの結果に要件とテスト カバレッジのレビューを加え、PR を作成する前の確認をまとめました。

追加したテストで実際の不足が解消される必要があります。QA の実行で新たなテストが不要と判断される場合もあります。マージを許可する前に、コードと根拠を確認してください。変更があった場合は、関連する根拠も更新します。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが、作業の内容に影響します。このワークショップでは、指示の更新、スキルのカスタマイズ、QA プロファイルの作成、MCP サーバーの構成を行いました。こうしたカスタマイズを会話間で再利用し、チームのニーズに合わせて調整できます。指示は標準を設定し、スキルは繰り返し実行するタスクを説明し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。**Plan** は実装前に方法を検討するとき、**Interactive** は対象を絞った変更を自分で確認しながら進めるとき、**Autopilot** は範囲が明確なタスクに使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じくらいコンテキストも重要です。何を、なぜ作り、どのように実装するかを明確に伝えることで、生成結果が大きく変わります。

## さらに確認する

主なワークフローを学びました。Copilot CLI の他の機能も確認してみてください。

- `/review` でコード レビュー エージェントに変更を分析してもらいます。
- `/rubber-duck` で問題について話し合い、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` でタスクを Copilot cloud agent に送ります。

## 次の手順

どのツールも、使い続けることで上達します。実際のコード、趣味のコード、長年作ってみたいと思っていた小さなアプリなどで活用してください。チームと学んだことを共有し、お互いの経験から学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys をさらに拡張したい場合は、オプションの [Foundry Backer Concierge シリーズ][foundry]に進みます。他の環境での内容を比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]をご覧ください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
