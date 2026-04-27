yuumanoza-tan-guang-chang-634719150434156546
# finalize

[https://3ds.hacks.guide/finalizing-setup](https://3ds.hacks.guide/finalizing-setup) （セットアップの仕上げ）に関連するスクリプト群です。

## ディレクトリ構成
- **`/romfs/finalize/`**: `finalize.romfs` にパッキングされるファイル群
    - **`/romfs/finalize/img`**: トラブルシューティング用の参照画像
    - **`/romfs/finalize/finalize.gm9`**: `finalize_helper.gm9` の後に実行されるスクリプト。以下の処理を行います：
        - 基本的な自作ソフト（Homebrew）をSYSNAND SDにインストール
        - GodMode9をCTRNAND (`/rw/luma/payloads`) にコピー
        - `essential.exefs` を `/gm9/backups` にバックアップ
        - 不要になったCFWインストール用ファイルを削除
        - 最小サイズのNANDバックアップを `/gm9/backups` に作成
    - **`/romfs/finalize/donor.db`**: タイトルデータベースがない本体（eショップ未利用など）向けの空のデータベース
- **`finalize_helper.gm9`**: GM9スクリプトランナー (`finalize_helper.firm`) としてビルドされる、`finalize.romfs` 展開用スクリプト
- **`docs.md`**: エラー詳細およびスクリプトのドキュメント

## 同梱ソフトウェア
以下のリポジトリのコンパイル済みバイナリが含まれています：
- FBI / Homebrew Launcher Loader / Anemone3DS / Checkpoint / ftpd / Universal-Updater / GodMode9 (GM9Megascript含む)

## リリースと使用方法
**本リポジトリのリリースは一般利用を目的としていません。** 利用する場合は以下のいずれかの方法で行います。

### A. 自動ビルド済みバイナリを使用する場合
[GitHub Actions](https://github.com/hacks-guide/finalize/actions/) でビルドされたものを使用します。
1. `finalize_helper.firm` を `/luma/payloads/` に配置
2. `finalize.romfs` をSDカードのルートに配置

### B. 手動でファイルを配置する場合
1. リポジトリをクローンする
2. `romfs/finalize` フォルダの中身をSDカードのルートにコピー
3. `finalize.gm9` を `/gm9/scripts/` にコピー
4. `GodMode9.firm` を `/luma/payloads/` にコピー
   - ※Lumaの `boot.firm` がSDカードのルートにある必要があります。

## ビルド方法
以下のツール一式が必要です：
- **3dstool**
- **devkitARM** (3DS関連パッケージを含む)

### 手順
```bash
# リポジトリのクローン
git clone [https://github.com/hacks-guide/finalize](https://github.com/hacks-guide/finalize) --recurse-submodules
cd finalize

# ビルドの実行
make
