# Memen プラグイン

[English](README.md)

Claude Code と Codex から [memen](https://memen.app) を使うためのプラグインです。AIに自分の1日を聞けるようになり、AIと進めた作業も memen の記録に残せます。

## できること

ふだんの言葉で頼めます。

- 「memen で今日の記録を見せて」
- 「昨日の午後なにしてたか memen で調べて」
- 「memen に『見積もりを送る』というTODOを足して」
- 「いまやった作業を memen に記録して」

## 始める前に

Web版の memen にログインできるアカウントが必要です。いまは Google でログインしている人がつなげます。iPhone で Apple のアカウントだけで登録した人は、まだつなげません。

## 入れ方

### Claude Code

1. Claude Code の中で次を実行します。

   ```text
   /plugin install memen --marketplace kkaiki/memen-plugins
   ```

2. `/mcp` を開き、memen を選んで「Authenticate」を押します。
3. ブラウザで memen にログインし、「許可する」を押します。

### Codex

1. ターミナルで次を実行します。

   ```bash
   codex plugin marketplace add kkaiki/memen-plugins
   codex plugin add memen@memen
   codex mcp login memen
   ```

2. ブラウザで memen にログインし、「許可する」を押します。

許可したあと、ブラウザは `localhost` のページに戻ります。手元の Claude Code・Codex が結果を受け取るための動きで、問題ありません。

## AIにできること・できないこと

| できる | できない |
| --- | --- |
| 1日・1週間の記録を読む(TODO、メモ、予定、時間の使い方の要約) | 文字起こしの原文を読む |
| 作業をタイムラインに記録する | 記録やメモを消す |
| TODO と予定を足す・動かす | スクリーンタイム・サイトブロックの制限を変える |
| TODO と予定を消す(確認のうえ1件ずつ) | |

## データの扱い

AIが読んだ記録は、つないだAIの事業者(Claude なら Anthropic、Codex なら OpenAI)に送られ、その事業者の扱いに従います。memen が返す本文からは、APIキーなどの秘密情報を消しています。プラグインはキーを持たず、ログインは OAuth だけで行います。

詳しくは [AIとつなぐ](https://memen.app/ai) と[プライバシーポリシー](https://memen.app/privacy)をご覧ください。

## やめるとき

memen にログインし、メニューの「つないだAI」から解除します。解除すると、そのAIはすぐに memen を読み書きできなくなります。
