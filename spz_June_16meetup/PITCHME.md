# TODO: タイトルを決める
#### 16卒エンジニア限定ミートアップ LT (2018/06/22)
#### nikkie

---

### Too Long; Didn't Listen

>テーマは「この一ヶ月で知ったこと／感じたこと」

[2018/06/22 16卒エンジニア限定ミートアップ](https://supporterzcolab.com/event/402/)

+++

### Too Long; Didn't Listen

- flaskについて学んだことを話します
- flaskとはPythonのWebフレームワーク

+++

### About nikkie (@ftnext)

- Software Engineer (3rd year)
  - Python: half year
  - 2018/12~ 趣味で始めた
  - 2018/04~ FlaskでAPI開発

+++

### こんなもの作りました

https://speakerdeck.com/ftnext/pillow-mosaic-art-nyumon

![mosaic art](https://pbs.twimg.com/media/DY0mx1kVwAE4k9J.jpg)

+++

### この一ヶ月でできるようになりました

- line-bot-sdk on Azure (WebApps)

![line-bot-sdk on Azure](https://pbs.twimg.com/media/Df0pjeKUcAAvNIP.jpg)

---

### What's flask

![flask logo](http://flask.pocoo.org/docs/1.0/_images/logo-full.png)

+++?image=https://img.supporterzcolab.com/thumbs/93/6e/936e380d5aeb12a08a1a91058cb9aac7.png&size=contain

+++

### What's flask

- シンプルでとっつきやすいWebフレームワーク

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
  return 'Hello, World!'

if __name__ == '__main__':
  app.run()
```

---

### 知ったこと1: ログの出し方

- `app.logger` (`app = Flask(__name__)`)
- 実態は標準モジュール`logging`

+++

### logging

- ログ書き込み先やログのフォーマットの指定が必要
  - 使い出しの設定が必要で`print`から切り替えるのに戸惑った
- 公式チュートリアル: [Logging HOWTO](https://docs.python.jp/3/howto/logging.html)

---

### 知ったこと2: DBの扱い(importを散らす)

[The Flask Mega-Tutorial Part IV: Database](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-iv-database)より

```python
from flask import Flask
from config import Config
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config.from_object(Config)
db = SQLAlchemy(app)

from app import models
```

+++

- importはファイルの先頭にまとめるという思い込みがあった
- `app`と`db`を作ってから`from app import routes, models`がポイント
- `app/models.py`の中で`db`を`import`する

+++

### 以下では、循環importが発生

```python
from flask import Flask
from config import Config
from flask_sqlalchemy import SQLAlchemy
from app import models

app = Flask(__name__)
app.config.from_object(Config)
db = SQLAlchemy(app)
```

---

### まとめ

- ログの使い方は[Logging HOWTO](https://docs.python.jp/3/howto/logging.html)で押さえる
- DBを扱うときはimportを散らす

+++

### 今後

- WebApps(Windows OS)へのデプロイにロックインを感じる
- Dockerを試してみたい

+++

### ご清聴ありがとうございました

Contact: [Twitter @ftnext](https://twitter.com/ftnext)
