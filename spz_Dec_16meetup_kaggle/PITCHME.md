# Kaggleの<br>タイタニックに<br>取り組んで<br>感じたこと
#### 16卒エンジニア限定ミートアップ LT (2018/12/14)
#### nikkie

---

### Too Long; Didn't Listen

>テーマは「この一ヶ月で知ったこと／感じたこと」

[2018/12/14 16卒エンジニア限定 "忘年会" ミートアップ](https://supporterzcolab.com/event/647/)

### Kaggleに入門して感じたことを共有します

注: 機械学習分野の話になります

+++

### About nikkie ([@ftnext](https://twitter.com/ftnext))

- Software Engineer (3rd year)
  - Server（Python独学 & 業務）
  - Infrastructure（Docker独学、Azure業務）
- [はてなブログ](http://nikkie-ftnext.hatenablog.com/)、[Qiita](https://qiita.com/ftnext)
- 2018/06 meetup LT [FlaskをAzureにデプロイして知った2つのこと](https://gitpitch.com/ftnext/2018_LTSlides/master?p=spz_June_16meetup)

+++

### diff of nikkie

- 転職しました！
- 2018/08~ 株式会社キカガク
- 2018/11~ 先輩に課題を出してもらう形でKaggleをスタート（機械学習勉強中）

+++

### 目次

- Kaggleとは？ タイタニックとは？
- 感じたこと
- まとめ

---

### Kaggleのタイタニックに取り組んで<br>感じたこと

- <div class="kaggle-color-highlight">Kaggleとは？ タイタニックとは？</div>
- 感じたこと
- まとめ

+++

### Kaggleとは

- データサイエンスコンペのプラットフォーム
- コンペでは、学習用データとテスト用データが与えられる
  - 学習用データからモデルを構築
  - モデルでテスト用データを推論した結果を提出

+++

### タイタニック

- Kaggleの入門者用コンペ
- https://www.kaggle.com/c/titanic
- 沈没したタイタニック号の乗客データを扱う
- 乗客の属性から、生存者／死亡者を予測するモデルを作り、精度(accuracy)を競う

+++

### 乗客データ 1/2

- PassengerId: 1
- Pclass(チケットの等級): 3 (一番低い)
- Name: Braund, Mr. Owen Harris さん
- Sex: 男性(male)
- Age: 22歳
- SibSp(同乗した兄弟/配偶者): 1人

+++

### 乗客データ 2/2

- Parch(同乗した両親/子供): 0人
- Ticket: A/5 21171
- Cabin: NA
- Fare(運賃): 7.25
- Embarked(乗船した港): S
- →死亡

---

### Kaggleのタイタニックに取り組んで<br>感じたこと

- Kaggleとは？ タイタニックとは？
- <div class="kaggle-color-highlight">感じたこと</div>
- まとめ

+++

### 感じたこと：想像以上にしんどい。。

- 精度が全然上げられない。
- <div class="kaggle-color-highlight">悪戦苦闘その1：提出練習用データセットの精度超え</div>
- 悪戦苦闘その2：精度80%超え

+++

### 提出練習用データセット

- 試しに提出することができるデータセット
- 性能：0.76555
- ロジックはシンプル。女性が助かり、男性が死亡と予測

+++

### 0.76555が全然超えられない😱

<canvas data-chart="line">
<!--
{
  "data": {
    "labels": ["sample", "try1", "try2", "try3", "try4", "try5", "try6", "try7"],
    "datasets": [
      {
        "data":[0.76555, 0.72727, 0.74162, 0.75119, 0.75119, 0.74641, 0.76076, 0.77990],
        "label":"accuracy","backgroundColor":"rgba(20,220,220,.8)"
      }
    ]
  },
  "options": { "responsive": "true" }
}
-->
</canvas>

+++

### 欠損値の扱い

- 属性データには欠損が含まれる
- Age(年齢)の扱いがポイント
  - 学習用データ891件のうち177件(19.9%)欠けている
  - テスト用データ418件のうち86件(20.1%)欠けている

+++

### ひとまず平均値で埋めてみる

- 年齢の欠損を学習用データの平均(30歳)で埋めた
- アルゴリズムはランダムフォレストを選択
- 精度 0.72727 (< 0.76555)

+++

### Pclassごとの平均で埋める

Pclass | 1 | 2 | 3
----- | ----- | ----- | ------
平均年齢 | 38 | 30 | 25

- 学習用データから算出
- アルゴリズムはランダムフォレストを選択
- 精度 0.74162 (< 0.76555)

+++

### アルゴリズムを変更

- 先輩の示唆：LightGBM, XGBoost → LightGBMを選択
- early_stoppingさせて、精度 0.77990（ようやく > 0.76555）
- 注: アルゴリズム以外にも特徴量の追加など行っています（時間都合により省略）

---

### 感じたこと：想像以上にしんどい。。

- 精度が全然上げられない。
- 悪戦苦闘その1：提出練習用データセットの精度超え
- <div class="kaggle-color-highlight">悪戦苦闘その2：精度80%超え</div>

+++

### 先人の知恵: PclassとSexごとの平均

- 80%超えという課題に対して[Titanic Data Science Solutions
カーネル](https://www.kaggle.com/startupsci/titanic-data-science-solutions)を真似た
- それぞれのデータについて平均年齢を算出（表は学習用データのもの）

Pclass | 1 | 2 | 3
----- | ----- | ----- | ------
男性 | 40 | 30 | 25
女性 | 35 | 28 | 21.5

+++

### ぎりぎり80%に届かずorz

- アルゴリズムはXGBoostを選択
- 精度 0.79904

---

### Kaggleのタイタニックに取り組んで<br>感じたこと

- Kaggleとは？ タイタニックとは？
- 感じたこと
- <div class="kaggle-color-highlight">まとめ</div>

+++

### 振り返り：なぜ悪戦苦闘しているのか

- Kaggleという戦場で武器のマニュアルを読んでいる状態
- 精度向上に繋がる見込みが高い施策と低い施策の区別がつかない（時間を費やしてもちょっとしか精度を上げられない）
- lightgbm, xgboostがブラックボックス（2種類APIがあって混乱）

+++

### Try（やってみること）

- lightgbm, xgboostのチュートリアルで手を動かして、使い方を把握する
- カーネルを情報収集して、大きく精度を上げている方法を真似て手を動かす

+++

### まとめ：Kaggleのタイタニックに取り組んで感じたこと

- kaggle入門は苦しい
- タイタニックでは思うように精度をあげられず悪戦苦闘(中)
- すべて成長の余地（伸びしろ）ととらえて、Kaggleでの実践と本やWebでの情報収集を両輪で進めてみる

+++

### ご清聴ありがとうございました

Contact: [Twitter @ftnext](https://twitter.com/ftnext)
