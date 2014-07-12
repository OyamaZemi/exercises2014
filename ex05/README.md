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


## 発展

* [Object Oriented Programming - quant-econ](http://quant-econ.net/python_oop.html)
  にならって class を定義して使ってみる．
* 3x3 ゲームもやってみる．


## 定常状態 (2014/7/12)

遷移行列を書いてしまえば，あとはそれを mc_tools.py の `mc_compute_stationary`
に渡せば定常状態を返してくれるわけですが，
突然変異の確率 epsilon がとても小さかったり，プレイヤーの数がとても大きかったりすると，
負の要素を含むベクトルを返してくることがあるようです．

以下の議論を参照：

* [4×4行列で、こんな例を見つけました](https://github.com/haru110jp/KMR/commit/73033cc0dab28d6b9f32cba2fdf55b88f520dbee)
* [mc_compute_stationary returns a vector with a negative element?](https://github.com/haru110jp/KMR/issues/1)

対処法は考え中．
