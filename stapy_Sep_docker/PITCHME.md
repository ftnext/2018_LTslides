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
- app <- @color[#e22b30](イメージにて`app.py`を実行)
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

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
	- [DockerHub ftnext/iris_api](https://hub.docker.com/r/ftnext/iris_api/)
念のため、開発環境でイメージの動作確認
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

### Appendix

- Docker導入
- VirtualBoxと何が違うのか？
- ソースコードについて(Flask/Dockerfile)
- dockerコマンドについて
	- `build`, `login`, `push`, `run`
- docker-compose.yml
- 本番環境での運用
- APIの動作確認ツール

+++

### Docker導入

- [今日からはじめるDocker - コンテナー仮想化の必要性を理解して、まず開発環境に導入してみよう！](https://employment.en-japan.com/engineerhub/entry/2017/09/28/110000)
	- Windowsの方: Docker for Windows
		- サポートされていないWindowsの場合: Docker Toolbox
	- Macの方: Docker for Mac
- なお、私はMacでのみDocker経験があります

+++

### コンテナはVirtualBoxと何が違うのか？

- コンテナは仮想マシンのようにも見える
- 違いは目的(『Docker』p.4)
	- VirtualBoxは異なる環境の再現が目的
	- コンテナはアプリケーションを持ち運べるようにすることが目的
- アーキテクチャ(ハイパバイザ型／コンテナ型)の話は今回は省略します

+++

### Flaskソースコード解説 1/2

```python
@app.route('/predict', methods=['POST'])
def predict():
	# POSTされたJSONを取得(input_は辞書として扱える)
    input_ = request.get_json()
	# POSTされた長さと幅は文字列なので、小数に変換する
    length = float(input_['length'])
    width = float(input_['width'])
	# 長さと幅の値を標準化
    input_std = sc.transform(np.array([[length, width]]))
	# :
```

+++

### Flaskソースコード解説 2/2

```python
@app.route('/predict', methods=['POST'])
def predict():
	# :
	# predictionは分類器が返した0~2のラベル
    prediction = ppn.predict(input_std)
	# IRIS_KINDにラベルと品種名を定義済み
	# 品種を含むJSON(APIの返す値)を用意する
    response = jsonify(
        {'prediction': IRIS_KIND[int(prediction[0])]})
    response.status_code = 200
    return response
```

+++

### Dockerfile解説 1/3

```Dockerfile
# Python3.6系が設定済みのUbuntu環境をベースにする
FROM python:3.6
RUN apt update && apt install python-dev -y
# ホストマシンに用意したファイル一式をイメージの/home以下にコピー
COPY . /home
```

+++

### `COPY . /home`後の`/home`の中身

- Dockerfile
- requirements.txt
- app
  - app.py
  - ppn_iris.pkl
  - sc_iris_petal.pkl

+++

### Dockerfile解説 2/3

```Dockerfile
RUN cd /home && pip install -r requirements.txt
```

- イメージに以下のパッケージを`pip install`

```txt
Flask==1.0.2
gunicorn
numpy==1.13.3
scikit-learn==0.19.2
scipy==1.1.0
```

+++

### Dockerfile解説 3/3

```Dockerfile
# イメージの5000番ポートを解放
EXPOSE 5000
# /home/app以下(app.pyがあるフォルダ)を対象にする
WORKDIR /home/app
# gunicornを使ってapp.pyを5000番ポートで動作させる
ENTRYPOINT ["gunicorn", "-b", "0.0.0.0:5000", "--access-logfile", "-", "--error-logfile", "-"]
CMD ["app:app"]
```

+++

### 今回のDockerfileには問題がある

- 問題: rootユーザでアプリケーションを実行していること
- rootユーザとは別にアプリケーション実行用のユーザを作るべき（『Docker』より）
- 宿題事項として、今後アップデートします

+++

### イメージの作成: `docker build`

- Dockerfileからイメージを作成するコマンド
- 例: `docker build -t ftnext/iris_api:1.0 .`
	- 最後の`.`はカレントディレクトリにあるDockerfileを指定している
	- `-t`で指定しているのはイメージのタグ名
		- タグ名の書式は「リポジトリ名/イメージ名:バージョン」

+++

### リポジトリへのアップロード: `docker login`と`docker push`

- `docker login`: DockerHubに対話的にログイン
- `docker push ftnext/iris_api:1.0`: 端末内にある`ftnext/iris_api:1.0`イメージをDockerHubにアップロード

+++

### リポジトリへのアップロード 注釈

- 実は今回は`docker login`と`docker push`を使っていない
- GitHubリポジトリとDockerHubリポジトリを連携させる設定をしている
	- 参考: [Qiita DockerhubのAutomated build を設定する](https://qiita.com/FoxBoxsnet/items/a31fc46681d9b67c8cc6)

+++

### コンテナ起動: `docker run`

- イメージからコンテナを起動する: `docker run -i -t --rm -p 5000:5000 ftnext/iris_api:1.0`
	- 基本はイメージを指定: `docker run ftnext/iris_api:1.0`
	- Dockerfileで定義されている`ENTRYPOINT`命令が実行される
		- `CMD`命令で指定された引数が渡る
		- 参考: [Qiita dockerのENTRYPOINTとCMDの書き方と使い分け、さらに併用](https://qiita.com/hnakamur/items/afddaa3dbe48ad2b8b5c)

### コンテナ起動時の実行コマンド指定

- コンテナで実行したい命令も指定できる: `docker run python:3.6 bash`
	- `python:3.6`イメージからコンテナを起動し、bashコマンドでシェルを実行
	- コンテナの入力・出力の設定をすると、コンテナに接続した状態になる(後述)
- DockerfileのCMD命令に代えて、`docker run`で渡したコマンドが実行される
- `docker run`のオプションについては次のページへ

+++

### `docker run`の`-i -t`, `--rm`オプション

- `-i -t`: コンテナへの入力・出力の設定
	- 例: `docker run -i -t python:3.6 bash`
	- 結果: コマンドラインからコンテナに接続した状態になる
- `--rm`: コンテナが停止したときにコンテナを削除する
	- コンテナで作ったファイルやコンテナにインストールしたパッケージは消える

+++

### `docker run`の`-p`オプション

- `-p`: ポートの共有設定
	- 書式は、ホストのポート番号:ゲストのポート番号
	- `docker run -p 5000:5000 ftnext/iris_api:1.0`とすると、 http://127.0.0.1:5000/predict でコンテナ内のAPIを叩ける
	- 端末の5000番ポートへのアクセスが、コンテナの5000番ポートへのアクセスとして扱われる

+++

### docker-compose.yml

- `docker run`時の設定をyml形式のファイルに書き出せる
	- `docker-compose.yml`のあるフォルダで`docker-compose up`
- 複数のイメージを扱う必要があるときに役に立つ
	- 例: DjangoのイメージとMySQLのイメージを用意。MySQLのコンテナ -> Djangoのコンテナの順で起動したい

+++

### 本番環境での運用: Kubernetes

- 本番環境で`docker run`や`docker-compose up`をするのは不適切
	- コンテナの状態を常時監視できないため
- 本番環境では、コンテナの監視を提供する **オーケストレーションツール** を使う必要がある
- デファクトのオーケストレーションツールはKubernetes
- [こちらの勉強会スライド](https://docs.google.com/presentation/d/1_mQJQ0Yz1zJHqUPefNYNPfx5mjHEbfRwTzUOaWi8vZ8/edit#slide=id.p)で勉強中です

+++

### APIの動作確認ツール

- Advanced REST clientを使用
- Google Chromeの拡張として入手できる

+++

### EOF
