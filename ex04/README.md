課題4 (2014/6/23)
=========

TeX の beamer クラスを使って，fictitious play のプログラムに関する発表資料を作る．

* 提出方法：GitHub にファイルをプッシュする．
* 締め切り：6月28日 (土)



## できあがった図をファイルに PDF 形式で保存する

[課題2](../ex02/README.md)でやったとおり．

たとえば，matchingpennies_plot.pdf という名前で保存したければ
`plt.show()` の直前に

```python
plt.savefig('matchingpennies_plot.pdf')
```

と書く．
余白をゼロにしたければ

```python
plt.savefig('matchingpennies_plot.pdf', bbox_inches='tight', pad_inches=0)
```

とする．


## TeX でスライドを作る

(最初の項をとばしてここからやりたい人は，[testimages](testimages) の中のダミーファイル
matchingpennies_plot.pdf をダウンロードして作業フォルダに保存し，SourceTree
でコミット&プッシュしておいてください．
あとで自分のプログラムの出力ファイルに入れかえること．)

[beamer-sample.tex](beamer-sample.tex) を開き，その中身を

* 奥村本から TeX をインストールした人は，TeXShop (Mac) あるいは TeXWorks (Windows)
で新しいファイルを新規作成してコピー
* 大学では，mi で新しいファイルを新規作成してコピー

して，たとえば fictplay-slides.tex という名前で作業ファイル内に保存する (拡張子重要)．

タイプセットする．
エラーが出なければ fictplay-slides.pdf というファイルができる．

やり方を忘れた人は[課題2](../ex02/README.md)やゼミの
[Wiki](http://oyamazemi.wiki.fc2.com) の関連箇所を見てみる．

(6/27追記)
ゼミの Wiki の [Beamer](http://oyamazemi.wiki.fc2.com/wiki/Beamer)
の項目での指摘にしたがって，beamer-sample.tex で `containsverbatim` を `fragile` に変更．


### スライドの中身を書く

fictplay-slides.tex を編集して発表スライドの中身を書く
(「[LaTeX](http://hwb.ecc.u-tokyo.ac.jp/current/applications/latex/)」の各項目参照)．

* Fictitious play について説明する．
* 自分のコードについて説明する．工夫した点，今後の課題などを述べる．

**コピペ厳禁！**
自分の言葉で書くこと．引用する場合は引用元を明記すること．

* beamer-sample.tex の設定は一番シンプルなものになっている．
  凝りたければ「beamer テーマ」などで Google で検索せよ．

できあがったら (途中でも) fictplay-slides.tex と fictplay-slides.pdf の2つのファイルを
SourceTree でコミット&プッシュする．
(ほかにもたくさんファイルができるが，それらはプッシュしない．)

`handout` オプションをつけた状態でタイプセットしてできたものをコミット&プッシュすること．


### PDF ファイルに README.md からリンクを張る

fictplay-slides.pdf を Google Docs Viewer を通して表示させる．
