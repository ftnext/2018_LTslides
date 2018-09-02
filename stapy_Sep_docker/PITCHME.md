# Entrance of Docker for Pythonista
## 〜DockerではじめるPython環境構築（←要調整）〜
#### みんなのPython勉強会#38 (2018/09/12) nikkie

---

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- Software Engineer?
- Love Python@color[#eba3ff](@fa[heart]), Love Docker@color[#eba3ff](@fa[heart]@fa[heart])

+++

### Joined Translation

- Django Girls Tutorial 翻訳に関わりました。
	- https://tutorial.djangogirls.org/ja/

---

### About this talk

- 一推しのDockerをPythonistaに知ってほしい！使ってほしい！
- 題材: 機械学習のモデルをAPIとして公開
	- Dockerを使ってAPIとして公開します

+++

### 注意事項

- Dockerについてはざっくり理解を優先した説明です(学習リソース示す)

+++

### 登場人物

- Irisデータセット
- Flask
- Docker

+++

### Irisデータセット

- みんな大好き、あやめのデータ
  - がくの幅・長さ、花びらの幅・長さ[単位:cm]、品種
- scikit-learnを使ってあやめの品種の分類器を作る
- 分類器をAPIにしたい(Webアプリとして公開したい)

+++

### Flask

> ウェブフレームワークの1つ（『独学プログラマー』p.218）

- 「シンプルなウェブアプリケーションをシンプルに作るときに使う」
  - 機械学習のモデルのAPI化に向く

+++

### 目次

- TODO: 各スライドがFIXしたらアップデートする
- Dockerとは？
- 分類器作成 & API化
- コンテナ化 & クラウドにデプロイ

+++

### Dockerとは？

- アプリケーションを動作する状態で持ち運ぶための技術
- 「コンテナ型仮想化」

+++

### アプリケーションを持ち運ぶ

- アプリケーションには環境の設定がある(OS、環境変数)
- 開発環境と本番環境の差分を吸収
	- Dockerコンテナで開発を進める
	- デプロイする際は、Dockerで移動させる

+++

### コンテナまわりの用語集

- Dockerイメージ: コンテナのもと
	- 実行(`docker run`)してコンテナが動作する
- Dockerfile: イメージの設計書(テキストファイル)
	- ビルド(`docker build`)してイメージができる

+++

Dockerコンテナは仮想マシンとして振る舞うように見える
`docker run`する際はホストの間に接点を設定する

+++

### Dockerのメリット

1. デプロイの省力化
    - Flaskアプリケーションをデプロイして説明します
1. 環境構築の省力化
    - Appendix: 機械学習環境の構築

+++

### 仮想化に関連する用語

- ホスト／ゲスト
- Dockerイメージ
- Dockerコンテナ

---

### あやめの分類器作成

- あやめの花びらの長さと幅から品種を分類する
	- 長さ 5.1cm, 幅 2.4cm -> 品種はvirginica
- [Python機械学習プログラミング 3章](https://github.com/rasbt/python-machine-learning-book/blob/master/code/ch03/ch03.ipynb)に基づく
- 注: 今回、分類器の性能にはこだわっていません

+++

### データセット分割、標準化

```python
iris = datasets.load_iris()
# Petal(花びら)のlengthとwidthから品種を分類する
X = iris.data[:, [2, 3]]
y = iris.target
X_train, X_test, y_train, y_test = train_test_split(
		X, y, test_size=0.3, random_state=0)
sc = StandardScaler()
sc.fit(X_train)
X_train_std = sc.transform(X_train)
X_test_std = sc.transform(X_test)
```

+++

### パーセプトロンの学習、性能確認

```python
ppn = Perceptron(max_iter=40, eta0=0.1, random_state=0, shuffle=True)
ppn.fit(X_train_std, y_train)
y_pred = ppn.predict(X_test_std)
accuracy_score(y_test, y_pred)
```

- 分類の正解率: 91.1%

+++

### `joblib`で掃き出す

- Webアプリケーションでloadするため
- 分類器: `joblib.dump(ppn, 'ppn_iris.pkl')`
- 標準化のScaler: `joblib.dump(sc, 'sc_iris_petal.pkl')`

+++

### APIがやること

1. 花びらの長さと幅のJSONがPOSTされる
		- `{ "length": 5.1, "width": 2.4 }`
1. 分類器に渡す前に標準化する
1. 分類器で分類する
1. 分類結果をJSONで返す
		- `{ "prediction": "virginica" }`

+++

### ファイル類の配置

- app
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

+++

### Webアプリ側で読み込む (app.py)

```python
sc = joblib.load('sc_iris_petal.pkl')
ppn = joblib.load('ppn_iris.pkl')
```

+++

### ソースコードに起こす (app.py)

```python
@app.route('/predict', methods=['POST'])
def predict():
    input_ = request.get_json()
    length = float(input_['length'])
    width = float(input_['width'])
    input_std = sc.transform(np.array([[length, width]]))
    prediction = ppn.predict(input_std)
    response = jsonify(
        {'prediction': IRIS_KIND[int(prediction[0])]})
    response.status_code = 200
    return response
```

+++

### 動作の様子

画像を入れる

---

### コンテナ化

分類器のAPIを持ち運べるようにする

1. Dockerfileを作る
1. Dockerfileからイメージを作る
1. イメージからコンテナを作る

TODO: 用語の説明を入れること

+++

### イメージの概要

- FlaskのAPIのソースコードを配置
- APIを実行する
	- 本番サーバとして実行
	- `python app.py`のように実行する開発サーバはAPIとして公開する際は使うべきではない

+++

### Dockerfile

```Dockerfile
FROM python:3.6
RUN apt update && apt install python-dev -y
COPY . /home
RUN cd /home && pip install -r requirements.txt
EXPOSE 5000
WORKDIR /home/app
ENTRYPOINT ["gunicorn", "-b", "0.0.0.0:5000", "--access-logfile", "-", "--error-logfile", "-"]
CMD ["app:app"]
```

参考: [chhantyal/flask-docker](https://github.com/chhantyal/flask-docker/blob/68c0e439c50b12989fb87548e32ca1b1dfeb11e8/Dockerfile)

+++

### ファイル類の配置

- Dockerfile <- NEW!
- requirements.txt <- NEW!
- app
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

+++

### build image

- `docker build -t <イメージ名:バージョン> .`
- Dockerfileをベースにイメージを作成する

+++

### イメージを実行する

- `docker run -p 5000:5000 <イメージ名:バージョン>`

+++

### 動作の様子

画像を入れる

+++

### クラウドにデプロイ


---
