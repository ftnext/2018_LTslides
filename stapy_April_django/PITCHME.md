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

<script async class="speakerdeck-embed" data-slide="20" data-id="c2f8d454de5c490f94ea26220eeef55a" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

+++

### みんなのPython勉強会#33 (2018/03)

# 「Pythonを学んだ人にWebもオススメしたい理由」@hirokiky

+++

### Road to "Djangoにモザイクアート"

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
