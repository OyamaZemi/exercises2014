課題3 (2014/6/9)
=========

Fictitious play のシミュレーションをしてみる．

* 提出方法：GitHub にファイルをプッシュする．
* 締め切り：6月21日 (土)


## Fictitious Play

[Fictitious play の説明](http://nbviewer.ipython.org/github/OyamaZemi2014/exercises/blob/master/ex03/fictplay_notes.ipynb)


## やること

1. 説明をよく読んで，0 期から T-1 期までの信念 x_0(t), x_1(t) の動きをプロットする
   (T は 100 とか 1000 とか自分で設定する)．

   An Introductory Example - quant-econ の
   [Exercise 5](http://quant-econ.net/python_by_example.html#exercise-5)
   をお手本にしてみましょう．  
   (ただし，`pylab` ではなく `matplotlib.pyplot` を使うようにしましょう．)

2. 上で作ったプログラムを何回も回して x_0(T-1) のリストを作る．
   それをヒストグラムとして表示する．

   ヒストグラムの表示方法は
   [Matplotlib - quant-econ](http://quant-econ.net/matplotlib.html)
   参照のこと．


## 拡張

* 他の 2x2 ゲームでもやってみる．
* 3x3 ゲームもやってみる．
* 利得や選択にランダムネスを入れてみる．
