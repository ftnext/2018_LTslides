# Djangoにモザイクアート
#### みんなのPython勉強会#34 (2018/04/03)
#### nikkie

---

### nikkie (@ftnext)

- 3年目ソフトウェアエンジニア（サーバーサイド、機械学習）
- [Twitter @ftnext](https://twitter.com/ftnext)、[はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- ほしいもの「Django Congress チケット」

+++

https://speakerdeck.com/ftnext/pillow-mosaic-art-nyumon

![Pillowでモザイクアート](stapy_April_django/assets/20180116PyNyumonLT-slide1.png)

+++?image=stapy_April_django/assets/20180116PyNyumonLT-slide20.png&size=contain

+++

### みんなのPython勉強会#33 (2018/03)

## 「Pythonを学んだ人にWebもオススメしたい理由」@hirokiky

+++

### Road to "Djangoにモザイクアート"

- 作成済みのモザイクアートを表示する
- ボタンを押すとモザイクアートが作られて表示される
- モザイクアートの設定値がいじれる
- <span>注意: <span class="red-char>v1.11</span>で実装</span> |

---

### Step1: 作成済みのモザイクアートを表示する

- Django Girls Tutorial
- 画像ファイル=静的ファイルの扱い(staticフォルダ)

+++

### Django Girls Tutorial

- [プロジェクトを作成しよう](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/django_start_project/)
- [Djangoモデル](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/django_models/)
- [Django urls](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/django_urls/)
- [Djangoビュー](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/django_views/)
- [テンプレートに表示しよう](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/django_templates/)
- [CSSでカワイくしよう](https://djangogirlsjapan.gitbooks.io/workshop_tutorialjp/css/)

+++

### MosaicArtモデル

- user: モザイクアートを作成したユーザ
- file_name: モザイクアートのファイル名
- original_image: モザイクアートにした元の画像
- created_date: モザイクアート作成日時

+++

### モザイクアート表示

- 静的ファイルとして表示
```lang=html
{% load static %}
{% get_static_prefix as STATIC_PREFIX %}

<img src="{{ STATIC_PREFIX }}images/target/{{ mosaic_art.original_image }}">
<img src="{{ STATIC_PREFIX }}images/{{ mosaic_art.user }}/{{ mosaic_art.file_name }}" width="400" height="400">
```

+++

### staticフォルダ配置

- Django Girls Tutorial
  - ├ mysite/  <- Project
  - ├ gallery/ <- Application
  - ├ static/  <- Mosaic arts (PNG file)
  - └ manage.py
- この配置ではmanage.pyの`BASE_DIR`の取得が参考になる

+++

### staticフォルダ配置(2)

- アプリケーションフォルダの中に配置する
  - ├ mysite/  <- Project
  - ├ gallery/ <- Application
    - └ static/
      - └ gallery/
        - (Mosaic arts...)

+++?image=https://pbs.twimg.com/media/DY0mx1kVwAE4k9J.jpg&size=contain

---

### ボタンを押すとモザイクアートが作られて表示される

- フォームのサブミットボタン
- 設定値決め打ちでモザイクアートを作成

+++

https://twitter.com/ftnext/status/977475056535138304

---

### モザイクアートの設定値がいじれる

- モザイクアートにする画像を選べるようにした

+++

### モザイクアートのソースコード

- モザイクアートにする画像がべた書き
- 作成したモザイクアートのファイル名がべた書き
- → これらを引数で持たせるように修正
- （他にもべた書きが多い）
