# WebAppsにデプロイは難しい
#### みんなのPython勉強会#35 LT (2018/05/10)
#### nikkie

---

# stapy3周年<br>おめでとう<br>ございます！ @fa[birthday-cake]

+++

### 自己紹介 nikkie

- ソフトウェアエンジニア3年目
- TwitterやQiita: @ftnext
- Python Love @fa[birthday-cake fa-pink]
- Azure使うことが多い

---

### WebAppsにデプロイは難しい

### Pythonで作ったWebアプリをWebAppsにデプロイする方法を話します

+++

### WebAppsとは

- AzureのPaaS
  - Azure: マイクロソフトのクラウド
  - PaaS: ソースコードさえあれば、Webアプリを配信できるツール
- 無料でも使える

+++

### 今回のWebアプリ

- Flaskを利用
  - Djangoと比べてシンプル。簡単なWebアプリ(API)をぱっと作るのに向いている
- もちろんDjangoもWebAppsでデプロイできる

---

### HOW TO DEPLOY

チュートリアル、サンプルコードあります

+++

### ポイント

1. Pythonのバージョン
1. ログ出力

+++

### Pythonのバージョン

- WebAppsはPython3.4系
- バージョンを合わせるのは非常に重要です

+++

ハージョンを合わせなかったことでハマりました

TODO: iframeを使う

+++

### ログ出力

- Flaskで設定(`app.logger`)
- WebAppsのログを追ったところ迷宮入りしかけた
  - どこを見ても500エラーとしか出てこない(※個人の体験です)

---

### デプロイは奥が深い

### 検証用サーバと本番用サーバ

+++

### 検証用サーバ

- `python main.py`で動くサーバ (http://127.0.0.1/)
- デプロイするものではない

+++

### 本番用サーバ

- 以下を組合せて成立
  - Webサーバ(Apache, nginx)
  - 接続インターフェース(WSGI)
  - Webアプリ(Flask, Django)
- 引き続き勉強します

---

### まとめ

- ソースコードさえあればWebAppsで公開できる
- WebAppsはPythonのバージョンの設定とログ出力を知っていれば怖くない(はず)

+++

### ご清聴ありがとうございました

### 質問やコメントなど大歓迎です
