課題2 (2014/6/2)
=========

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
