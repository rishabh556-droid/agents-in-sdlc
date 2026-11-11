---
title: "演習 2 - Copilot エージェント モードで機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリケーションに小さな変更を加える場合でも、複数のファイルを更新し、テストを実行する必要があることがよくあります。開発者は通常、必要なファイルを探し、変更を加え、テストを実行し、問題を調査し、見落としたファイルを見つけて再度更新します。作業は次々と続きます。

こうした場面で Copilot のエージェント モードが役立ちます。

エージェント モードは IDE 内でより自律的に作業します。開発者と同様に、既存のプロジェクト構造を調べ、必要な更新を行い、テストなどのタスクを実行し、見つかった問題を自動的に修正します。エージェント モードを使ってサイトに機能を追加する方法を確認しましょう。

> [!NOTE]
> 名前は似ていますが、エージェント モードと cloud agent は異なる用途向けです。エージェント モードは IDE 内で作業し、すばやいフィードバックと対話を可能にします。cloud agent はチームの一員のように非同期で作業し、issue とプルリクエストを通じてやりとりします。

この演習では、次のことを学びます。

- Copilot エージェント モードがプロジェクトを調べ、関連ファイルを見つけ、複数のファイルを連携して変更する方法
- GitHub Copilot エージェント モードで UI とデータ層にまたがる新機能を実装する方法
- Copilot エージェント モードが生成した変更とテストを、コードベースにマージする前にレビューする方法

## シナリオ

ゲームの一覧が増えてきたため、カテゴリと publisher で絞り込めるようにします。前の演習で publishers ヘルパーを追加しました。残りのデータ層、UI、テストの作業を Copilot エージェント モードで完了します。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の Web サイトを確認し、現在の機能を把握しましょう。

この Web サイトは、開発者をテーマにしたボードゲームのクラウドファンディング プラットフォームです。ゲームの一覧と詳細を表示できます。単一の Astro アプリで、ビルド時にページを静的 HTML として生成します。ページは frontmatter 内で Drizzle ORM を使ってローカル SQLite データベースを直接参照します。独立したバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータ アクセス ヘルパーは `src/lib/` に置き、インタラクティブな機能は標準 DOM API を使う小さな範囲の Astro `<script>` で追加します。

### Web サイトを起動する

Web サイトを実行しやすくするため、単一の Astro 開発サーバーを起動する `npm run dev` タスクが用意されています。GitHub Codespace で次の手順を実行します。

1. Codespace に戻ります。前の演習を終えていれば、`main` に戻っているはずです。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、Codespace 内に新しいターミナルを開きます。
3. フィルター機能の作業用ブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーの準備ができると、次のような URL の表示が出ます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くよう促すダイアログが表示された場合は、**x** を選択して閉じます。

5. ターミナルで <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら Astro サーバーのアドレス `http://localhost:4321` を選択し、Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost URL を選択すると、自動的に `https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは、Web サーバーを実行している Codespace へのプライベート トンネルです。

### Web サイトを確認する

Web サイトを起動したら、機能を確認します。主な機能は次のとおりです。

- **ホーム ページ**: タイトル、画像、説明を含むボードゲームの一覧を表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、そのタイトル、説明、publisher、カテゴリなどの詳細ページが表示されます。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めます。モードとモデルの選択は演習によって異なるため、必要な箇所で説明します。

Web サイトの初期実装は機能しますが、新しい機能を追加しましょう。まずバックログを確認します。テンプレートからプロジェクトをセットアップすると issue のバックログが自動的に作成されます。GitHub Copilot に内容を表示するよう依頼します。

1. Chat ビューのエージェント ドロップダウンから **Agent** を選択します。**Agent** はファイルをまたぐ変更を自律的に計画・実装し、ターミナル コマンドを実行してツールを呼び出します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデルの一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> ワークショップの作成者が特定のモデルを推奨するものではありません。このワークショップの作成時に Claude Sonnet 4.5 を使用したため、比較的一貫した体験になることを期待して手順に記載しています。ただし、LLM は確率的に動作するため、提案内容が手順の例と異なる場合があります。これは通常の想定された動作です。

> [!NOTE]
> LLM の確率的な性質により、Copilot が異なる MCP コマンドを使う場合がありますが、タスクは完了できるはずです。

3. 次のプロンプトを Copilot に送信して、issue のバックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. すべての issue を一覧表示するコマンドを実行するには **Continue** を選択します。
5. 生成された issue の一覧を確認します。

Copilot は、利用者にとって役立つと思われる項目に基づいて優先順位も付けています。

## 指示ファイルを確認する

エージェントにコードを生成させる前に、作業のコンテキストを Copilot に与える指示ファイルを確認しましょう。Web サイトに機能を追加する方法が記載された [UI 指示ファイル](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)を使います。

1. Codespace で `.github/instructions/ui.instructions.md` に移動します。
2. 機能追加に関する全体的な指針を確認します。次の内容が含まれています。
   - アーキテクチャの概要
   - コンポーネントの設計、テスト容易性、アクセシビリティの原則
   - Astro、Tailwind CSS、Drizzle など、ファイルの種類別の指示へのリンク

> [!TIP]
> 指示ファイルから、他の指示ファイルやプロジェクト ファイルを参照できます。パスは指示ファイルからの相対パスです。これにより、指示の再利用、複雑な内容の分割、例やテンプレートの提示ができます。

## フィルタリング機能を実装する

フィルタリングを完成させるには、少なくとも次の 3 つの更新が必要です。

- データ層 (`src/lib/`) に残りのフィルタリング ロジックを追加または調整する
- フィルタリング動作のテストを追加または更新する
- ゲーム一覧ページを更新してフィルター UI を追加する

コードベースにマージする前に、テストを実行して成功させる必要もあります。Copilot エージェント モードに依頼して機能を追加しましょう。

1. Copilot との現在の会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択し、指示ファイルを指定します。

   ![UI 指示ファイルを選択する例](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント ドロップダウンで、引き続き **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. モデルとして引き続き **Claude Sonnet 4.5** が選択されていることを確認します。
5. バックログにある関連 issue の要件に基づいて機能を実装するよう、次のプロンプトを Copilot に送信します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べ、機能に関連するファイルを探す様子を確認します。データ層のヘルパー、UI、テストを見つけた後、ファイルを変更してテストを実行します。

   ![Copilot がプロジェクト ファイルを調べている様子](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、変更、テストの実行などを行うため、タスクの複雑さやコードベースの規模によっては数分かかります。作業中にエディターに **Keep** と **Undo** が表示されることがあります。Copilot が完了するとすべての変更に対して選択できるので、作業中に選択する必要はありません。

7. Copilot に促されたら **Continue** を選択し、テストを実行します。

   ![Copilot Chat ペインに表示されたテスト実行の確認ダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりすることがあります。問題ありません。Copilot はタスクが完了し、エラーが見つからなくなるまで、コード生成とテストを繰り返します。

   ![Copilot エージェント モードのチャット セッションが完了した画面](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot などの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを表示しているブラウザーに戻り、新機能を試します。
11. 動作を確認し、コードをレビューしたら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次の手順

この演習では、GitHub Copilot エージェント モードを使って Tailspin Toys の Web サイトに機能を追加しました。次のことを学びました。

- GitHub Copilot エージェント モードで UI とデータ層にまたがる新機能を実装する方法
- Copilot エージェント モードがプロジェクトを調べ、関連ファイルを見つけ、複数のファイルを連携して変更する方法
- Copilot エージェント モードが生成した変更とテストを、コードベースにマージする前にレビューする方法

次は [Playwright MCP サーバーで機能をテスト][next-lesson]し、プルリクエストを作成します。

### 発展演習 — ページ分割を実装する

ゲーム一覧が増えてくると、ページ分割が必要になります。この演習で学んだ内容を使い、Copilot にページ分割を実装するよう依頼してみましょう。次の点を検討してください。

- 既存の指示ファイルを使うなど、現在のベスト プラクティスに従います。
- 利用者がページ サイズを選べるようにするか、値を固定するかなど、ページ分割の方法を検討します。
- 希望する実装に必要なガイダンスを、プロンプトで Copilot に提供します。
- 必要に応じて Copilot に変更を依頼し、コンテキストを追加します。これは Copilot を使う通常のワークフローです。

## リソース

- [Copilot の ask、edit、agent モード: 機能と使い分け][choose-mode]
- [VS Code のエージェント モード][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
