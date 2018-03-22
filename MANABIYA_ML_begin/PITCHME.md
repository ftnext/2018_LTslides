# 機械学習を<br>はじめたいあなたへ
#### MANABIYA LT大会【AI LT枠】(2018/03/23)
#### nikkie

---

### nikkie

- ソフトウェアエンジニア(4月から3年目)
- [Twitter @ftnext](https://twitter.com/ftnext)、[はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 1月から案件ドリブンで機械学習に従事 |
  - Azure ML Studio(後述)でレコメンド |
  - 「回帰」「分類」は知っているが、<br>使ったことはなかった |

+++

### LT: 機械学習をはじめたいあなたへ

- 機械学習に興味のある方が一歩を踏み出すとっかかりになったら。 |
- 機械学習をバリバリやっている方からの質問や指摘、大歓迎です！ |

---

### 機械学習

- アルゴリズムを用いてデータからモデルを作成: 学習 |
- モデルは未知のデータについて予測する |
- (例)レコメンド: 商品の評価データをもとに作ったモデルでユーザへのオススメ商品を予測 |

+++

# 機械学習は

# not 目的

# but <span class="red-char">手段</span>

+++

### やりたいことファースト

- やりたいことの達成を最優先で機械学習に取り組もう
  - 自分でモデルを作らなくてもいい |
  - 必要な知識はつまみ食いで要領よく |

+++

### 以下の3名にnikkieから提案

- Aさん: 画像に何が写っているか知りたい |
- Bさん: 手元のデータで機械学習をやりたい |
- Cさん: 機械学習を勉強したい |

---

### 画像に何が写っているか知りたいAさんへ

- APIとして公開されている学習済みのAIを使おう |
- 一から機械学習に取り組まなくてもAさんのやりたいことは達成できる |

+++?image=MANABIYA_ML_begin/assets/images/computer-vision-api-image.png&size=contain

+++

### 学習済みのAIを使う

- 例: Computer Vision API
- APIを呼び出すだけで機械学習の結果が使える

---

### 手元のデータで機械学習をやりたいBさんへ

- 使いやすい機械学習のツールを使おう |
- 機械学習の考え方を身につけよう |

+++

### scikit-learn

- 代表的なライブラリ(Python製)
- アルゴリズムは実装済み。数学の知識がなくても動かせる |
- 一つの道: PythonやPythonでのデータ処理の仕方(pandas)を学んでscikit-learnを使う |

+++

### Azure Machine Learning Studio

- <span>ブラウザでアクセス: https://studio.azureml.net/</span>
- アルゴリズムは実装済み。数学の知識がなくても動かせる |
- コーディング不要。GUIでドラッグ&ドロップ |

+++?image=MANABIYA_ML_begin/assets/images/recommend_sample-7.png&size=contain

+++

### 機械学習の考え方

- ツールを使いこなすために必要
- 身につけたら実務に役立った
  - カテゴリ値の扱い |
  - トレーニングデータとテストデータの分け方 |

---

### 機械学習を勉強したいCさんへ

- 私が今後勉強していきたい部分を紹介
- (アルゴリズムを理解するための数学的な勉強の優先度は低いという立場)
- 数学的な勉強をするというアプローチももちろんあり |

+++

### 一番重要と思うこと: データの傾向の把握

- そもそもデータが偏っていたらモデルの性能はよくない |
- データの傾向の把握は「探索的データ解析」と呼ばれる |

+++

### 探索的データ解析を勉強するには

- kaggleのkernelを見るのがよさそう |
  - kaggle: データ解析コンペのプラットフォーム |
  - kernel: 参加者が公開しているコンペでのデータ解析の事例 |

+++?image=MANABIYA_ML_begin/assets/images/kaggle-kernel.png&size=contain

---

### まとめ

- 公開されているAIを使うことで、機械学習に取り組む必要がない場合がある
- scikit-learnやAzure ML Studioなどから自分にあったツールを使おう
- 事例から「探索的データ解析」のやり方を学ぶとよさそう

+++

### ご清聴ありがとうございました

+++

### 画像URL

- <span class="ref-char">Computer Vision API イメージ: https://qiita.com/ftnext/items/970069ff509f69812f23</span>
- <span class="ref-char">Azure ML Studioでレコメンド: https://raw.githubusercontent.com/ftnext/CogBot11-LT-201801/master/image/recommend_sample-7.png</span>
- <span class="ref-char">kaggleのkernel: https://www.kaggle.com/c/titanic/kernels?sortBy=votes&group=everyone&pageSize=20&competitionId=3136</span>
