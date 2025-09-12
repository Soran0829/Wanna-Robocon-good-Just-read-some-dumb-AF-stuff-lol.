# Part 2: プログラミング環境の導入

ロボットの制御プログラムを開発するために、お使いのWindows PCにプログラミング環境を構築します。ここでは、2つの主要な方法を紹介します。

1.  **WSL (Windows Subsystem for Linux) を利用する方法 (推奨)**
    - Windows上でLinux環境を動かし、そこで開発を行います。ロボコンでよく使われるROSなどのツールとの親和性が高く、チーム内の環境を統一しやすいメリットがあります。

2.  **Windowsネイティブ環境を構築する方法**
    - WSLを使わず、Windowsに直接コンパイラ等をインストールします。シンプルな構成ですが、Linuxでしか動作しないツールは使えません。

---

## 方法1: WSL (Windows Subsystem for Linux) を利用する (推奨)

### Step 1: WSLのインストール

1.  **PowerShellを管理者として開く**
    - スタートメニューで「PowerShell」と検索し、右クリックして「管理者として実行」を選択します。

2.  **WSLインストールコマンドの実行**
    - 開いたPowerShellで以下のコマンドを実行します。これにより、WSLと標準のLinuxディストリビューションである「Ubuntu」がインストールされます。
    ```powershell
    wsl --install
    ```

3.  **PCの再起動と初期設定**
    - インストールが完了したらPCを再起動します。
    - 再起動後、Ubuntuのターミナルが自動的に開き、ユーザー名とパスワードの設定を求められます。これらはLinux環境内でのみ使用するものですので、自由に設定してください。

### Step 2: VS CodeとWSLの連携

1.  **Visual Studio Code (VS Code) のインストール**
    - まだインストールしていない場合は、[公式サイト](https://code.visualstudio.com/)からダウンロードしてインストールします。

2.  **WSL拡張機能のインストール**
    - VS Codeを起動し、左側の拡張機能アイコンをクリックします。
    - 検索バーに `WSL` と入力し、Microsoft提供の「WSL」拡張機能をインストールします。

3.  **WSL環境でVS Codeを開く**
    - Ubuntuのターミナル（スタートメニューから「Ubuntu」で検索して起動できます）で、作業したいディレクトリに移動し、以下のコマンドを実行します。
    ```bash
    # 例: ホームディレクトリに 'project' フォルダを作成して移動
    mkdir ~/project
    cd ~/project
    
    # カレントディレクトリをVS Codeで開く
    code .
    ```
    - これで、VS CodeがWSLに接続された状態で起動します。ウィンドウの左下に「WSL: Ubuntu」と表示されていれば成功です。

### Step 3: 開発ツールのインストール (WSL内)

VS Codeのターミナル（`Ctrl + @`で開けます）で、以下のコマンドを実行してC/C++/Pythonの開発ツールをインストールします。

1.  **C/C++ (GCC, G++)**
    ```bash
    # パッケージリストを更新
    sudo apt update
    
    # C/C++コンパイラとデバッガをインストール
    sudo apt install build-essential gdb
    ```
    - VS Codeの拡張機能タブで「C/C++」を検索し、WSL側にインストールします。

2.  **Python**
    - Ubuntuには通常Python3がプリインストールされています。`pip`（パッケージ管理ツール）をインストールします。
    ```bash
    sudo apt install python3-pip
    ```
    - VS Codeの拡張機能タブで「Python」を検索し、WSL側にインストールします。

### Step 4: コードの実行

- **C++の例 (`hello.cpp`)**
    ```cpp
    #include <iostream>
    
    int main() {
        std::cout << "Hello from WSL!" << std::endl;
        return 0;
    }
    ```
    **コンパイルと実行:**
    ```bash
    g++ hello.cpp -o hello
    ./hello
    ```

- **Pythonの例 (`hello.py`)**
    ```python
    print("Hello from WSL!")
    ```
    **実行:**
    ```bash
    python3 hello.py
    ```

---

## 方法2: Windowsネイティブ環境を構築する (WSLなし)

### Step 1: C/C++コンパイラのインストール (MinGW-w64)

1.  **MinGW-w64のダウンロード**
    - [winlibs.com](https://winlibs.com/) にアクセスします。
    - 最新バージョンの「UCRT runtime」セクションにある「Win64」向けの「ZIP archive」をダウンロードします。

2.  **ファイルの展開**
    - ダウンロードしたZIPファイルを、`C:\` ドライブ直下など、分かりやすい場所に展開（解凍）します。
    - 展開後のフォルダ名が `mingw64` となるように配置します。（例: `C:\mingw64`）

3.  **環境変数Pathの設定**
    - Windowsがコンパイラを見つけられるようにPathを設定します。
    - `C:\mingw64\bin` というパスをコピーします。（展開先によってパスは異なります）
    - Windowsの「設定」→「システム」→「詳細情報」→「システムの詳細設定」→「環境変数」を開きます。
    - 「システム環境変数」の `Path` を選択し、「編集」→「新規」でコピーしたパスを貼り付け、OKを押して閉じます。

4.  **インストールの確認**
    - コマンドプロンプトまたはPowerShellを**新しく開き**、以下を実行してバージョン情報が表示されれば成功です。
    ```bash
    g++ --version
    ```

### Step 2: Pythonのインストール

1.  [Python公式サイト](https://www.python.org/downloads/windows/)からインストーラーをダウンロードして実行します。
2.  **重要:** インストーラーの最初の画面で **「Add python.exe to PATH」** のチェックボックスを必ずオンにしてください。

### Step 3: VS Codeの設定と実行

1.  **VS Codeのインストール**
    - [公式サイト](https://code.visualstudio.com/)からダウンロードしてインストールします。

2.  **拡張機能のインストール**
    - VS Codeの拡張機能タブで「C/C++」と「Python」を検索し、インストールします。

3.  **コードの実行**
    - VS Codeでファイル（例: `hello.cpp` や `hello.py`）を開き、ターミナル（`Ctrl + @`）で以下のコマンドを実行します。

- **C++の例**
    ```bash
    g++ hello.cpp -o hello.exe
    ./hello.exe
    ```

- **Pythonの例**
    ```bash
    python hello.py
    ```