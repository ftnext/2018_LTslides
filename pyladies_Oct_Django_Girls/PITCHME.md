# 翻訳は<br>人のためならず
### 〜Django Girls Tutorial翻訳で<br>学んだ3つのこと〜
#### PyLadies Tokyo 4周年記念パーティ LT (2018/10/08)
#### nikkie

---

# PyLadies Tokyo<br>4周年 おめでとう<br>ございます！ @fa[birthday-cake]

+++

### おめでたい場に<br>おめでたいことも持ち寄りました！

+++

# 祝 @color[#ff9400](Django Girls<br>Tutorial) 日本語版<br>Django2.0.x対応 @fa[birthday-cake]

+++

### LT: 翻訳は人のためならず

- 翻訳に参加して学んだことを話します
- ×: 翻訳は人のためにならないからやらない方がよい
- ○: 翻訳は@color[#006bff](他の人のためだけでなく自分のためになる)

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
- 「@color[#006bff](Djangoに入門したい方にオススメ)」と評価されている(個人的見解)
- ※ Django：PythonでWebアプリを作るためのパッケージ

+++

### TutorialのDjango2.0.x対応とは

- 2017年12月Djangoの2系がリリース
- Tutorial（英語版）も2系にアップデート
- 翻訳して日本語版Tutorialも<br>アップデート ←@color[#006bff](イマココ)

+++

### Django2.0.x対応での変更点

- Django2系に合わせて@color[#006bff](コードのアップデート)

```python
# mysite/urls.py
    path('', include('blog.urls')),
# blog/models.py
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
```

- デプロイ先は@color[#006bff](PythonAnywhere)（Herokuからの卒業）
- Check it now!: https://tutorial.djangogirls.org/ja/

---

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### Django Girls Tutorial翻訳で学んだこと

1. @color[#006bff](Djangoの使い方)
1. Django Girls Tutorialに精通
1. コミュニティの力

+++

### Djangoの使い方

- 翻訳とレビューで手を動かす中で、以下のフローを抽出
  1. プロジェクトを作る
  1. アプリケーションを作る
  1. settings.py編集 `INSTALLED_APPS`など

```shell
$ django-admin startproject mysite .
$ python manage.py startapp blog
```

+++

### Djangoの使い方-機能追加手順

![機能追加フロー](pyladies_Oct_Django_Girls/assets/django_add_feature.png)

+++

### Django Girls Tutorial翻訳で学んだこと

1. Djangoの使い方
1. @color[#006bff](Django Girls Tutorialに精通)
  - ここが好き
  - お茶目なところ
1. コミュニティの力

+++

### ここが好き @fa[heart]

- ブログの投稿が見つからないときに404エラーページを表示する
- 404エラーページのカスタマイズは「super importantじゃないから、今はやらない」

> But it's not super important right now, so we will skip it.

- @color[#006bff](super importantなものに集中)する姿勢 @color[#eba3ff](@fa[heart])

+++

### お茶目なところ 🤫

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
1. @color[#006bff](コミュニティの力)

+++

### コミュニティの力

- 少しずつ力を出し合って、2.0.x対応を達成
- Django Girls Tutorial修了レベルで翻訳に参加
  - フォローし合って翻訳達成
- 受け入れていただいたコミュニティに、今後は恩返ししていきたい
  - 「Django中級者を目指すアウトプットで入門者のお役に立てたら」

---

### まとめ：翻訳は人のためならず

- Djangoの使い方がつかめた
- 精通したので、Pull Requestでアップデートしていく
- コミュニティの力で翻訳を達成した

+++

### 思うこと

- Django 2.0.x対応のチュートリアルを、次は多くの方に使ってほしい
- チュートリアルへのフィードバック歓迎！（もっといいものにしていきたい）

+++

### ご清聴ありがとうございました。

[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)をよろしくお願いします！<br>
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
