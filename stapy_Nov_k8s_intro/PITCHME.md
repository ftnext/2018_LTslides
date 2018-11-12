# Kubernetesはじめの一歩
## "Entrance of Docker for Pythonista"アップデート
#### みんなのPython勉強会#39 (2018/11/14) nikkie

---

### LT: Kubernetesはじめの一歩

- 9月のショートトーク(Dockerで機械学習モデルのデプロイ)のアップデート
- 機械学習モデルのDockerイメージをKubernetesでデプロイできました！

+++

### 注意書き

- Kubernetesの入り口に立ったレベルです
- 腹落ちしきっていない部分もあり、うまく言語化できていない箇所もあります
- Kubernetesに詳しい方からのコメント、大歓迎です！

+++

### About nikkie

- Software Engineer (Python & Docker @color[#eba3ff](@fa[heart]))
- 2018/09〜 stapy 4代目LT王子
- 2018/10〜 Django Girls Tutorial コーチ
- 2018/11 #ploneconf2018 お手伝い

---

### 目次

1. 9月のショートトーク要約
2. Kubernetesとは
3. Kubernetesを用いたデプロイ

+++

### 9月のショートトーク

- [Entrance of Docker for Pythonista 〜Dockerではじめる機械学習モデルのデプロイ〜](https://gitpitch.com/ftnext/2018_LTSlides/master?p=stapy_Sep_docker/)
- Dockerを使って機械学習モデルをAPIとしてデプロイする方法について10分で話した
- [登壇報告 | #stapy にて機械学習モデルをDockerでデプロイする方法について話しました](http://nikkie-ftnext.hatenablog.com/entry/2018/09/21/202316)

+++

### Dockerとは(復習)

- アプリケーションが動作する状態で持ち運べるプラットフォーム
- イメージ：動作可能なアプリケーション。イメージを持ち運ぶ
- コンテナ：動作させたイメージ（＝動作するアプリケーション）

+++

### Dockerを使って機械学習モデルをAPIとしてデプロイ(復習)

1. モデルを用意する
1. FlaskでAPI化
1. アプリケーションをコンテナ化（Dockerfileを書いてビルド）
1. VM(またはPaaS)にデプロイ

+++

### 9月トークの課題: 本番運用

- 本番環境ではコンテナの監視機能が必要：**オーケストレーションツール**
- `docker run`や`docker-compose up`ではコンテナの状態を常時監視できない

---

### 目次

1. 9月のショートトーク要約
2. Kubernetesとは
3. Kubernetesを用いたデプロイ

+++

### Kubernetesとは

- オーケストレーションツール（コンテナの監視機能を提供）のデファクトスタンダード
- nikkieは「クバネテス」と読む派
- 略称：k + ubernete(8文字) + s
- クラウドベンダーは軒並み提供(GCP, AWS, Azure, IBM, ...)

+++

### 登場人物

- クラスタ
- リソース(ymlファイル)
- kubectlコマンド

+++

### k8sの入り口

- リソースをymlファイルで定義する
- 次の2つをおさえればデプロイは可能
  - Deployment: どのDockerイメージをいくつ動かした状態とするか
  - Service: Dockerコンテナに外部からアクセス可能にする(＝L4ロードバランサ)

---

### 目次

1. 9月のショートトーク要約
2. Kubernetesとは
3. Kubernetesを用いたデプロイ

+++

### k8sを用いたデプロイ

1. クラスタを作成して接続（VMを作成して接続）
1. ymlファイルを置く(deployment.yml, service.yml,)
1. kubectlコマンドでデプロイ

+++

### 1. クラスタを作成して接続

- 今回はAKS(Azure Kubernetes Service)を使用
- 参考: [Azure Kubernetes Service クイック スタートでk8sでのデプロイの概要を掴む](https://qiita.com/ftnext/items/1b34eba1a295be30a77d)
- GCPでもデプロイ可能と思われる

+++

### 2-1. deployment.yml

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    name: iris-web
  name: iris-web
spec:
  replicas: 1
  selector:
    matchLabels:
      name: iris-web
  template:
    metadata:
      labels:
        name: iris-web
    spec:
      containers:
      # ショートトークで使ったイメージを指定(1個動かす)
      - image: ftnext/iris_api
        name: iris-web
        ports:
        - containerPort: 5000
```

+++

### 2-2. service.yml

```yml
apiVersion: v1
kind: Service
metadata:
  name: iris-web
spec:
  ports:
  - port: 5000
  # deployment(name: iris-web)と結びつける
  selector:
    name: iris-web
  type: LoadBalancer
```

+++

### 3. kubectlコマンドでデプロイ

```shell
# 前提: クラスタに接続していて、カレントディレクトリに
# deployment.yml, service.ymlがある
kubectl apply -f deployment.yml
kubectl apply -f service.yml
kubectl get svc -w
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
iris-web     LoadBalancer   10.0.112.236   <pending>     5000:31530/TCP   17s
kubernetes   ClusterIP      10.0.0.1       <none>        443/TCP          16m
iris-web   LoadBalancer   10.0.112.236   13.78.17.226   5000:31530/TCP   35s
```

+++

### 機械学習モデルのAPIが動いた！

図を入れる

---

### まとめ：Kubernetesはじめの一歩

- 9月トークの宿題オーケストレーションツールについてアップデート
- DeploymentとServiceをおさえればデプロイできる
- 今後: Django Girls Tutorialのブログをk8sでデプロイしてみる

+++

### 参考資料

- [Kubernates (GKE) ハンズオン 講義用_20181028_@Repro](https://docs.google.com/presentation/d/1tBR4XjAHspA0UHYvfdPTUaRJmvUIVjKMPVV4ipFKXms/edit#slide=id.p)
  - サンプルのyamlファイルを元にガンガンデプロイします。k8sの大枠を掴む→yamlの書き方を掴むと目的を変えて数周しました

+++

### ご清聴ありがとうございました。
## Happy Docker Life!
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
