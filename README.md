# n8n Google Calendar to Slack Workflow

Google カレンダーの予定を指定期間で取得し、Slack に通知する n8n ワークフローです。

## 機能

- Webフォームで期間を指定可能
- 指定した期間のGoogle カレンダーの予定を取得
- 日付別にグループ化して整形
- Slackチャンネルに通知

## セットアップ

### 前提条件

- n8n がインストールされていること
- Google Calendar API の認証情報
- Slack OAuth2 の認証情報

### インストール手順

1. このリポジトリをクローン
```bash
git clone https://github.com/osasasasa/n8n-google-calendar-slack-workflow.git
```

2. n8n でワークフローをインポート
   - n8n の管理画面を開く
   - 「Import from File」を選択
   - `workflows/google-calendar-to-slack.json` を選択

3. 認証情報の設定
   - Google Calendar ノードで認証情報を設定
   - Slack ノードで認証情報を設定

4. ワークフローをアクティベート

## 使い方

### テストモード
1. Form Trigger ノードの「Test Step」をクリック
2. フォームが開くので、開始日と終了日を入力
3. 通知先の Slack チャンネルを指定（デフォルト: #general）
4. 送信ボタンをクリック

### 本番運用
1. ワークフローをアクティベート
2. Production URL を使用してフォームにアクセス
3. 期間を指定して送信

## ワークフローの構成

1. **期間指定フォーム** - 期間とSlackチャンネルを入力するWebフォーム
2. **Google Calendar** - 指定期間の予定を取得
3. **予定整形** - 取得した予定を見やすく整形
4. **Slack通知** - 整形された予定をSlackに送信

## カスタマイズ

### 日付フォーマット
`予定整形`ノードの JavaScript コードで日付表示形式を変更できます。

### 取得する予定の数
Google Calendar ノードの `Limit` パラメータで変更可能（デフォルト: 100）

### タイムゾーン
日本時間（JST, +09:00）に設定されています。他のタイムゾーンに変更する場合は、各ノードの時刻設定を修正してください。

## トラブルシューティング

### "Bad request" エラーが発生する場合
- Google Calendar ノードの After/Before フィールドが Expression モードになっているか確認
- 日付フォーマットが正しいか確認（YYYY-MM-DD形式）

### 予定が取得できない場合
- Google Calendar の認証情報が正しく設定されているか確認
- カレンダーIDが正しいか確認（デフォルト: primary）

## 貢献

Issue や Pull Request は歓迎します。