# Entrance of Docker for Pythonista
## 〜DockerではじめるPython環境構築（←要調整）〜
#### みんなのPython勉強会#38 (2018/09/12) nikkie

---

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext)
- Software Engineer?
- Love Python@color[#eba3ff](@fa[heart]), Love Docker@color[#eba3ff](@fa[heart]@fa[heart])

+++

### Joined Translation

- Django Girls Tutorial 翻訳に関わりました。
	- https://tutorial.djangogirls.org/ja/

---

### About this talk

- 一推しのDockerをPythonistaに知ってほしい！使ってほしい！
- Dockerを使い、機械学習のモデルをAPIとして公開します

+++

### 登場人物

- scikit-learn Irisデータセット
- Flask
- Docker

+++

### Irisデータセット

- みんな大好き、あやめのデータ
  - がくの幅・長さ、花びらの幅・長さ[単位:cm]、品種
- あやめの品質の分類器を作り、APIにする(Webアプリとして公開する)

+++

### Flask

> ウェブフレームワークの1つ（『独学プログラマー』p.218）

- 「シンプルなウェブアプリケーションをシンプルに作るときに使う」
  - 機械学習のモデルのAPI化に向く

+++

### 目次

- Dockerとは？
- 分類器作成 & API化
- コンテナ化 & クラウドにデプロイ

+++

### Dockerとは？

- 仮想化技術の1つ
- Dockerを使うと、アプリケーションを動作する状態で持ち運べる
- 注: ざっくり理解を優先した説明です

+++

### アプリケーションを持ち運ぶ

- 環境の設定がある。Dockerはそれを持ち運ぶ

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

### 分類器作成

- [Python機械学習プログラミング 3章](https://github.com/rasbt/python-machine-learning-book/blob/master/code/ch03/ch03.ipynb)に基づく
  - `Perceptron(max_iter=40, eta0=0.1, random_state=0, shuffle=True)`
- 注: 今回、モデルの性能にはこだわっていません

+++

### あやめの分類器

```python
iris = datasets.load_iris()
# Petal(花びら)のlengthとwidthから品種を分類する
X = iris.data[:, [2, 3]]
y = iris.target
```

+++

### データセット分割、標準化

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=0)
sc = StandardScaler()
X_train_std = sc.transform(X_train)
X_test_std = sc.transform(X_test)
```

+++

### パーセプトロンを学習させる

```python
ppn = Perceptron(max_iter=40, eta0=0.1, random_state=0, shuffle=True)
ppn.fit(X_train_std, y_train)
```

+++

### 分類の正解率: 91.1%

```python
y_pred = ppn.predict(X_test_std)
accuracy_score(y_test, y_pred)
```

+++

### `joblib`で掃き出す

- Webアプリケーションでloadする
- 分類器: `joblib.dump(ppn, 'ppn_iris.pkl')`
- 標準化のScaler: `joblib.dump(sc, 'sc_iris_petal.pkl')`

+++

### APIがやること

1. 花びらのlengthとwidthのJSONがPOSTされる(実測値)
1. 分類器に渡す前に標準化する
1. 分類器で分類する
1. 分類結果をJSONで返す

+++

### ファイル類の配置

- app
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

+++

### Webアプリ側で読み込む

```python
sc = joblib.load('sc_iris_petal.pkl')
ppn = joblib.load('ppn_iris.pkl')
```

+++

### ソースコードに起こす

```python
input_ = request.get_json()
length = float(input_['length'])
width = float(input_['width'])
input_std = sc.transform(np.array([[length, width]]))
prediction = ppn.predict(input_std)
response = jsonify({'prediction': int(prediction[0])})
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

###


---
