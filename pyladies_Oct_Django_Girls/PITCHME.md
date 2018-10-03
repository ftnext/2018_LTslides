# 翻訳は人のためならず
### 〜Django Girls Tutorial翻訳で学んだこと〜
#### PyLadies Tokyo 4周年記念パーティ LT (2018/10/08)
#### nikkie

---

# PyLadies Tokyo 4周年 おめでとうございます！ @fa[birthday-cake]

+++

### おめでたい場におめでたいことも持ち寄りました！

+++

# 祝 Django Girls Tutorial 日本語版 Django2.0.x対応バージョンリリース @fa[birthday-cake]

+++

### LT: 翻訳は人のためならず

- ×: 翻訳は人のためにならないからやらない方がよい
- ○: 翻訳は他の人のためだけでなく自分のためになる
- 翻訳に参加して学んだことを話します

+++

### About nikkie

- Software Engineer (3rd year)
- 2018/05~ Join Translation (& Reviewer)
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09 #stapy 4代目LT王子戴冠

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
- 翻訳して日本語版Tutorialもアップデート ←イマココ

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
1. チームで達成

+++

### Djangoの使い方

- 翻訳とレビューの中で手を動かす中で、以下のフローを抽出
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

### Django Girls Tutorialに精通

- Django Girls Tutorialのここが好き
- Django Girls Tutorialのお茶目なところ

+++

### ここが好き

> But it's not super important right now, so we will skip it.

- ブログの投稿が見つからないときに404エラーページを表示する
- 404エラーページのカスタマイズは「super importantじゃないから、今はやらない」

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

### チームで達成

- 少しずつ持ち寄って、リリースを達成
- みんなで力を合わせて翻訳を成し遂げたのだから、多くの方に使ってほしい
- お茶目なところを見つけたら、フィードバック歓迎！

---

### まとめ：翻訳は人のためならず

- Djangoの使い方がつかめた
- 精通したので、Pull Requestでアップデートしていく
- 少しずつ持ち寄って、チームで達成した

+++

### 思うこと

- Django Girls Tutorial修了レベルで翻訳に参加
  - 「一歩でも先にいれば、教えられることがある」
- コミュニティに受け入れていただけたので、今後は恩返ししていきたい
  - Django入門した方のお役に立てるアウトプットができたら

+++

### ご清聴ありがとうございました。

[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)をよろしくお願いします！<br>
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
