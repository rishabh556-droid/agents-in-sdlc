---
title: "レッスン 2 - 星評価を追加する: 手早い改善"
description: "GitHub Copilot app で最初のエージェント セッションを開始し、ゲーム カードに小さな変更を加えて、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

ワークスペースを確認し、クイックチャットを試しました。次は**エージェント セッション**を開始して、プロジェクトに初めての変更を加えます。変更は小さくします。ゲームのデータにはすでに星評価がありますが、ホーム ページのゲーム カードには表示されていません。エージェントに評価を表示させ、変更をレビューし、最初のプルリクエストとしてマージします。

このレッスンでは、次のことを行います。

- エージェント セッションを開始し、セッションの構成を学びます。
- エージェントに小さく対象を絞った変更を依頼します。
- ワークスペースの差分ビューで変更をレビューします。
- アプリをローカルで実行し、ブラウザーで変更を確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。しかし、ホーム ページのゲーム カードには、タイトル、カテゴリ、publisher、説明しか表示されていません。最初のセッションの練習として、各カードに既存の評価を表示するようエージェントに依頼します。小規模で自己完結した、最初のセッションに適した変更です。

## セッションの構成

**セッション**は、独立したワークスペースで実行されるエージェントとの会話です。各セッションには**専用の git worktree とブランチ**が割り当てられます。そのため、一方で機能を追加し、もう一方でバグを修正するなど、変更を競合させずに複数のセッションを同時に実行できます。セッションはリポジトリごとにサイドバーにまとめて表示されます。いずれかを選ぶと切り替えられます。

セッション内には、エージェントとの**会話**、ファイルを調査・編集するときのエージェントの**ツール アクティビティ**、差分付きの**変更ファイル**一覧が表示されます。

## セッションを開始して変更を依頼する

新しいセッションを開始し、プロジェクトの調査と機能の実装に取りかかります。[アプリのセットアップ][prior-lesson]で GitHub リポジトリからプロジェクトを追加しました。そのリポジトリの新しいセッションを作成して、変更を依頼します。

1. GitHub Copilot app に戻ります (またはアプリを開きます)。
2. サイドバーの上部にある **+** を選択してセッションを開始します。
3. リポジトリとして `tailspin-toys` を選択します。
4. プロンプト ボックスの下で **new working tree** と **Interactive** モードを選び、次のプロンプトを送信します。

    ```plaintext
    Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
    ```

5. <kbd>Enter</kbd> を押して、プロンプトを Copilot に送信します。

Copilot app は、最初にプロジェクトの分離されたコピーである新しい worktree を作成して作業を開始します。次にプロジェクトを調査し、新機能の追加に必要な更新対象ファイルを見つけ、必要なコードを作成します。Copilot app を使って新機能を追加できました。

## 差分をレビューする

AI が生成した変更は、小さなものでもマージ前に必ずレビューします。Copilot app 内で変更を確認しましょう。

1. アプリの右上にある **Toggle review panel** を選択します。開いたパネルで **Changes** を選択し、変更されたファイルと差分を確認します。

    ![Create PR ボタンの右にある Toggle review panel ボタンを矢印で示した GitHub Copilot app の上部ツールバー](../../../_images/app-2-review-panel.png)

2. ゲーム詳細の表示に使われる中心的なファイル `GameCard.astro` にコードが追加されているはずです。次のような小さなブロックで、評価がある場合は表示し、`starRating` が `null` の場合は "No rating yet" に置き換えます。

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot はすべての生成 AI ツールと同様に確率的に動作するため、コードは上記と異なる場合があります。大まかな構造は似ているはずです。

## 変更を確認する

ブラウザーを開く前に、エージェントが実行した自動チェックの結果をレビューします。数値の `starRating` と、`null` の場合の代替表示の両方をテストしていることを確認します。前提条件が不足していたり、チェックがスキップされたりしている場合は成功ではありません。インストールの要求は内容を確認してから承認します。

コードを読むだけで動くと判断せず、Copilot に Web サイトを開いてもらい、更新された UI を確認しましょう。Copilot に Web サイトを起動させ、ブラウザー キャンバスで開きます。

> [!TIP]
> キャンバスは、Copilot app 内で使えるインタラクティブなウィジェットです。後のレッスンではカスタム キャンバスを確認し、自分でも作成しますが、ここでは組み込みのブラウザー キャンバスを使います。

1. 次のプロンプトを使い、アプリを起動してブラウザー キャンバスでページを開くよう Copilot に依頼します。

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. しばらくするとアプリが起動し、Copilot app 内にブラウザー ウィンドウが開きます。
3. 評価済みのゲーム カードに 5 点満点の評価が表示されることを確認します。
4. 確認が終わったら、次のプロンプトでこのセッションが起動した開発サーバーを停止するよう Copilot に依頼します。

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## 最初のプルリクエストを作成してマージする

機能を作成できました。次に、コードベースに新しいコードをマージするプルリクエスト (PR) を作成します。

1. 右上にある **Create PR** を選択します。
2. プロンプトが表示された場合は **Sign in with your browser** を選び、手順に従って認証します。
3. PR を作成する前に対応する issue が必要だと Copilot から案内された場合は、そのプロセスに従うよう確認します。
4. Copilot が PR を作成します。
5. チャットのすぐ上にある **PR** バブルを選択し、レビューペインで PR を開きます。ここで必要に応じて内容をレビューできます。
6. 問題がなければ **Ready to merge** を選択します。
7. 新しいダイアログで **Merge pull request** を選び、PR をマージします。

## まとめと次の手順

GitHub Copilot app を使って、最初の変更をリリースしました。具体的には、次のことを行いました。

- エージェント セッションを開始し、セッションの構成を学びました。
- ゲーム カードに小さく対象を絞った変更を依頼しました。
- ワークスペースの差分ビューで変更をレビューしました。
- アプリをローカルで実行し、ブラウザーで星評価を確認しました。
- PR 1 を作成し、チェックをレビューして、明示的にマージしました。

次は[フィルター機能の issue を起点に、Plan と Autopilot モードを使って][next-lesson]、より大きな機能を構築します。

## リソース

- [GitHub Copilot app でのエージェント セッションの操作][agent-sessions]
- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app で issue とプルリクエストを管理する][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#github-copilot-app-をインストールして構成する
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
