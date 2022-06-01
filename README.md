## Githubにapp-htmlリポジトリの構成
以下のディレクトリ、ソース構成が前提
```
text
image
xxx-app　←アプリ／サイトのソースコードを入れるディレクトリ
  index.php　←xxx-appディレクトリに追加
  composer.json　←xxx-appディレクトリに追加
```

## app-htmlリポジトリをクローンする
```
git clone git@github.com:minopon/app-html.git
```

## Heroku CLI でapp-html-1アプリを作る
```
heroku create --app app-html-1
```

## HerokuでAPI_KEYを取得
https://dashboard.heroku.com/account

## Githubのapp-htmlリポジトリ設定でAPI_KEY内容を `HEROKU_API_KEY`という名前で登録
https://github.com/minopon/app-html/settings/secrets/actions

## GIthubActions設定
https://github.com/minopon/app-html/actions/new
の`set up a workflow yourself`リンクから以下を設定。
以下設定して保存すると、そのまま実行されてHerokuにデプロイされる。

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

## 以降はGithubにプッシュするとHerokuに自動デプロイされる
```
git add .
git commit -m fix
git push origin main
```
