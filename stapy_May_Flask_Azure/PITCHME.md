# WebAppsに<br>デプロイは難しい
#### みんなのPython勉強会#35 LT (2018/05/10)
#### nikkie

---

# stapy3周年<br>おめでとう<br>ございます！ @fa[birthday-cake]

+++

### 自己紹介 nikkie

- ソフトウェアエンジニア3年目
- @ftnext [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext)
- Python Love @fa[heart fa-pink]
- Azure使うことが多い

---

### LT: WebAppsにデプロイは難しい

## Pythonで作ったWebアプリを<br>WebAppsにデプロイする方法を話します

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

![Flask Logo](http://flask.pocoo.org/docs/0.12/_images/logo-full.png)

---

### HOW TO DEPLOY

チュートリアル、サンプルコードあります
- チュートリアル: [Azure に Python Web アプリを作成する](https://docs.microsoft.com/ja-jp/azure/app-service/app-service-web-get-started-python)
- サンプルコード: [Azure-Samples/python-docs-hello-world](https://github.com/Azure-Samples/python-docs-hello-world)

+++

### ポイント

1. Pythonのバージョン
1. ログ出力
動作サンプル: [ftnext/python-docs-hello-world](https://github.com/ftnext/python-docs-hello-world)

+++

### Pythonのバージョン

- WebAppsはPython3.4系
- バージョンを合わせるのは非常に重要です

+++

ハージョンを合わせなかったことでハマりました

[Python3.6を境にjson.loads()の動きが変わっていたことで1週間ハマりました ToT](https://qiita.com/ftnext/items/e2120cfa0fcecbd599c1)

+++

### ログ出力

- Flaskで設定(`app.logger`)
- WebAppsのログを追ったところ迷宮入りしかけた
  - どこを見ても500エラーとしか出てこない(※個人の体験です)

![500エラー](https://camo.qiitausercontent.com/575b8dfa1f54caf70921635e3aba0ad87d801a67/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f38323133322f39343166326435342d386166622d356238322d393031612d6434383862343466313263372e706e67)

---

### デプロイは壁が高い

### 検証用サーバと本番用サーバ

+++

### `main.py`(MSのサンプルコード)

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
  return 'Hello, World!'

if __name__ == '__main__':
  app.run()
```

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
- WebAppsはPythonのバージョンの設定と<br>ログ出力を知っていれば怖くない(はず)

+++

### ご清聴ありがとうございました

### 質問やコメントなど大歓迎です

[Twitter @ftnext](https://twitter.com/ftnext)
