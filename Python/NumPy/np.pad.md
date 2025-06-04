# np.pad

`numpy.pad` は、NumPy 配列の周りにパディング（余白）を追加するための関数です。画像処理、信号処理、畳み込みニューラルネットワークなど、様々な分野で活用されています。

## 基本構文

```python
numpy.pad(array, pad_width, mode='constant', **kwargs)
```

## 主なパラメータ

- **array**: パディングする配列（入力配列）
- **pad_width**: 各軸（次元）の前後に追加するパディング幅
  - 単一の整数: すべての軸の前後に同じ幅を追加
  - タプル `(before, after)`: すべての軸に対して前と後ろに異なる幅を追加
  - タプルのシーケンス: 各軸ごとに個別にパディング幅を指定
- **mode**: パディング方法（デフォルトは 'constant'）
- **kwargs**: モードに応じた追加パラメータ

## 主なモード

1. **'constant'**: 定数値でパディング
   - `constant_values`: パディングに使用する値（デフォルト: 0）

2. **'edge'**: 配列の端の値を使ってパディング

3. **'reflect'**: 配列の要素を反射してパディング
   - 境界の値自体は反射に含まれない

4. **'symmetric'**: 配列の要素を対称的に反射
   - 境界の値も反射に含まれる

5. **'wrap'**: 配列の要素を周期的に繰り返す

## 使用例

```python
import numpy as np

# 1次元配列の例
arr = np.array([1, 2, 3, 4])

# 両端に2つずつ0を追加
padded_constant = np.pad(arr, 2, mode='constant')
# 結果: [0 0 1 2 3 4 0 0]

# 値5でパディング
padded_value = np.pad(arr, 2, mode='constant', constant_values=5)
# 結果: [5 5 1 2 3 4 5 5]

# エッジパディング
padded_edge = np.pad(arr, 2, mode='edge')
# 結果: [1 1 1 2 3 4 4 4]

# 反射パディング
padded_reflect = np.pad(arr, 2, mode='reflect')
# 結果: [3 2 1 2 3 4 3 2]

# 2次元配列の例
arr_2d = np.array([[1, 2], [3, 4]])

# 上下左右に1行/列ずつパディング
padded_2d = np.pad(arr_2d, 1, mode='constant')
# 結果: 
# [[0 0 0 0]
#  [0 1 2 0]
#  [0 3 4 0]
#  [0 0 0 0]]

# 軸ごとに異なるパディング幅を指定
padded_asymmetric = np.pad(arr_2d, ((1, 2), (3, 1)), mode='constant')
# 結果:
# [[0 0 0 0 1 2 0]
#  [0 0 0 0 3 4 0]
#  [0 0 0 0 0 0 0]
#  [0 0 0 0 0 0 0]]
```

画像処理などではこの関数を使って、画像の周りに余白を追加したり、畳み込み操作の前処理として利用されることが多いです。