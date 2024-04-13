# Auto PR Closer

このGitHub Actionは、指定された日数以上アクティブでないプルリクエストを自動でクローズします。チームがクリーンで最新の状態を保つのに役立ちます。

## 機能

- **自動クローズ**: 指定された期間アクティブでないプルリクエストを自動的にクローズします。
- **ブランチ削除**: クローズ時に関連するブランチも自動的に削除します。

## 入力

| 名前  | 説明                                           | 必須 |
| ------ | -------------------------------------------- | :--: |
| `token` | GitHub Token。このActionの実行に必要です。        | はい |
| `days`  | クローズするプルリクエストのアクティブでない日数 | はい |

## 出力

| 名前    | 説明                               |
| ------- | ---------------------------------- |
| `pr_ids` | クローズされたプルリクエストのIDのリスト |

## 使い方

1. このActionをGitHubリポジトリの`.github/workflows`ディレクトリに配置します。
2. 必要に応じて`days`と`token`の値を設定します。

### Workflowファイルの例

```yml
name: Close Stale Pull Requests
on:
  schedule:
    - cron: '0 0 * * *'  # 毎日UTC0時に実行

jobs:
  close_stale_prs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Close Stale Pull Requests
        uses: actions/auto-pr-closer@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          days: 30
