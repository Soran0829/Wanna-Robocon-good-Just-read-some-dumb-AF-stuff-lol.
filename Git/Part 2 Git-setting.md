# ユーザー設定（認証項目なし）

Git の基本ユーザー設定（user.name / user.email / 既定ブランチ名 main）のみをまとめます。認証（HTTPS/SSH・鍵）に関する内容は含みません。

---

## 1. 基本ユーザー情報の設定

あなたが行ったコミットに記録される名前とメールアドレスを設定します。この設定は、Gitを使い始める際に一度だけ行えば問題ありません。

```bash
# あなたの名前を設定します（GitHubのユーザー名がおすすめです）
git config --global user.name "Your Name"

# あなたのメールアドレスを設定します（GitHubに登録しているアドレスがおすすめです）
git config --global user.email "you@example.com"
```

> **Note:**
> `--global` オプションは、PC上の全てのGitリポジトリに適用される共通設定です。特定のプロジェクトだけ違う設定にしたい場合は、そのリポジトリのフォルダ内で `--global` を付けずにコマンドを実行します。

### 設定の確認
正しく設定されたかを確認します。
```bash
git config --global user.name
git config --global user.email
```

すべての設定と設定ファイルの場所を確認:
```bash
git config --list --show-origin
```

メモ
- --global はユーザー単位。特定リポジトリだけ変更したい場合は、そのリポジトリ内で --local を使用（--local は省略可）。
- 会社と個人でメールを使い分けたい場合は includeIf を使うと便利（上級）:
  ```ini
  # ~/.gitconfig
  [includeIf "gitdir:~/work/company/"]
      path = ~/.gitconfig-company
  ```
  ```ini
  # ~/.gitconfig-company
  [user]
      email = your.corporate@example.com
      name  = Your Corp Name
  ```

---

## 2. 既定ブランチ名を main に設定

新規リポジトリ作成時の既定ブランチ名を main にします。以前は `master` が一般的でしたが、現在では `main` が推奨されています。

```bash
git config --global init.defaultBranch main
```

### (補足) 既存リポジトリのブランチ名を変更する場合
もし `master` という名前のブランチを `main` に変更したい場合は、以下のコマンドを実行します。
```bash
# 現在のブランチ名を 'main' に変更
git branch -m master main
```
リモートリポジトリのデフォルトブランチは、GitHubなどのWebサイト上で変更する必要があります。

---

## 3. 動作確認（任意）

最低限の確認を一時ディレクトリで行います。

```bash
mkdir git-config-check && cd git-config-check
git init
echo "hello" > readme.txt
git add readme.txt
git commit -m "test: initial commit"
git log --oneline
```

設定値の確認:
```bash
git config --global --get user.name
git config --global --get user.email
git config --global --get init.defaultBranch
```

---

## 4. よくあるつまずき

- コミット作者が Unknown/不正
  - user.name / user.email が未設定または誤設定。--global か --local で正しい値を設定。
- 新規作成時に main ではなく master ができる
  - `git config --global init.defaultBranch main` を設定後、改めて `git init` する。
- グローバル設定を変えたのに反映されない
  - リポジトリのローカル設定が優先されている可能性。`git config --list --show-origin` で設定の出所を確認する。