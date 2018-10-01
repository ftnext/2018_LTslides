# Django Girls Tutorial翻訳に参加して（仮）
#### PyLadies Tokyo 4周年記念パーティ LT (2018/10/08)
#### nikkie

---

# PyLadies Tokyo 4周年 おめでとうございます！ @fa[birthday-cake]

+++

### このLTでは

- おめでたい場におめでたいことを持ち寄りました！
- 祝 Django2.0.x対応 Django Girls Tutorial日本語版リリース @fa[birthday-cake]
- 翻訳に参加して得たものについて話します

+++

### About nikkie

- Software Engineer (3rd year)
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [Qiita](https://qiita.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/05~ Join Translation (& Reviewer)
- 2018/09 #stapy 4代目LT王子戴冠

---

### Django Girls Tutorial

- ブログを作るチュートリアル
- 対象者：プログラミング未経験者
- Django：PythonでWebアプリを作るためのパッケージ
- Djangoに入門したい方にオススメ

+++

### Django Girls Tutorial

- 旧バージョン：Django 1.11.x
  - https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/content/
- 新バージョン：Django 2.0.x
  - https://tutorial.djangogirls.org/ja/

+++

### 新バージョンのTutorial

- Django2.0.xに合わせてアップデート
  - urls.py: `path()`
  - models.py: `on_delete=models.CASCADE`
- デプロイ先はPythonAnywhere（Herokuからの卒業）

---

### Django Girls Tutorial翻訳に参加して

1. Djangoの使い方をつかんだ
1. Django Girls Tutorialに精通した
1. コミュニティに加わった

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
- Django Girls Tutorialって実は。。。

+++

### ここが好き

> But it's not super important right now, so we will skip it.

- ブログの投稿が見つからないときに404エラーページを表示する
- 404エラーページのカスタマイズは「super importantじゃないから、今はやらない」

+++

### 実は、誤植もあります。。

- Pull Request上げていきます！
- 例えば、デプロイ！ではまだ作っていないファイルがPythonAnywhereに送られています

```
(ola.pythonanywhere.com) $ ls blog/
__init__.py __pycache__ admin.py forms.py migrations models.py static
templates tests.py urls.py views.py
```

+++

### コミュニティに加わる

- Django Girls Tutorial修了レベルでも歓迎していただけた（感謝）
- 翻訳 → レビュー → コーチ とステップアップ
- 一歩でも先にいれば、教えられることがある

+++

### コミュニティに加わって思うこと

- みんなで力を合わせて翻訳を成し遂げたのだから、多くの方に使ってほしい（フィードバック歓迎！）
- 詰まったら、質問先の一つとして@ftnextまでお気軽にどうぞ
- nikkie自身は、アウトプットでDjango入門した方のお役に立てたらと考えています

---

### まとめ：Django Girls Tutorial翻訳に参加して

- Djangoの使い方がつかめた
- 精通したので、Pull Requestでアップデートしていく
- コミュニティに受け入れていただけたので、今後は恩返ししていきたい

+++

### ご清聴ありがとうございました。

[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)をよろしくお願いします！<br>
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
