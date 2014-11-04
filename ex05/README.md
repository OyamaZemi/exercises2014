課題5 (2014/6/30)
=========

Kandori-Mailath-Rob (KMR) の確率進化モデルのシミュレーションをしてみる．

* 提出方法：GitHub にファイルをプッシュする (新規レポジトリを作成すること)．
* 締め切り：7月12日 (土)


## KMR モデル

[KMR の確率進化動学の説明](http://nbviewer.ipython.org/github/OyamaZemi2014/exercises/blob/master/ex05/KMR_notes.ipynb)


## やること

1. KMR モデルの説明をよく読んで，0 期から T-1 期までの X\_t の列を生成し，X\_t(N) の動きをプロットする．
   (epsilon は小さい値に設定し，それに依存して T は大きい値に設定する)．

2. また，X\_t そのものではなく，X\_t の実現値の頻度分布 \\bar{X}\_t の様子も調べる．
   (\\bar{X}\_t の動きをプロットしたり，\\bar{X}\_{T-1} の分布をヒストグラムにしてみたりする．)

3. {X\_t} の定常分布を求めてヒストグラムにする．
   epsilon を小さくしていって，定常分布の変化の様子を見る．

4. (ゼロから自分でコードを書いてもよいが)
   quant-econ の
   [discrete_rv.py](https://github.com/jstac/quant-econ/blob/master/quantecon/discrete_rv.py)
   と
   [mc_tools.py](https://github.com/jstac/quant-econ/blob/master/quantecon/mc_tools.py)
   が便利なので，それらを使わせてもらうことにする．

   (これらのファイルをダウンロードして作業フォルダに保存しておく．)

5. それぞれのグラフは png ファイルに保存し，前回同様 README.md からリンクして
   github.com のページに表示されるようにする．

6. あるいは，[ここ](http://nbviewer.ipython.org/github/oyamad/stochevolution/blob/master/KMR_2x2_example.ipynb)を参考にして，
   IPython notebook での実行例を保存した .ipynb ファイルをプッシュし，
   REAME.md から nbviewer.ipython.org を通してリンクする．

   たとえば，

   ```
   [実行結果](http://nbviewer.ipython.org/github/USERNAME/stochevolution/blob/master/KMR_2x2_example.ipynb)
   ```

   のように書く．
   ただし，

   * ユーザ名: USERNAME
   * レポジトリ名: stochevolution
   * ファイル名: KMR_2x2_example.ipynb

   になっているので，各自適切に変える．


## 発展

* [Object Oriented Programming - quant-econ](http://quant-econ.net/py/python_oop.html)
  にならって class を定義して使ってみる．
* 3x3 ゲームもやってみる．


## 定常分布 (2014/7/12)

遷移行列を書いてしまえば，あとはそれを mc_tools.py の `mc_compute_stationary`
に渡せば定常分布を返してくれるわけですが，
突然変異の確率 epsilon がとても小さかったり，プレイヤーの数がとても大きかったりすると，
負の要素を含むベクトルを返してくることがあるようです．

以下の議論を参照：

* [4×4行列で、こんな例を見つけました](https://github.com/haru110jp/KMR/commit/73033cc0dab28d6b9f32cba2fdf55b88f520dbee)
* [mc_compute_stationary returns a vector with a negative element?](https://github.com/haru110jp/KMR/issues/1)


## 定常分布 - その後 (2014/8/8)

### 原因

上記のような遷移行列では，最大固有値は 1 のはずですが，2番目に大きい固有値が 1 に非常に近いようで，
(古いバージョンの) `mc_compute_stationary` はその2番目の固有値に対する固有ベクトルを返してきていたようです．
そのような固有ベクトルは一般には (normalize しても) 確率分布にはならない．

### 対処法

浮動小数点計算の精度を上げて1番目と2番目の固有値の差が有意に判別できるようにすればよい．
[mpmath](http://mpmath.org) という，任意の精度で計算をしてくれるパッケージがあるので，それを使う．

それで書いてみたのが以下のコード：

* [mc_compute_stationary_mpmath.py](https://github.com/oyamad/test_mc_compute_stationary#mc_compute_stationary_mpmathpy)

その機能は新しいバージョンの
[mc_tools.py](https://github.com/QuantEcon/QuantEcon.py/blob/8ee46a2894550534ffb0e8bdf42f7d56994b271f/quantecon/mc_tools.py)
(2014/8/12 のバージョン)
に取り入れてもらいました．

### mpmath

その mpmath ですが：

* 固有値を計算してくれる `eig` という関数は mpmath version 0.18 以降でないと入っていない
  (現在の最新バージョンは0.19)．
* mpmath の最新版をインストールするのが一つの手だが，
  mpmath は [SymPy](http://sympy.org) というパッケージに含まれていて，
  その SymPy は Anaconda に含まれている．
* が，今学期はじめにインストールした Anaconda のバージョンは1.9.2で，そこに含まれる
  SymPy (version 0.7.4.1) に入っている mpmath のバージョンは0.17．
* Anaconda を最新版にアップデートすると，SymPy のバージョン0.7.5が入っていて，
  それに入っている mpmath のバージョンは0.18になっている．

ということで，ゼミの wiki の
「[Anaconda のアップデート](http://oyamazemi.wiki.fc2.com/wiki/Anaconda%20のアップデート)」
のページを参考にして Anaconda をアップデートしてください．

アップデートしたら，新しい `mc_compute_stationary` で定常分布が正しく返ってくるかチェックしてみてください．


## 定常分布 - その後 (2014/11/4)

その後，よく考えてみたのですが：

* マルコフ連鎖の遷移行列は必ず 1 を固有値にもっていて，固有値 1 に対応する固有ベクトルが定常分布，
  ということがわかっているのに，一般の固有値問題を解く関数を使うのは筋が悪い
* そもそも mpmath は遅い

と思い至りました．

### Grassmann-Taksar-Heyman (GTH) アルゴリズム

P を遷移行列とすると，定常分布は
x P = x すなわち x (P - I) = 0 という x (行ベクトル) についての連立線形方程式の 0 ベクトル以外の (基準化) 解として求まります
(I は単位行列)．
連立方程式の解法のひとつに[ガウスの消去法](http://ja.wikipedia.org/wiki/ガウスの消去法) (あるいは掃き出し法)
というのがありますが，
このアルゴリズムは引き算を含むので epsilon がとても小さかったりプレイヤーの数が大きかったりするときに使うと，
非常に近い数どうしの引き算が[桁落ち](http://ja.wikipedia.org/wiki/誤差#.E6.A1.81.E8.90.BD.E3.81.A1)を引き起こし，
まったく見当違いの答を返してくることがあります．
(このような桁落ちが最初のケースで起きていたと考えられます．)

GTH アルゴリズムは，入力行列 P - I がもつ「行についての和はつねに 0」という性質を使って引き算を回避するものです．
桁落ちが起きないので，KMR 行列でも正しく定常分布を求めてくれます．
詳しくは[この資料](http://www.sti.uniurb.it/events/sfm07pe/slides/Stewart_1.pdf)
(pp.44-81) 参照のこと．

Numpy を使って書いたのが [gth_solve.py](https://github.com/QuantEcon/QuantEcon.py/blob/master/quantecon/gth_solve.py)．

GTH アルゴリズムは既約な遷移行列にしか使えないので，可約な行列を既約な行列に分解するアルゴリズムを実装するコードも書いて，
あわせて QuantEcon ライブラリに入れてもらいました．
バージョン 0.1.6 から使えるようになっています．

経緯については以下の以下の議論を参照のこと：

* [MARKOV: More efficient implementation for computing stationary distributions](https://github.com/QuantEcon/QuantEcon.py/pull/79)

### QuantEcon ライブラリのアップデート

すでに QuantEcon ライブラリをインストールしている人は，ターミナルで `-U` オプションをつけて

```
pip install quantecon -U
```

と打ってアップデートしてください．

アップデート完了後ターミナルで

```
python -c "import quantecon; print quantecon.__version__"
```

と打って `0.1.6` と返ってくれば正しくインストールされています．
