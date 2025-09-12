# Part 1: Gitのインストールと環境準備

Gitの学習を始める前に、お使いの環境（Windows/Mac/Linux）にGitをインストールし、操作ツール（CLI/GUI）を選択する方法を解説します。

---

## 1. Gitのインストール

### 1.1. インストール確認
まず、Gitがすでにインストールされていないか確認します。ターミナル（コマンドプロンプト）で以下のコマンドを実行してください。

```bash
git --version
```
バージョン情報（例: `git version 2.45.1.windows.1`）が表示されればインストール済みです。表示されない場合や、エラーになる場合はOSごとに以下の手順でインストールしてください。

> **Note:** インストール後にコマンドが認識されない場合は、PCまたはターミナルを再起動すると解決することがあります。

---

### 1.2. Windows

**推奨:** **Git for Windows** を利用します。Git本体に加え、コマンドラインツール「Git Bash」も同梱されています。

- **インストーラー:** [公式サイト](https://git-scm.com/download/win)からダウンロードして実行します。
- **パッケージマネージャー (任意):**
  - **winget:**
    ```powershell
    winget install --id Git.Git -e --source winget
    ```
  - **Chocolatey:**
    ```powershell
    choco install git -y
    ```

#### 推奨インストーラー設定
対話形式のインストーラーでは、以下の設定を推奨します。
- **Default editor:** `Visual Studio Code` など、普段使うエディタを選択
- **Adjusting your PATH environment:** `Git from the command line and also from 3rd-party software` を選択
- **HTTPS transport backend:** `Use the OpenSSL library` を選択
- **Configuring the line ending conversions:** `Checkout Windows-style, commit Unix-style line endings` を選択
- **Default branch name for new repositories:** `main` を選択

---

### 1.3. macOS

**方法A (推奨):** Xcode Command Line Tools に含まれるGitを利用します。
```bash
xcode-select --install
```

**方法B:** 最新版を利用したい場合は、パッケージマネージャー [Homebrew](https://brew.sh/index_ja) を使ってインストールします。
```bash
brew install git
```

---

### 1.4. Linux

お使いのディストリビューションに合わせて、パッケージマネージャーでインストールします。

- **Debian/Ubuntu:**
  ```bash
  sudo apt-get update
  sudo apt-get install -y git
  ```
- **Fedora/RHEL/CentOS:**
  ```bash
  sudo dnf install -y git
  ```
- **Arch Linux:**
  ```bash
  sudo pacman -S git
  ```

---

## 2. 操作ツール（CLI / GUI）の選択

Gitの操作には、コマンドで操作するCLIと、グラフィカルな画面で操作するGUIの2種類があります。

### 2.1. CLI (コマンドラインインターフェース)
ターミナル上でコマンドを直接入力してGitを操作する方法です。
- **特徴:** 全てのGit機能にアクセス可能。慣れると高速かつ自動化にも応用できるため、最も強力な方法です。
- **代表的なコマンド:**
  ```bash
  git status      # 状態の確認
  git add <file>  # ファイルをステージング
  git commit -m "変更内容のメッセージ" # コミット
  git push        # リモートリポジトリに送信
  ```

### 2.2. GUI (グラフィカルユーザーインターフェース)
マウス操作で直感的にGitを扱えるツールです。

- **GitHub Desktop:**
  - **特徴:** GitHubとの連携がスムーズで、初心者でも扱いやすいシンプルなUIが魅力です。差分（変更箇所）の確認も簡単です。
  - **ダウンロード:** https://desktop.github.com/

- **IDE統合機能:**
  - **特徴:** Visual Studio CodeやJetBrains製IDE（IntelliJ, PyCharm等）には、標準でGit操作機能が組み込まれています。コーディングからバージョン管理までを一つの画面で完結できます。
  - **注意:** IDEの機能を使う場合でも、Git本体のインストールは別途必要です。

---

## 3. 使い分けのガイド

- **初心者:** まずは **GitHub Desktop** や **IDEのGUI機能** で、クローン・コミット・プッシュといった基本的な流れを視覚的に掴むのがおすすめです。同時に、`git status` や `git add` などの基本的なCLIコマンドにも触れておくと、後々の学習がスムーズになります。
- **中級者以上:** 日常的なコミットやブランチ操作は **CLI** を中心に行い、差分確認やコンフリクト解消などでは **IDEのGUI機能** を補助的に使うと効率的です。
- **チーム開発:** レビューやプルリクエストの管理は **GitHub** のWebサイト上で行うのが基本です。操作方法はCLI/GUIどちらでも問題ありませんが、チーム内で用語や概念（ブランチ、マージなど）の認識を揃えておくことが重要です。

---

## 4. インストール後の動作確認
最後に、Gitが正しく動作するか簡単なテストを行いましょう。

```bash
# 1. テスト用のフォルダを作成して移動
mkdir git-test && cd git-test

# 2. Gitリポジトリを初期化
git init

# 3. テスト用のファイルを作成
echo "hello git" > readme.md

# 4. ファイルをステージング
git add readme.md

# 5. ファイルをコミット
git commit -m "Initial commit"

# 6. コミット履歴を確認
git log --oneline
```
`Initial commit` という履歴が表示されれば、環境準備は完了です。
次のPartでは、Gitを使う上で必須となるユーザー情報の設定や、SSHキーの生成・登録について解説します。
