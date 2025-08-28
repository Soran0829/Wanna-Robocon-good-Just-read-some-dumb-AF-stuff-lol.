# ローカルファイルをリモートリポジトリにアップロードする手順

GitHubなどのリモートリポジトリにローカルファイルをアップロードし、作業用ブランチを作成する手順をまとめています。

---

## 1. リモートリポジトリの準備

1. GitHubで新しいリポジトリを作成します。
    - [新規作成ページ](https://github.com/new) から作成可能です。
2. リポジトリのURL（例: `https://github.com/ユーザー名/リポジトリ名.git`）を控えておきます。

---

## 2. ローカルリポジトリの初期化

```bash
# 作業ディレクトリへ移動
cd /path/to/your/project

# Git初期化（.gitフォルダが無い場合のみ）
git init
```

---

## 3. リモートリポジトリを登録

```bash
git remote add origin https://github.com/ユーザー名/リポジトリ名.git
```

---

## 4. 作業用ブランチの作成
必須というわけではないが、「誰が」「なんのために」pushしたものかを明確にしたいときに使いたい
| 名前     |  意味      |
|----------|-----------|
| 〇〇-dev| 開発用ブランチ。未完成の作業や、テスト、検証ようのブランチ   |
| main,master |  完成、検証が完了したプロジェクトをいれるような場所  |

```bash
# 例：feature/add-file という名前でブランチを作成
git checkout -b feature/add-file
```

---

## 5. ファイル追加＆コミット

```bash
# ファイルを追加
git add ファイル名

# まとめて追加したい場合は
git add .

# コミット
git commit -m "add ファイルの説明"
```

---

## 6. リモートリポジトリにプッシュ

```bash
git push -u origin feature/add-file
```

---

## 7. GitHub上でプルリクエストを作成

- GitHubリポジトリページにアクセスし、"Compare & pull request"ボタンからPR（プルリクエスト）を作成します。

---

## 手順まとめ

1. GitHubでリポジトリを作成  
2. `git init`でローカルリポジトリを初期化  
3. `git remote add origin`でリモートリポジトリを登録  
4. `git checkout -b ブランチ名`で新しいブランチを作成  
5. `git add`と`git commit`でファイルを追加・コミット  
6. `git push -u origin ブランチ名`でリモートにプッシュ  
7. GitHub上でプルリクエストを作成

---
