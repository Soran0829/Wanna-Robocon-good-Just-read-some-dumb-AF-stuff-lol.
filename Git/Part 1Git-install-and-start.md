# 環境準備（必須）
Git の教育・演習を始める前に必要な「Git のインストール（Windows/Mac/Linux）」と「CLI/GUI ツールの選択肢（Git GUI, GitHub Desktop, IDE 統合）」をまとめます。

---

## 1. Git のインストール

### 1.1 共通（確認手順）
- インストール確認
  ```bash
  git --version
  ```
- うまく動かない場合は、再起動やシェルの再起動（新しいターミナルを開く）を試してください。

---

### 1.2 Windows
最も簡単：Git for Windows（Git Bash 同梱）

- ダウンロード: https://git-scm.com/download/win
- パッケージマネージャ
  - winget:
    ```powershell
    winget install --id Git.Git -e --source winget
    ```
  - Chocolatey:
    ```powershell
    choco install git -y
    ```

推奨インストーラー設定（対話インストール時）
- Default editor: お好み（VS Code 推奨）
- Adjust PATH: Git from the command line
- HTTPS transport backend: OpenSSL
- Line endings: Checkout Windows-style, commit Unix-style (core.autocrlf=true)
- Use Git Credential Manager: 有効（推奨）
- Default branch for new repos: main

起動方法
- Git Bash（同梱）または Windows Terminal（PowerShell）から `git` を実行

---

### 1.3 macOS
方法 A: Xcode Command Line Tools（最小構成）
```bash
xcode-select --install
```

方法 B: Homebrew（最新版を使いたい場合）
```bash
# Homebrew 未導入なら https://brew.sh/ を参照
brew install git
```

確認
```bash
git --version
```

---

### 1.4 Linux
ディストリビューション別
- Debian/Ubuntu
  ```bash
  sudo apt-get update
  sudo apt-get install -y git
  ```
- Fedora/RHEL/CentOS
  ```bash
  sudo dnf install -y git
  ```
- Arch Linux
  ```bash
  sudo pacman -S git
  ```

確認
```bash
git --version
```

---

## 2. CLI と GUI ツールの選択肢

### 2.1 CLI（コマンドライン）
- 特徴
  - すべての機能にアクセス可能、学習コストはあるが再現性・自動化に強い
  - ドキュメントや Q&A 情報が豊富で、トラブルシュートしやすい
- 代表的なシェル
  - Windows: Git Bash、PowerShell、Windows Terminal
  - macOS: Terminal、iTerm2 + zsh
  - Linux: bash/zsh など
- 基本コマンド例
  ```bash
  git status
  git add <file>
  git commit -m "message"
  git log --oneline --graph --decorate
  git push
  ```

### 2.2 Git GUI（同梱ツール）
- 起動
  ```bash
  git gui
  gitk      # 履歴閲覧ツール
  ```
- 特徴
  - 追加インストール不要。ステージ/コミットや簡単な履歴確認に便利
  - 見た目はシンプル。高度なレビューや PR 連携は別ツールが必要

### 2.3 GitHub Desktop
- ダウンロード: https://desktop.github.com/
- 特徴
  - GitHub と密接に連携。クローン、ブランチ、コミット、PR 作成が簡単
  - 差分表示が見やすい。初心者や GUI 派にとても扱いやすい
- 向いている用途
  - 個人/小規模チーム、レビュー前のローカル作業、PR の起点に

### 2.4 IDE 統合
- Visual Studio Code
  - 標準で Git 連携（ソース管理ビュー、差分、部分ステージ、拡張機能が豊富）
  - 拡張: GitHub Pull Requests and Issues、GitLens など
  - 注意: Git 本体は別途インストールが必要
- JetBrains IDE（IntelliJ IDEA / PyCharm / WebStorm など）
  - GUI でほぼ一通り操作（チェリーピック、インタラクティブリベース等）
  - VCS 設定で Git 実行ファイルパスを確認
- Visual Studio（.NET）
  - Team Explorer / Git ツール内蔵、GitHub 連携も容易
- Xcode（iOS/macOS）
  - 基本的な Git 操作に対応（Source Control メニュー）

---

## 3. 使い分けのガイド
- 初学者
  - GitHub Desktop または IDE の Git 機能で操作感を掴む
  - 並行して CLI の基本（status/add/commit/push）を習得
- 中級者以上
  - 日常は CLI 中心＋IDE の差分表示
  - 複雑な履歴整形（rebase、bisect 等）は CLI 推奨
- チーム運用
  - レビューや PR は GitHub（Web/CLI/IDE 拡張）で統一
  - GUI と CLI を併用し、共通のコマンド/画面を教材にする

---

## 4. インストール後の動作確認（任意）
最低限のチェック（個人用の一時ディレクトリで）
```bash
mkdir git-check && cd git-check
git init
echo "hello" > readme.txt
git add readme.txt
git commit -m "test: initial commit"
git log --oneline
```

以上で、インストールとツール選定の最小セットは完了です。次のステップとして、ユーザー名/メール設定や既定ブランチ名（main）の設定、認証（HTTPS/SSH）などを進めてください。
