# Djangoにモザイクアート
#### みんなのPython勉強会#34 (2018/04/03)
#### nikkie

---

### nikkie (@ftnext)

TODO: 自己紹介を入れる

+++

### Pillowでモザイクアート(2018/01)

https://speakerdeck.com/ftnext/pillow-mosaic-art-nyumon

+++

### みんなのPython勉強会#33 (2018/03)

# 「Pythonを学んだ人にWebもオススメしたい理由」@hirokiky

+++

# モザイクアート on Django

+++

### Road to モザイクアート on Django

- 作成済みのモザイクアートを表示する
- ボタンを押すとモザイクアートが作られて表示される
- モザイクアートの設定値がいじれる

---

### 作成済みのモザイクアートを表示する

- Django Girls Tutorial
- staticフォルダ

+++

### staticフォルダ問題

- manage.pyと同じ階層にstaticフォルダを配置する
  - Django Girls Tutorialで採用
- アプリケーションフォルダの中に配置する
  - blog/
    - └ static/
        - └ blog/

+++

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">&lt;img&gt;タグのsrc属性の指定でだいぶハマった。<br>{% static &quot;{{モデル.プロパティ}}&quot; %}ってやるとDBに格納しているファイル名が展開されないが、<br>{{STATIC_PREFIX}}{{モデル.プロパティ}}って並べるとDBに格納しているファイル名が展開された。<a href="https://t.co/ti4kLDCZJQ">https://t.co/ti4kLDCZJQ</a><br>テンプレートに並べてみました。 <a href="https://t.co/9JLAVScVBx">pic.twitter.com/9JLAVScVBx</a></p>&mdash; nikkie (@ftnext) <a href="https://twitter.com/ftnext/status/976480577388883968?ref_src=twsrc%5Etfw">2018年3月21日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

---

### ボタンを押すとモザイクアートが作られて表示される

- フォームのサブミットボタン
- 設定値決め打ちでモザイクアートを作成

+++

<blockquote class="twitter-video" data-lang="ja"><p lang="ja" dir="ltr">わーい、Djangoでモザイクアート作れるようになったーー！<br><br>やむをえずもろもろ決め打ちにしているので改善点しかないんですが、一つ一つ潰していきます。<br>現状は私のTwitterアイコンしかモザイク化できませんし、モザイクに使うパーツも決め打ちです。 <a href="https://t.co/bfi0SfjmoY">pic.twitter.com/bfi0SfjmoY</a></p>&mdash; nikkie (@ftnext) <a href="https://twitter.com/ftnext/status/977475056535138304?ref_src=twsrc%5Etfw">2018年3月24日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
