課題2 (2014/6/2)
=========

できあがった図をファイルに保存，GitHub のレポジトリのページに表示，そして TeX でレポートを書く．

* 提出方法：GitHub にファイルをプッシュする．
* 締め切り：6月7日 (土)



## できあがった図をファイルに保存する

直線の本数や間隔を変えた図を2つ作って，それぞれファイルに保存してみましょう．

パラメタの値の範囲や刻みあるいは個数のセットを2つ用意する．
それぞれセット0, セット1と呼ぶことにする．
(例えば，セット0では t は -2 から 2 まで 13 個の値を動く，セット1では t は -3 から 3 まで 31 個の値を動く，とか．)


### PNG ファイル

まず，PNG ファイルに保存する．
2つのファイルに envelope0.png, envelope1.png という名前をつけるとする (拡張子が重要)．

ファイルに保存するのは `savefig` という命令．
`plt.show()` の直前に

```python
plt.savefig(envelope0.png)
```

と書いて実行すると，(いまのパラメタの値がセット0なら) セット0の図が envelope0.png に保存される
(python スクリプトファイルと同じフォルダ内)．

パラメタの値をセット1に変え，また，`plt.savefig(envelope0.png)` を

```python
plt.savefig(envelope1.png)
```

と変えて実行すると，セット1の図が envelope1.png に保存される．

* 例えば，
  セット0実行時
  
  ```python
  value_max, num_values = 2, 13
  #value_max, num_values = 3, 31
  ```
  
  セット1実行時
  
  ```python
  #value_max, num_values = 2, 13
  value_max, num_values = 3, 31
  ```
  
  のように，使わない方に "#" をつけるようにすると，少し手間が減る．

* ただ，本当は，パラメタ値のセットのリストを作って，そのリストの要素に関する `for` ループを作って回すべき．

透過ファイルにして，余白をゼロにしたければ `transparent=True, bbox_inches='tight', pad_inches=0` をつけて

```python
plt.savefig(envelope0.png, transparent=True, bbox_inches='tight', pad_inches=0)
```

あるいは

```python
plt.savefig(envelope1.png, transparent=True, bbox_inches='tight', pad_inches=0)
```

とする．


### PDF ファイル

PDF ファイルにも保存しておく．

セット0, セット1それぞれに対して，

```python
plt.savefig(envelope0.pdf, bbox_inches='tight', pad_inches=0)
```

および

```python
plt.savefig(envelope1.pdf, bbox_inches='tight', pad_inches=0)
```

と書いて実行する (拡張子に注意)．

現状で，作業フォルダ内に envelope0.png, envelope1.png, envelope0.pdf, envelope1.pdf の4つのファイルが存在するはず．
SourceTree でこれらのファイルをコミット&プッシュしておく．



## PNG ファイルを GitHub レポジトリのページに表示させる

(最初の項をとばしてここからやりたい人は，[testimages](testimages) の中の
envelope0.png と envelope1.png をダウンロードして作業フォルダに保存し，SourceTree でコミット&プッシュしておいてください．)

README.md ファイルに次のように書き込む：

```
私のプログラムの出力結果です：

![envelope0](envelope0.png)
![envelope1](envelope1.png)
```

もしサイズ調整したかったら

```
私のプログラムの出力結果です：

<img src="envelope0.png" alt="envelope0" width="120"/>
<img src="envelope1.png" alt="envelope1" width="120"/>
```

と書き込む (width のあとの数字を適宜調整する)．

README.md ファイルの編集のしかたは2通りあって，

* 自分のコンピュータの作業ファイル内の README.md をいつも使っているテキストエディタで開いて編集
  (そのあと SourceTree で README.md をコミット&プッシュ)
* Web ブラウザで自分の GitHub のレポジトリのページに行って README.md を開き，Edit ボタンを押して編集

のいずれかでやる．

Web ブラウザで自分の GitHub のレポジトリのページを開いて，うまくいっているか確認．

[Writing on GitHub](https://help.github.com/categories/88/articles)



## TeX でレポートを書く

(最初の項をとばしてここからやりたい人は，[testimages](testimages) の中の
envelope0.pdf と envelope1.pdf をダウンロードして作業フォルダに保存し，SourceTree でコミット&プッシュしておいてください．)

[sample.tex](sample.tex) を開き，その中身を

* 奥村本から TeX をインストールした人は，TeXShop (Mac) あるいは TeXWorks (Windows) で新しいファイルを新規作成してコピー
* 大学では，mi で新しいファイルを新規作成してコピー

して，たとえば envelope-report.tex という名前で作業ファイル内に保存する (拡張子重要)．


### 奥村本から TeX をインストールした人

TeXShop (Mac) あるいは TeXWorks (Windows) で「タイプセット」する．


### 大学

「[まず使ってみる](http://hwb.ecc.u-tokyo.ac.jp/current/applications/latex/)」に書いてあるとおりにやってみる．


いずれの場合も，エラーが出たらエラーメッセージとともに (みんなも Cc して) メール送ってください．


### レポートの中身を書く

* 包絡線定理について説明する．
* 自分のコードについて説明する．工夫した点，今後の課題などを述べる．


できたら (途中でも) envelope-report.tex と envelope-report.pdf ファイルを SourceTree でコミット&プッシュする．
(ほかにもたくさんファイルができるが，それらはプッシュしない．)