# 翻訳は<br>人のためならず
### 〜Django Girls Tutorial翻訳で<br>学んだ3つのこと〜
#### PyLadies Tokyo 4周年記念パーティ LT (2018/10/08)
#### nikkie

---

# PyLadies Tokyo<br>4周年 おめでとう<br>ございます！ @fa[birthday-cake]

+++

### おめでたい場に<br>おめでたいことも持ち寄りました！

+++

# 祝 Django Girls<br>Tutorial 日本語版<br>Django2.0.x対応 @fa[birthday-cake]

+++

### LT: 翻訳は人のためならず

- 翻訳に参加して学んだことを話します
- ×: 翻訳は人のためにならないからやらない方がよい
- ○: 翻訳は他の人のためだけでなく自分のためになる

+++

### LT: 翻訳は人のためならず

1. 自己紹介
2. Django Girls Tutorialの紹介
3. 翻訳で学んだ3つのこと（LTのメイン）

+++

### About nikkie

- Software Engineer (3rd year)
- 2018/05~ Join Translation (& Reviewer)
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- Self-taught Python@color[#eba3ff](@fa[heart]) & Docker@color[#eba3ff](@fa[heart])

---

### Django Girls Tutorial とは

- プログラミング未経験者向け
- Djangoを使ってブログを作り、インターネットに公開する
- 「Djangoに入門したい方にオススメ」と評価されている(個人的見解)
- ※ Django：PythonでWebアプリを作るためのパッケージ

+++

### Django Girls Tutorial Django2.0.x対応とは

- 2017年12月Djangoの2系がリリース
- Tutorial（英語版）も2系にアップデート
- 翻訳して日本語版Tutorialも<br>アップデート ←イマココ

+++

### Django2.0.x対応での変更点

- Django2系に合わせてコードのアップデート

```python
# mysite/urls.py
    path('', include('blog.urls')),
# blog/models.py
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
```

- デプロイ先はPythonAnywhere（Herokuからの卒業）
- https://tutorial.djangogirls.org/ja/

---

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### Djangoの使い方

- 翻訳とレビューで手を動かす中で、以下のフローを抽出
  1. プロジェクトを作る `django-admin startproject mysite .`
  1. アプリケーションを作る `python manage.py startapp blog`
  1. settings.py編集 `INSTALLED_APPS`など
  1. 機能追加手順(次スライド)

+++

### Djangoの使い方-機能追加手順

1. 新規ページへ遷移するリンクを追加
1. 新規ページのURL設定
1. （新規モデル作成）
1. 新規ページのビュー作成
1. 新規ページのテンプレート作成

+++

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### Django Girls Tutorialに精通

- Django Girls Tutorialのここが好き
- Django Girls Tutorialのお茶目なところ

+++

### ここが好き (@fa[heart])

- ブログの投稿が見つからないときに404エラーページを表示する
- 404エラーページのカスタマイズは「super importantじゃないから、今はやらない」

> But it's not super important right now, so we will skip it.

- super importantなものに集中する姿勢 (@fa[heart])

+++

### お茶目なところ

- Pull Request上げていきます！
- 例えば、デプロイ！ではまだ作っていないファイルがPythonAnywhereに送られています

```
(ola.pythonanywhere.com) $ ls blog/
__init__.py __pycache__ admin.py forms.py migrations models.py static
templates tests.py urls.py views.py
```

+++

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### コミュニティの力

- 少しずつ力を出し合って、2.0.x対応を達成
- -> 次は多くの方に使ってほしい
- フィードバック歓迎！（もっといいものにしていきたい）

---

### まとめ：翻訳は人のためならず

- Djangoの使い方がつかめた
- 精通したので、Pull Requestでアップデートしていく
- コミュニティの力で翻訳を達成した

+++

### 思うこと

- Django Girls Tutorial修了レベルで翻訳に参加
  - 「一歩でも先にいれば、教えられることがある」
- 受け入れていただいたコミュニティに、今後は恩返ししていきたい
  - 「アウトプットがDjango入門した方のお役に立てたら」

+++

### ご清聴ありがとうございました。

[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)をよろしくお願いします！<br>
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
