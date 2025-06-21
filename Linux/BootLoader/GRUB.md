# GRUB

[[BootLoader|ブートローダー]]の一つで、GNU GRand Unified Bootloaderの略称。Linuxシステムにおいて最も広く使用されているブートローダーであり、複数のオペレーティングシステムを選択して起動できるマルチブート機能を提供する。

GRUBは、コンピュータの起動時に実行される最初のプログラムの一つで、カーネルを読み込んでオペレーティングシステムを起動する役割を担う。ハードディスクやUSBメモリなどの記憶媒体から起動可能で、複数のオペレーティングシステムがインストールされている環境でユーザーが選択できるブートメニューを表示する。

## GRUB Legacy と GRUB2 の違い

### GRUB Legacy（GRUB 0.9x）

GRUB Legacyは初期のバージョンで、現在では廃止されている。以下の特徴がある：

**アーキテクチャ**
- シンプルな単一ステージ設計
- 限られた機能セット
- 基本的なファイルシステムサポート

**設定ファイル**
- `/boot/grub/menu.lst` または `/boot/grub/grub.conf`
- 手動での設定が必要
- 設定の変更には直接ファイルを編集

**制限事項**
- 2TB以上のディスクサポートが限定的
- [[GPT]]パーティションテーブルのサポートが不完全
- UEFIファームウェアに対応していない

### GRUB2（GRUB 1.9x以降）

GRUB2は完全に書き直されたバージョンで、現在の標準となっている：

**アーキテクチャ**
- モジュラー設計
- 動的ローディング機能
- 豊富なファイルシステムサポート（ext2/3/4、XFS、Btrfs、ZFS等）

**高度な機能**
- [[UEFI]]ファームウェアへの完全対応
- [[GPT]]パーティションテーブルのサポート
- 2TB以上の大容量ディスクサポート
- 暗号化されたファイルシステムからの起動
- ネットワークブート（PXE）機能
- グラフィカルなブートメニュー

**スクリプト機能**
- Bashライクなスクリプト言語
- 条件分岐やループ処理
- 変数の使用が可能

## 設定ファイルの構造

### GRUB2の主要設定ファイル

**メイン設定ファイル**
- `/boot/grub/grub.cfg` - 実際の設定ファイル（自動生成）
- `/etc/default/grub` - グローバル設定
- `/etc/grub.d/` - 設定スクリプトディレクトリ

**設定スクリプトの構成**
- `00_header` - 基本設定とヘッダー
- `05_debian_theme` - テーマ設定（Debian系）
- `10_linux` - Linuxカーネルエントリの生成
- `20_linux_xen` - Xenハイパーバイザーエントリ
- `30_os-prober` - 他のOSの自動検出
- `40_custom` - カスタムエントリ
- `41_custom` - 追加のカスタムエントリ

### 重要な設定パラメータ

**タイムアウト設定**
```bash
GRUB_TIMEOUT=5
GRUB_TIMEOUT_STYLE=menu
```

**デフォルト起動エントリ**
```bash
GRUB_DEFAULT=0
GRUB_SAVEDEFAULT=true
```

**カーネルパラメータ**
```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""
```

**解像度設定**
```bash
GRUB_GFXMODE=1024x768
GRUB_GFXPAYLOAD_LINUX=keep
```

## 設定の更新方法

GRUB2では設定ファイルを直接編集せず、以下のコマンドで更新する：

**Debian/Ubuntu系**
```bash
sudo update-grub
```

**Red Hat/CentOS/Fedora系**
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

**UEFI環境の場合**
```bash
sudo grub2-mkconfig -o /boot/efi/EFI/[distribution]/grub.cfg
```

## インストール場所

### BIOS環境
- `/boot/grub/` - 設定ファイルとモジュール
- [[MBR]]のboot sector - 第1ステージ
- `/boot/grub/core.img` - 第2ステージ

### UEFI環境
- `/boot/efi/EFI/[distribution]/` - GRUB2のEFIアプリケーション
- `/boot/grub/` - 設定ファイルとモジュール

## トラブルシューティング

**GRUB Rescue モード**
GRUBが正常に起動できない場合に表示される最小限の環境。基本的なコマンドでシステムの修復が可能。

**よくある問題**
- 設定ファイルの破損
- パーティション構造の変更
- カーネルファイルの移動や削除
- ファイルシステムの破損

**修復コマンド例**
```bash
# モジュールの読み込み
insmod ext2
insmod linux

# ルートパーティションの設定
set root=(hd0,1)

# カーネルの手動起動
linux /vmlinuz root=/dev/sda1
initrd /initrd.img
boot
```

## まとめ

GRUB2は、GRUB Legacyから大幅に機能が拡張され、現代のハードウェアとファームウェア環境に対応した強力なブートローダーとなっている。モジュラー設計により柔軟性が向上し、複雑なブート環境でも安定した動作を提供する。設定の自動生成機能により、手動での設定ミスを減らしつつ、高度なカスタマイズも可能となっている。