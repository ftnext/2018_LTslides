# Entrance of Docker for Pythonista
## 〜Dockerではじめる<br>機械学習モデルのデプロイ〜
#### みんなのPython勉強会#38 (2018/09/12) nikkie

---

### お詫び: 副題変更

- 当初「DockerではじめるPython環境構築」
- 参加者の皆さまの関心の高いトピックでDockerについて話すため、「Dockerではじめる機械学習モデルのデプロイ」に変更

+++

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- Software Engineer (3rd year)
	- Self-taught Python@color[#eba3ff](@fa[heart]) & Docker@color[#eba3ff](@fa[heart]@fa[heart])
	- 二つ名「Pythonのもくもく会でAzureでハマっている人」
	- 2018/08~ [株式会社キカガク](https://www.kikagaku.co.jp)にエンジニアとしてJoin

+++

### Joined Translation

- Django Girls Tutorial 翻訳に関わりました
	- https://tutorial.djangogirls.org/ja/
	- Django 2.0.x
	- Deploy to PythonAnywhere (not Heroku)
- この秋、Django Girls Workshop Coachデビュー

+++

### About this talk

- 一推しのDockerをPythonistaに知ってほしい！使ってほしい！
	- Dockerをまだ触ったことがない方が触るきっかけとなれば幸いです
- 題材: @color[#e22b30](機械学習のモデルをAPIとして公開)
	- Dockerを使ってAPIとして公開します

+++

### 注意事項

- Dockerについてはざっくり理解を優先した説明です
- Appendixも用意しましたが、わからないことは遠慮なく質問してください
- Docker独学の身なので、詳しい方がいらっしゃったら懇親会で教えてください

---

### 目次

- @color[#e22b30](Dockerとは？)
- 機械学習のモデルをAPIとして公開
	- 次の話の中で手順をブレイクダウンします

+++

### Dockerとは？

- アプリケーションが動作する状態で持ち運べるプラットフォーム
	- Dockerの仕組みに沿えば、どこへでも持ち運べる
- アプリケーションの持ち運びに関連する2概念
	- イメージ
	- コンテナ

+++

### イメージとは？

- 動作可能なアプリケーション（ただし動作はしていない）
	- <span class="later-explained">ソースコード+実行環境</span>
	- <span class="later-explained">Dockerfile(テキストファイル)から`build`される</span>
		- <span class="later-explained">Dockerfileにはイメージの作成手順を書く</span>
- イメージを持ち運ぶ
	- <span class="later-explained">クラウド上のリポジトリにアップロードして、イメージを共有(配布)できる</span>
	- <span class="later-explained">例: 開発環境(Docker使用)で`build`したイメージをDocker Hub(リポジトリ)にアップロード</span>

+++

### イメージとは？

- 動作可能なアプリケーション（ただし動作はしていない）
	- ソースコード+実行環境
	- Dockerfile(テキストファイル)から`build`される
		- Dockerfileにはイメージの作成手順を書く
- イメージを持ち運ぶ
	- <span class="later-explained">クラウド上のリポジトリにアップロードして、イメージを共有(配布)できる</span>
	- <span class="later-explained">例: 開発環境(Docker使用)で`build`したイメージをDocker Hub(リポジトリ)にアップロード</span>

+++

### イメージとは？

- 動作可能なアプリケーション（ただし動作はしていない）
	- ソースコード+実行環境
	- Dockerfile(テキストファイル)から`build`される
		- Dockerfileにはイメージの作成手順を書く
- イメージを持ち運ぶ
	- クラウド上のリポジトリにアップロードして、イメージを共有(配布)できる
	- 例: 開発環境(Docker使用)で`build`したイメージをDocker Hub(リポジトリ)にアップロード

+++

### コンテナとは？

- 動作させたイメージ（＝動作するアプリケーション）
	- イメージを`run`するとコンテナが起動する
- <span class="later-explained">仮想マシンのようにも見える</span>
	- <span class="later-explained">イメージを`run`する際に、ホストマシンと仮想マシンの間の設定をする</span>
	- <span class="later-explained">例: ポート、ディレクトリの共有設定</span>

+++

### コンテナとは？

- 動作させたイメージ（＝動作するアプリケーション）
	- イメージを`run`するとコンテナが起動する
- 仮想マシンのようにも見える
	- イメージを`run`する際に、ホストマシンと仮想マシンの間の設定をする
	- 例: ポート、フォルダの共有設定

+++

### Dockerでデプロイするには

1. アプリケーションを用意
1. Dockerfileを書いてイメージ作成
1. イメージをリポジトリにアップロード
1. デプロイ先でイメージを取得し、実行(`run`)する

+++

### Dockerを使って機械学習のモデルをAPIとして公開するには

1. アプリケーションを用意
	1. @color[#e22b30](機械学習のモデル)を用意
	1. 機械学習のモデルを@color[#e22b30](APIに組み込む)
1. Dockerfileを書いてイメージ作成
1. イメージをリポジトリ(@color[#e22b30](Docker Hub))にアップロード
1. デプロイ先でイメージを取得し、実行(`run`)する
	- @color[#e22b30](GCPのVM(Ubuntu 16.04))で実行

---

### 目次（更新版）

- <span class="already-explained-item">Dockerとは？</span>
- @color[#e22b30](機械学習のモデルを用意)
- 機械学習のモデルをAPIに組み込む
- イメージ作成 & リポジトリにアップロード
- デプロイ先でイメージを実行

+++

### 今回の分類器

- あやめの品種の分類器を作る
	- Irisデータセット(あやめの花のデータ)
	- 花びらの長さ 5.1cm, 幅 2.4cm -> 品種は virginica と分類
- scikit-learnを使う

+++

### あやめの分類器作成手順

- 目標: あやめの花びらの長さと幅から品種を分類する
	1. データセットの分割
	1. 花びらの長さと幅のデータを標準化
	1. パーセプトロンを学習
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
- [『Python機械学習プログラミング』 3章](https://github.com/rasbt/python-machine-learning-book/blob/master/code/ch03/ch03.ipynb)に基づく

+++

### パーセプトロンの学習、性能確認

- 分類の正解率: 91.1%

```python
ppn = Perceptron(max_iter=40,
		eta0=0.1, random_state=0, shuffle=True)
ppn.fit(X_train_std, y_train)
y_pred = ppn.predict(X_test_std)
accuracy_score(y_test, y_pred)
```

- [『Python機械学習プログラミング』 3章](https://github.com/rasbt/python-machine-learning-book/blob/master/code/ch03/ch03.ipynb)に基づく

+++

### `joblib`で掃き出す

- 分類器: `joblib.dump(ppn, 'ppn_iris.pkl')`
- 標準化のScaler: `joblib.dump(sc, 'sc_iris_petal.pkl')`
- Webアプリケーションで`joblib.load`して使うため
- ここまでのソースコード: [ftnext/iris_perceptron.ipynb](https://gist.github.com/ftnext/07bccfa93b24edec29292ec548e8d6e3)

---

### 目次

- <span class="already-explained-item">Dockerとは？</span>
- <span class="already-explained-item">機械学習のモデルを用意</span>
- @color[#e22b30](機械学習のモデルをAPIに組み込む)
- イメージ作成 & リポジトリにアップロード
- デプロイ先でイメージを実行

+++

### あやめの分類器をAPIに組み込む

- 機械学習のモデルのAPI化には、Flaskが向く

> ウェブフレームワークの1つ（『独学プログラマー』p.218）

- エンドポイント(`/predict`)
	- 利用者は花びらの長さと幅のJSONデータをPOSTする
	- APIがあやめの品種を返す

+++

### APIの処理

1. 花びらの長さと幅のJSONがPOSTされる
	- `{ "length": 5.1, "width": 2.4 }`
1. 分類器に渡す前に、POSTされた長さと幅の値を標準化する
1. 分類器で分類する
1. 分類結果をJSONで返す
	- `{ "prediction": "virginica" }`

+++

### ソースコードに書き起こす (app.py)

```python
sc = joblib.load('sc_iris_petal.pkl')
ppn = joblib.load('ppn_iris.pkl')

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

- [GitHub ftnext/iris_api app/app.py](https://github.com/ftnext/iris_api/blob/20c7733c31faf98c9050f2d243382dbe49c176fa/app/app.py)

+++

### ファイルの配置

- app
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl
- appディレクトリ内で`python app.py`で開発サーバ起動

+++

### Flaskの開発サーバで動作確認

<span class="api-result-img">
![Flaskの開発サーバのレスポンス](stapy_Sep_docker/assets/local_flask_api.png)
</span>

---

### 目次

- <span class="already-explained-item">Dockerとは？</span>
- <span class="already-explained-item">機械学習のモデルを用意</span>
- <span class="already-explained-item">機械学習のモデルをAPIに組み込む</span>
- @color[#e22b30](イメージ作成 & リポジトリにアップロード)
- デプロイ先でイメージを実行

+++

### イメージを作成する

- イメージ＝ソースコード+実行環境
	1. APIのソースコードを配置
	1. APIを実行する設定をする
		- gunicornを使って本番サーバとして実行
		- 開発サーバ(`python app.py`で実行するサーバ)は、APIとして公開する際は使うべきではない

+++

### ファイル類の配置

- @color[#2743d2](Dockerfile) <- 追加
- @color[#2743d2](requirements.txt) <- 追加
- app <- @color[#e22b30](中身をイメージへ配置)
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

+++

### イメージの環境設定: requirements.txt

- イメージに以下のパッケージを`pip install`

```txt
Flask==1.0.2
gunicorn
numpy==1.13.3
scikit-learn==0.19.2
scipy==1.1.0
```

+++

### Dockerfileに書き起こす

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

### リポジトリにアップロード

1. イメージ作成: `docker build -t <イメージ名:バージョン> .`
1. リポジトリにアップロード
	- `docker login` してから `docker push <イメージ名:バージョン>`
開発環境でイメージの動作確認する場合
	- `docker run -i -t --rm -p 5000:5000 <イメージ名:バージョン>`
	- 注: 開発環境は、Docker for Mac(18.06.1-ce-mac73)

+++

### 動作の様子 (Docker for Mac)

<span class="api-result-img">
![コンテナの本番サーバのレスポンス](stapy_Sep_docker/assets/container_flask_api.png)
</span>

---

### 目次

- <span class="already-explained-item">Dockerとは？</span>
- <span class="already-explained-item">機械学習のモデルを用意</span>
- <span class="already-explained-item">機械学習のモデルをAPIに組み込む</span>
- <span class="already-explained-item">イメージ作成 & リポジトリにアップロード</span>
- @color[#e22b30](デプロイ先でイメージを実行)

+++

### デプロイ戦略

- 大きく2通り考えられる
- VM利用: dockerコマンドを設定。取得したイメージをrunする
- PaaS利用: リポジトリのイメージを指定するだけ

+++

### VMにデプロイ！

- GCPにUbuntu16.04のVMを構築
- dockerコマンドを設定
	- 参考: [GCEの無料枠を使って個人用Mastodonを立てる(translucensさん はてなブログ)](https://translucens.hatenablog.jp/entry/mastodon-gce)
- イメージを取得して`run`する
- 注: この方法は本番環境としてAPIを運用するには不適切(Kubernetesを使うべき)

+++

### 動作の様子

<span class="api-result-img">
![コンテナの本番サーバのレスポンス](stapy_Sep_docker/assets/gcp_vm_flask_api.png)
</span>

+++

### PaaSにデプロイ！

- AzureのWebAppsにはイメージを指定することも可能
- しかし、ローカル、GCPのVMでは動くイメージがWebAppsでは動作しない。。
	- 「Pythonのもくもく会でAzureでハマっている人」(再掲)
	- 原因調査中。引き続き宿題事項として取り組んでいきます。。

---

### まとめ: Entrance of Docker for Pythonista

- あやめの分類器をAPIにし、DockerでGCPのVMにデプロイした
- Dockerは、アプリケーションが動作する状態で持ち運べるプラットフォーム
	- イメージ: アプリケーションのソースコード+実行環境
	- コンテナ: 動作させたアプリケーション

+++

### Dockerを使った機械学習モデルのデプロイ(仮説)

1. モデルを用意する（精度にこだわって）
2. FlaskでAPI化
3. アプリケーションをコンテナ化
4. VM(またはPaaS)にデプロイ
	- VMはGCPに限らない
	- centOSの場合もdockerを設定すればよい

+++

### ご清聴ありがとうございました。
Dockerを触ってみようと思っていただけたら幸いです
## Happy Docker Life!
Contact: [Twitter @ftnext](https://twitter.com/ftnext)<br>
参考資料、Appendixが続きます

+++

### 参考資料

- O'Reilly [『Docker』](https://www.oreilly.co.jp/books/9784873117768/): Flaskアプリをイメージにする手順が学べます
- モデルのAPI化: [A Flask API for serving scikit-learn models](https://towardsdatascience.com/a-flask-api-for-serving-scikit-learn-models-c8bcdaa41daa)
- 定期的に[Dockerを取り上げてくださるサポーターズ勉強会](https://supporterzcolab.com/search/?q=docker)で知見を深めました

---

# Appendix

TODO: このあと詰める

+++

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
