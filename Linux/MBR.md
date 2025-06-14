# MBR
# MBRのブロックサイズについて

MBR（Master Boot Record）は、コンピュータのハードディスクやその他のブートデバイスの最初のセクタに位置するデータ構造です。MBRに関するブロックサイズの主な特徴は以下の通りです：

- **基本サイズ**: MBRは一般的に**512バイト**のセクタに格納されています
- **構成内訳**:
  - 最初の**446バイト**: ブートローダーコード
  - 次の64バイト: パーティションテーブル（16バイト×4エントリ）
  - 最後の2バイト: ブートシグネチャ（0x55, 0xAA）

MBRを使用したパーティショニングでは、セクタサイズは通常512バイトで、これが基本的なブロックサイズとなります。ただし、現代の大容量ストレージデバイスではMBRの2TB制限があるため、GPT（GUID Partition Table）が代わりに使用されることが増えています。

# MBRのパーティションテーブル

パーティションテーブルの64バイト（16バイト×4エントリ）は、**ディスク上のパーティション（区画）の情報を記録するために**使用されます。

## パーティションテーブルの主な役割

- ハードディスクをどのように論理的に分割するかの「地図」を提供
- 各パーティションの位置、サイズ、種類を定義
- OSがディスクのどの部分をどう使うべきかを示す

## 各エントリ（16バイト）に含まれる情報

- **ブートフラグ**（1バイト）：そのパーティションが起動可能かどうか
- **パーティション開始位置**の情報
- **パーティションタイプ**（1バイト）：NTFS、FAT32、Linuxなどのファイルシステム種別
- **パーティションサイズ**の情報

これらの情報に基づいて、OSは起動時にディスクを適切に認識し、各パーティションにアクセスできるようになります。
# ブートシグネチャとは

ブートシグネチャは、MBR（Master Boot Record）の**最後の2バイト**に位置する特別な値で、以下の特徴があります：

## 基本情報
- **具体的な値**: `0x55AA`（16進数）
- **MBR内の位置**: 最後の2バイト
- **表記**: リトルエンディアン形式で、ディスク上では実際に「55 AA」の順で保存

## 主な目的
- **ブート可能セクタの識別**: BIOSが==このセクタが有効なブートセクタであることを認識するための「印」==
- **整合性チェック**: コンピュータ起動時、BIOSはこのシグネチャを確認

## 重要性
- このシグネチャが正しくない場合、BIOSはそのディスクからの起動を拒否
- ブートプロセスの最初のステップとして機能
- どのディスク・デバイスが起動可能かをBIOS/UEFIが判断する基準になる

簡単に言えば、「このセクタはブートセクタとして有効です」とBIOSに伝えるための標識として機能します。