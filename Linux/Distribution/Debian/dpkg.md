# dpkg

[[Debian]]系[[Linux]]ディストリビューションで使用されるパッケージ管理システムの低レベルツール。パッケージのインストール、削除、情報表示などの基本的な操作を行う。

## 主要機能

dpkgは以下の機能を提供する：
- .debパッケージファイルのインストールと削除
- インストール済みパッケージの情報表示
- パッケージの状態管理
- パッケージの依存関係チェック（基本的なもの）

## 基本コマンド

### パッケージのインストール
```bash
sudo dpkg -i package.deb
```

### パッケージの削除
```bash
sudo dpkg -r package_name
```

### 完全削除（設定ファイルも含む）
```bash
sudo dpkg -P package_name
```

### インストール済みパッケージの一覧表示
```bash
dpkg -l
dpkg -l | grep pattern
```

### パッケージ情報の表示
```bash
dpkg -s package_name
```

### パッケージの内容確認
```bash
dpkg -L package_name
```

### ファイルの所属パッケージ確認
```bash
dpkg -S /path/to/file
```

## 主要オプション

| オプション | 説明 |
|------------|------|
| `-i` | パッケージをインストール |
| `-r` | パッケージを削除（設定ファイルは残す） |
| `-P` | パッケージを完全削除 |
| `-l` | インストール済みパッケージ一覧 |
| `-s` | パッケージ状態の表示 |
| `-L` | パッケージに含まれるファイル一覧 |
| `-S` | ファイルの所属パッケージ検索 |
| `--configure` | パッケージの設定を完了 |
| `--force-depends` | 依存関係を無視して実行 |

## パッケージ状態

dpkgは各パッケージの状態を以下のように管理する：

- **ii**: インストール済み、正常に設定済み
- **rc**: パッケージは削除済みだが設定ファイルが残存
- **iU**: インストール済みだが未設定
- **pn**: パッケージ未インストール

## トラブルシューティング

### 破損したパッケージの修復
```bash
sudo dpkg --configure -a
```

### 依存関係の問題解決
```bash
sudo apt-get install -f
```

### パッケージデータベースの再構築
```bash
sudo dpkg --audit
```

### パッケージの再設定（dpkg-reconfigure）
`dpkg-reconfigure`は、インストール済みパッケージの設定を再実行するためのツール。パッケージのインストール時に行われた設定プロセスを再度実行できる。

#### 基本的な使用方法
```bash
sudo dpkg-reconfigure package_name
```

#### よく使用される例
```bash
# タイムゾーンの再設定
sudo dpkg-reconfigure tzdata

# キーボードレイアウトの再設定
sudo dpkg-reconfigure keyboard-configuration

# ロケールの再設定
sudo dpkg-reconfigure locales

# 低レベルインターフェースで設定
sudo dpkg-reconfigure -p low package_name

# 設定の優先度を指定
sudo dpkg-reconfigure -p critical package_name
```

#### 優先度レベル
- **low**: すべての設定項目を表示
- **medium**: 通常の設定項目のみ表示（デフォルト）
- **high**: 重要な設定項目のみ表示
- **critical**: 極めて重要な設定項目のみ表示

#### 主要オプション
| オプション | 説明 |
|------------|------|
| `-p priority` | 設定の優先度を指定 |
| `-f frontend` | フロントエンド（dialog, readline, noninteractive等）を指定 |
| `--force` | 既に設定済みでも強制的に再設定 |
| `--default-priority` | デフォルト優先度を使用 |

## dpkg設定ファイル

dpkgは複数の設定ファイルを使用してパッケージ管理の動作を制御する。

### 主要な設定ファイル

#### /var/lib/dpkg/status
- インストール済みパッケージの状態を記録するデータベースファイル
- 各パッケージの詳細情報、依存関係、設定状態を保存
- dpkgの中核となるファイルで、破損するとシステムに重大な影響

#### /var/lib/dpkg/available
- 利用可能なパッケージの情報を格納
- `apt-cache`コマンドなどで更新される
- パッケージの説明、依存関係、バージョン情報を含む

#### /etc/dpkg/dpkg.cfg
- dpkgのグローバル設定ファイル
- システム全体のデフォルト動作を定義

```bash
# 例：設定の強制実行
force-confold
```

#### /etc/dpkg/dpkg.cfg.d/
- 追加の設定ファイルを配置するディレクトリ
- ファイル名の辞書順で読み込まれる

#### ~/.dpkg.cfg
- ユーザー固有のdpkg設定ファイル
- ホームディレクトリに配置

### 設定オプション

#### 主要な設定項目
```bash
# 設定ファイルの競合時に既存ファイルを保持
force-confold

# 設定ファイルの競合時に新しいファイルを使用
force-confnew

# 依存関係エラーを無視
force-depends

# アーキテクチャの不一致を無視
force-architecture

# パッケージ削除時に依存関係チェックを無視
force-remove-essential
```

### confファイルの管理

dpkgは設定ファイル（confファイル）を特別に管理する：

#### confファイルの状態
- **not-modified**: 変更されていない
- **modified**: ユーザーが変更
- **replaced**: パッケージ更新で置換

#### 競合時の選択肢
```bash
# パッケージ更新時の設定ファイル競合
Configuration file '/etc/example.conf'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
    D       : show the differences between the versions
    Z       : start a shell to examine the situation
```

### データベースファイルの場所

#### 主要なディレクトリ
- `/var/lib/dpkg/` - dpkgデータベース
- `/var/lib/dpkg/info/` - パッケージの制御スクリプト
- `/var/lib/dpkg/updates/` - 更新中の一時ファイル
- `/var/backups/` - statusファイルのバックアップ

#### バックアップと復旧
```bash
# statusファイルのバックアップ作成
sudo cp /var/lib/dpkg/status /var/lib/dpkg/status.backup

# バックアップからの復旧
sudo cp /var/backups/dpkg.status.0 /var/lib/dpkg/status
```

## aptとの関係

dpkgは低レベルなパッケージ管理ツールであり、[[apt]]はdpkgの上位レイヤーとして動作する。aptは以下の機能を提供：
- 依存関係の自動解決
- パッケージリポジトリからのダウンロード
- アップグレード管理

通常の運用では、aptを使用することが推奨される。dpkgは個別の.debファイルの操作や、詳細な情報取得に使用する。

## 注意点

- dpkgは依存関係を自動解決しないため、手動でのパッケージ管理には注意が必要
- 強制オプション（--force系）の使用は慎重に行う
- システムの重要なパッケージを削除する際は十分な検証が必要