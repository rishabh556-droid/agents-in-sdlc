---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

技術的負債に悩んでいない組織は、ほとんどありません。未解決のセキュリティ問題、更新が必要なレガシ コード、実装する時間がなくバックログに残った機能要求などがあります。GitHub Copilot cloud agent は、コードの更新や機能の追加といったタスクを自律的に実行します。作業が終わると、人間の開発者がレビューできるドラフト PR を作成します。時間のかかる作業を任せることで、開発者はより大きな課題に集中し、開発を加速できます。

Copilot cloud agent で次のことを学びます。

- コードを生成する環境のカスタマイズ
- 操作を安全に行う方法
- 明確な範囲の issue が重要な理由
- issue を Copilot に割り当てる方法

## シナリオ

Tailspin Toys には解消したい技術的負債があります。最初の Web サイトを作成した委託先がドキュメントを適切に整備しておらず、実際にはドキュメントがまったくありません。まず、アプリケーションのエクスポートされたすべての関数に TSDoc のドキュメント コメントを追加します。

また、デザイン チームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに、同じカテゴリに属する他のゲームを表示し、利用者が引き続きゲームを見つけられるようにします。現時点では完成度の高い実装ではなく、UX の受け入れテストに使えるものを求めています。この作業は現在ブロックされていますが、優先度がより高い issue が他にもあります。

こうしたタスクは優先順位が下がりやすく、Copilot cloud agent に任せるのに適しています。Copilot cloud agent は非同期に作業するため、開発者は他のタスクに集中し、後から結果をレビューして期待どおりか確認できます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同じようにバックグラウンドでタスクを実行できます。たとえば、[GitHub issue を Copilot に割り当て][assign-issue]ます。割り当てられると、Copilot は進捗を追跡するドラフト プルリクエストを作成し、環境を準備してタスクに取り組みます。作業中でも完了後でもセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 適切な範囲を設定することの重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単そうな作業でも、詳しく調べると複雑さが見えてきます。[Copilot cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を慎重に決めてください。AI ペア プログラマーとして扱い、段階を踏んで学び、試し、調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習ではカスタム指示とその役割を紹介しました。カスタム指示の演習をすでに完了していれば、`.github/copilot-instructions.md` が機能することを確認しています。まだの場合は、ここで簡単に確認しましょう。Copilot cloud agent に作業を割り当てる前に、このリポジトリにある指示ファイルを読み取り専用で確認して、後でその影響を調べられるようにします。

リポジトリの GitHub Web UI または起動済みの Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクションを確認します。特に TypeScript の規約と TSDoc ドキュメント コメントに関する要件を見てください。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` フロントマターが `**/*.test.ts` ファイルに指示を適用することを確認します。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てたら、指示ファイルに由来する TSDoc ドキュメント コメント、TypeScript の規約、コメント ヘッダーを確認します。後の演習で PR をレビューするときにも取り上げます。

## Copilot cloud agent の開発環境をセットアップする

人間がコードを作成する場合と同様に、Copilot にタスクを割り当てるときも、必要なツールや依存関係を整える特定の環境やセットアップ スクリプトが必要です。

cloud agent は作業環境として [GitHub Actions][github-actions] を使います。`.github/workflows/copilot-setup-steps.yml` に設定する[セットアップ ワークフロー][setup-workflow]を作成して、作業前に実行するツールや依存関係を指定できます。このラボでは学習に集中できるよう、あらかじめ設定されています。単一の Astro アプリで、Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー バイナリ、マイグレーションとシードが済んだ SQLite データベースを利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 各手順に必要な最小限の権限を設定します。Copilot の操作には独自のトークンが使われます。
    permissions:
      # 依存関係のインストールなど、セットアップ手順の一部としてリポジトリをクローンする場合は contents: read が必要です。クローンしない場合は、手順の完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ローカルの SQLite データベースをマイグレーションしてシードし、ビルドとテストでデータを利用できるようにします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub Actions ワークフローと同じですが、次の点を確認してください。

- `copilot-setup-steps` という単一のジョブがあります。Copilot がプルリクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブから手動でワークフローを実行できます。Copilot の実行を待たずに、正常に動くかテストできます。

## ドキュメントを追加する

誰もがドキュメントの重要性を理解していても、多くのプロジェクトでは情報が古いか、ドキュメントそのものが不足しています。こうした技術的負債は放置されがちで、生産性を低下させ、コードベースの保守や新しいメンバーの参加を難しくします。Copilot はドキュメントの作成を得意としているため、cloud agent に任せるのに適した issue です。バックグラウンドでドキュメントを作成してもらい、後の演習で結果を確認します。

1. 新しいブラウザー タブで github.com のリポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して issue を作成します。
8. 右側で **Assign to Copilot** を選択します。
9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエストを開きます。タイトルは `[WIP]: Code lacks documentation` のようになります。一覧にない場合は、少し待ってからブラウザーを更新してください。
12. 数分後、Copilot が todo リストを作成したことを確認します。

> [!NOTE]
> Copilot の todo リストが PR に表示されるまで数分かかる場合があります。前述のワークフローを実行して環境を作成し、プロジェクトを分析して、問題への最適な取り組み方を検討しています。

13. リストと、Copilot が実行する予定のタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot が issue に取り組み始めたことを示す更新を確認します。
15. **View session** ボタンを選択します。

    ![Copilot のセッション ビュー](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された表示を確認するため、ウィンドウの再読み込みが必要な場合があります。

16. ライブ セッションをスクロールして、Copilot が問題を解決する様子を確認します。コードを調べて状態を理解し、計画を考えて適切な方法を選び、コードを作成する過程が表示されます。

作業には数分かかる場合があります。Copilot cloud agent の主な目的の 1 つは、非同期に作業して他のタスクに集中できるようにすることです。この機能を活用して、もう 1 つのタスクを cloud agent に割り当ててから、アプリケーションに機能を追加する作業を進めます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

GitHub Copilot cloud agent の利点の 1 つは、作業を分担できることです。デザイン チームのために関連ゲームのセクションを追加する作業に時間がかからなくても、その時間を他のタスクに使えます。Copilot cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して issue を作成します。
8. 右側で **Assign to Copilot** を選択します。
9. **Assign** を選択します。

まもなく、Copilot が作業を始めたことを示す 👀 が issue の最初のコメントに表示されます。

![Copilot が issue に取り組んでいることを目の絵文字で示す様子](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組んでいます。Copilot cloud agent はソフトウェア エンジニアのように作業するため、常に監視する必要はありません。完了後にレビューできます。次はカスタムエージェントの作成と使用を確認します。

## まとめと次の手順

このレッスンでは [GitHub Copilot cloud agent][copilot-agents] を学びました。cloud agent に issue を割り当てると、非同期に作業してもらえます。技術的負債の解消、新しい機能の作成、別のフレームワークへのコード移行などに活用できます。

次のことを確認しました。

- コードを生成する環境のカスタマイズ
- 操作を安全に行う方法
- 明確な範囲の issue が重要な理由
- issue を Copilot に割り当てる方法

cloud agent がバックグラウンドで作業している間に、カスタムエージェントの作成と使用に進みます。[Copilot cloud agent は MCP サーバー][cloud-agent-mcp]も使用でき、前のモジュールで確認したカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローに関するベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
