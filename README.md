## Githubにapp-htmlリポジトリ作成
```
text
image
xxx-app　←アプリ／サイトのソースコードを入れるディレクトリ
  index.php　←xxx-appディレクトリに追加
  composer.json　←xxx-appディレクトリに追加
```
## HerokuでAPI_KEYを取得
https://dashboard.heroku.com/account

## Githubのapp-htmlリポジトリ設定でAPI_KEYをSecretsに登録
https://github.com/minopon/app-html/settings/secrets/actions

## GIthubActions設定
app-html/.github/workflows/main.yml
```
name: Heroku deployment

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1

      - name: Add heroku remote origin
        run: |
          git remote add heroku https://heroku:${{ secrets.HEROKU_API_KEY }}@git.heroku.com/app-html-1.git
      - name: Deploy app to Heroku
        run: |
          git subtree push --prefix xxx-app heroku main
```

## herokuで空のapp-html-1アプリを作る

## Github にプッシュ
```
git push origin main
```
