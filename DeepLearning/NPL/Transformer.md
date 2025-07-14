# Transformer

[[注意機構]]（Attention Mechanism）のみを用いた深層学習モデルアーキテクチャで、2017年にVaswaniらによって提案された。従来のRNNやCNNを使用せず、Self-Attentionとしても知られる[[自己注意機構]]を中心に構築されている。

## アーキテクチャ

Transformerはエンコーダ・デコーダ構造を持ち、以下の主要コンポーネントから構成される：

### エンコーダ
- **Multi-Head Attention**：複数の[[注意機構]]を並列実行
- **Position-wise Feed-Forward Network**：各位置に対する[[全結合層]]
- **Residual Connection**：[[残差接続]]による勾配消失問題の緩和
- **Layer Normalization**：[[正規化]]による学習の安定化

### デコーダ
- **Masked Multi-Head Attention**：未来の情報を参照しない[[注意機構]]
- **Encoder-Decoder Attention**：エンコーダ出力への[[注意機構]]
- **Position-wise Feed-Forward Network**
- **Residual Connection**と**Layer Normalization**

## 主要な特徴

### 自己注意機構
入力系列の各位置が、同じ系列内の全ての位置との関連性を計算する仕組み。以下の式で表される：

$$
\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

ここで、$Q$（Query）、$K$（Key）、$V$（Value）は入力から線形変換により得られる。

### 位置エンコーディング
RNNのような逐次処理がないため、位置情報を明示的に与える必要がある。正弦波と余弦波を用いた[[位置エンコーディング]]により実現：

$$
\begin{align}
PE_{(pos, 2i)} &= \sin\left(\frac{pos}{10000^{2i/d_{model}}}\right) \\
PE_{(pos, 2i+1)} &= \cos\left(\frac{pos}{10000^{2i/d_{model}}}\right)
\end{align}
$$

### Multi-Head Attention
複数の[[注意機構]]を並列実行し、異なる表現部分空間での関連性を捉える：

$$
\text{MultiHead}(Q, K, V) = \text{Concat}(\text{head}_1, \ldots, \text{head}_h)W^O
$$

ここで各head$_i$は：
$$
\text{head}_i = \text{Attention}(QW_i^Q, KW_i^K, VW_i^V)
$$

## 利点

1. **並列化**：RNNと異なり、全ての位置を同時に処理可能
2. **長距離依存性**：直接的な[[注意機構]]により長距離の関連性を効率的に捉える
3. **解釈性**：[[注意重み]]の可視化により、モデルの判断根拠を理解しやすい
4. **汎用性**：様々なタスクに適用可能な柔軟なアーキテクチャ

## 応用例

### 自然言語処理
- **機械翻訳**：元の提案論文での主要タスク
- **[[BERT]]**：双方向エンコーダ表現
- **[[GPT]]**：生成型事前学習モデル
- **文書要約**、**質問応答**、**感情分析**など

### コンピュータビジョン
- **Vision Transformer (ViT)**：画像分類タスク
- **DETR**：物体検出タスク

### その他
- **音声認識**
- **プロテイン構造予測**
- **時系列予測**

## 計算複雑度

Self-Attentionの計算複雑度は系列長$n$に対して$O(n^2)$であり、長い系列に対しては計算コストが高い。これを改善するために、以下のような手法が提案されている：

- **Sparse Attention**：[[疎な注意機構]]
- **Linear Attention**：線形時間での近似
- **Longformer**：局所的・大域的注意の組み合わせ

## 訓練技術

### 事前学習
- **Masked Language Modeling**：ランダムにマスクされた単語の予測
- **Next Sentence Prediction**：文の順序予測
- **Autoregressive Language Modeling**：次の単語の予測

### 微調整
事前学習済みモデルを特定のタスクに適応させる[[転移学習]]手法。

Transformerは自然言語処理分野に革命をもたらし、現在の[[大規模言語モデル]]の基盤となっている重要なアーキテクチャである。