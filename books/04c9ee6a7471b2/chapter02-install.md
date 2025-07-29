---
title: "第2章: Windows環境でのNode.jsインストール"
---

# インストール方法の選択

この章では、Windows環境でNode.jsをインストールする具体的な方法を学習します。複数のインストール方法があるため、それぞれのメリット・デメリットを理解した上で、自分の状況に最適な方法を選択しましょう。

## インストール方法の比較

Windows環境でNode.jsをインストールする方法は主に3つあります：

### 方法1: 公式インストーラー（初心者推奨）

**特徴**：
- 最もシンプルで分かりやすい
- 1つのバージョンのみインストール
- 自動でPATH設定を行う

#### 用語解説：PATH（パス）
**PATH**とは、コンピューターが実行可能なプログラムを探すディレクトリ（フォルダ）の一覧です。PATHに追加されることで、どこからでもNode.jsコマンドを実行できるようになります。

**メリット**：
- 簡単で確実にインストールできる
- 初心者でも迷わない
- 公式サポートが充実

**デメリット**：
- 複数バージョンの管理ができない
- バージョン切り替えが困難

**適用場面**：
- プログラミング学習開始時
- 単一プロジェクトでの開発
- 最新版のみを使用する場合

### 方法2: nvm-windows（開発者推奨）

**特徴**：
- 複数バージョンの管理が可能
- プロジェクトごとにバージョンを切り替え
- 開発現場でよく使われる

#### 用語解説：nvm（Node Version Manager）
**nvm**は、複数のNode.jsバージョンをインストールし、必要に応じて切り替えることができるツールです。**nvm-windows**は、Windows専用のnvm実装です。

**メリット**：
- 複数バージョンの同時管理
- 簡単なバージョン切り替え
- プロジェクトごとの環境管理

**デメリット**：
- 初期設定がやや複雑
- PowerShellの知識が必要

**適用場面**：
- 複数プロジェクトでの開発
- チーム開発
- 長期的な開発を見据えた場合

### 方法3: パッケージマネージャー（効率重視）

**特徴**：
- Chocolatey、wingetなどを使用
- コマンドラインでのインストール
- システム全体のパッケージ管理

#### 用語解説：パッケージマネージャー
**パッケージマネージャー**とは、ソフトウェアのインストール、アップデート、削除を自動化するツールです。LinuxやmacOSでは標準的ですが、Windowsでも最近利用が増えています。

**メリット**：
- コマンドラインで効率的な管理
- 自動アップデート機能
- システム全体の一元管理

**デメリット**：
- パッケージマネージャーの事前インストールが必要
- トラブル時の対処が複雑

**適用場面**：
- 開発ツールを多数使用する場合
- 自動化を重視する場合
- システム管理の経験がある場合

## 推奨インストール方法の決定

**あなたの状況に応じた推奨方法**：

```mermaid
graph TD
    A[Node.js学習開始] --> B{プログラミング経験}
    B -->|初心者| C[公式インストーラー]
    B -->|1年未満| D{将来の予定}
    B -->|1年以上| E[nvm-windows]
    
    D -->|学習のみ| C
    D -->|実務予定| E
    
    C --> F[方法1: 公式インストーラー]
    E --> G[方法2: nvm-windows]
    
    classDef recommendClass fill:#c8e6c9
    classDef methodClass fill:#ffecb3
    
    class C,E recommendClass
    class F,G methodClass
```

**決定フローチャート**：
1. **プログラミング完全初心者** → 公式インストーラー
2. **複数プロジェクト予定** → nvm-windows
3. **チーム開発参加予定** → nvm-windows
4. **学習のみ・単発利用** → 公式インストーラー

## 方法1: 公式インストーラーによるインストール

### 事前準備

1. **システム要件の確認**
   - Windows 10 以降（推奨）
   - 管理者権限のアカウント
   - 安定したインターネット接続

2. **既存インストールの確認**
```powershell
# PowerShellで確認
node --version
npm --version
```

既にインストールされている場合は、「プログラムと機能」から削除してください。

### LTS版と最新版の選択

Node.jsには2つのリリースタイプがあります：

#### 用語解説：LTS（Long Term Support）
**LTS**は「長期サポート」の意味で、安定性と信頼性を重視したバージョンです。企業や本格的な開発では通常LTS版を選択します。

**LTS版（推奨）**：
- 安定性が高い
- 長期間サポートされる
- バグ修正とセキュリティアップデートが継続
- 現在のLTS版：v22.x.x

**最新版（Current）**：
- 最新機能を含む
- 実験的な機能も含まれる場合がある
- サポート期間が短い
- 現在の最新版：v23.x.x

**選択指針**：
- **学習・実務**：LTS版を選択
- **最新機能検証**：最新版を選択

### インストール手順（詳細）

#### Step 1: 公式サイトからダウンロード

1. **ブラウザでNode.js公式サイトにアクセス**
   ```
   https://nodejs.org/
   ```

2. **LTS版のダウンロードボタンをクリック**
   - 緑色の「LTS」ボタンをクリック
   - 自動的にWindows用インストーラーがダウンロード開始

3. **ダウンロード完了の確認**
   - ファイル名：`node-v22.x.x-x64.msi`（バージョンにより異なる）
   - ファイルサイズ：約30-50MB

#### Step 2: インストーラーの実行

1. **ダウンロードしたファイルを実行**
   - ダウンロードフォルダでファイルをダブルクリック
   - セキュリティ警告が表示された場合は「実行」をクリック

2. **インストールウィザードに従って進行**

   **Welcome画面**：
   - 「Next」をクリック

   **License Agreement**：
   - ライセンス条項を確認
   - 「I accept the terms in the License Agreement」にチェック
   - 「Next」をクリック

   **Destination Folder**：
   - インストール先フォルダの選択
   - 通常はデフォルト（`C:\Program Files\nodejs\`）のまま
   - 「Next」をクリック

   **Custom Setup**：
   - インストールする機能の選択
   - 全て**デフォルトのまま**にすることを推奨
   - 「Next」をクリック

   **Tools for Native Modules**：
   - 追加ツールのインストール選択
   - 初心者は**チェックを外したまま**推奨
   - 「Next」をクリック

#### 用語解説：ネイティブモジュール
**ネイティブモジュール**とは、C++で書かれたNode.jsモジュールのことです。高速な処理が必要な場合に使用されますが、初心者の段階では使用する機会は少ないです。

   **Ready to Install**：
   - 設定内容の最終確認
   - 「Install」をクリック
   - インストール開始（数分程度）

   **Installation Complete**：
   - 「Finish」をクリックしてインストール完了

#### Step 3: インストール確認

1. **PowerShellを管理者として起動**
   ```
   Windows + R → 「powershell」入力 → Ctrl + Shift + Enter
   ```

2. **バージョン確認**
   ```powershell
   node --version
   # 出力例：v22.11.0
   
   npm --version
   # 出力例：10.2.4
   ```

3. **簡単な動作テスト**
   ```powershell
   node -e "console.log('Node.js installation successful!')"
   # 出力：Node.js installation successful!
   ```

### インストール後の環境設定

#### PATH環境変数の確認

インストーラーが自動的にPATH設定を行いますが、確認方法を覚えておきましょう：

1. **システムのプロパティを開く**
   ```
   Windows + R → 「sysdm.cpl」入力 → Enter
   ```

2. **環境変数の確認**
   - 「詳細設定」タブ
   - 「環境変数」ボタンをクリック
   - 「システム環境変数」の「Path」を選択
   - 「編集」ボタンをクリック

3. **Node.jsのパスが追加されていることを確認**
   ```
   C:\Program Files\nodejs\
   ```

#### npm初期設定

```powershell
# npm設定の確認
npm config list

# グローバルインストール先の確認
npm config get prefix

# レジストリ（パッケージ取得先）の確認
npm config get registry
# 出力：https://registry.npmjs.org/
```

#### 用語解説：レジストリ
**レジストリ**とは、npmパッケージが保存されている場所のことです。デフォルトでは公式のnpmレジストリ（https://registry.npmjs.org/）が設定されています。

## 方法2: nvm-windowsによるバージョン管理

### nvm-windowsとは

**nvm-windows**は、Windows用のNode.jsバージョン管理ツールです。複数のNode.jsバージョンを同時にインストールし、必要に応じて切り替えることができます。

### インストール前の確認事項

1. **既存のNode.jsを完全削除**
   - 「プログラムと機能」からNode.jsをアンインストール
   - 残存フォルダの削除：
     ```
     C:\Program Files\nodejs\
     C:\Users\[ユーザー名]\AppData\Roaming\npm\
     ```

2. **PowerShellの実行ポリシー確認**
   ```powershell
   Get-ExecutionPolicy
   ```
   
   「Restricted」の場合は変更が必要：
   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

#### 用語解説：実行ポリシー
**実行ポリシー**とは、PowerShellスクリプトの実行に関するセキュリティ設定です。nvm-windowsはPowerShellスクリプトを使用するため、適切な設定が必要です。

### nvm-windowsのインストール手順

#### Step 1: ダウンロード

1. **GitHub リリースページにアクセス**
   ```
   https://github.com/coreybutler/nvm-windows/releases
   ```

2. **最新版のnvm-setup.exeをダウンロード**
   - 「Assets」セクションを展開
   - 「nvm-setup.exe」をクリック

#### Step 2: インストール

1. **インストーラーを実行**
   - ダウンロードした「nvm-setup.exe」をダブルクリック
   - セキュリティ警告で「実行」をクリック

2. **インストールウィザード**
   
   **License Agreement**：
   - 「I Agree」をクリック

   **Select Install Location**：
   - nvm-windowsのインストール先
   - デフォルト（`C:\Users\[ユーザー名]\AppData\Roaming\nvm`）推奨
   - 「Next」をクリック

   **Set Node.js Symlink**：
   - Node.jsのシンボリックリンク先
   - デフォルト（`C:\Program Files\nodejs`）推奨
   - 「Next」をクリック

#### 用語解説：シンボリックリンク
**シンボリックリンク**とは、実際のファイルやフォルダを指すショートカットのような仕組みです。nvm-windowsはこれを使って、複数のNode.jsバージョンを切り替えます。

   **Installation Complete**：
   - 「Finish」をクリック

#### Step 3: インストール確認

1. **新しいPowerShellを起動**（重要：再起動が必要）

2. **nvm-windowsの動作確認**
   ```powershell
   nvm version
   # 出力例：1.1.11
   ```

### Node.jsのインストールと管理

#### 利用可能なバージョンの確認

```powershell
# 利用可能な全バージョンを表示
nvm list available

# 出力例（抜粋）：
# |   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
# |--------------|--------------|--------------|--------------|
# |    23.3.0    |   22.11.0    |   0.12.18    |   0.11.16    |
# |    23.2.0    |   20.18.0    |   0.12.17    |   0.11.15    |
```

#### Node.js LTSバージョンのインストール

```powershell
# 最新LTS版をインストール
nvm install lts

# または特定バージョンを指定
nvm install 22.11.0

# インストール進行状況が表示される
# インストール完了まで数分待機
```

#### インストール済みバージョンの確認

```powershell
nvm list
# 出力例：
#   * 22.11.0 (Currently using 64-bit executable)
#     20.18.0
```

#### バージョンの切り替え

```powershell
# 特定バージョンに切り替え
nvm use 22.11.0

# 確認
node --version
# 出力：v22.11.0

npm --version
# 出力：10.2.4
```

#### バージョンの削除

```powershell
# 不要なバージョンを削除
nvm uninstall 20.18.0
```

## インストール後の設定と確認

### 基本動作テスト

#### Hello World プログラムの作成と実行

1. **テスト用フォルダの作成**
   ```powershell
   mkdir C:\nodejs-test
   cd C:\nodejs-test
   ```

2. **テストファイルの作成**
   ```powershell
   # テキストエディタでファイル作成
   notepad hello.js
   ```

3. **hello.jsの内容**
   ```javascript
   // hello.js
   console.log('Hello, Node.js!');
   console.log('Node.jsバージョン:', process.version);
   console.log('プラットフォーム:', process.platform);
   ```

4. **プログラムの実行**
   ```powershell
   node hello.js
   
   # 出力例：
   # Hello, Node.js!
   # Node.jsバージョン: v22.11.0
   # プラットフォーム: win32
   ```

### HTTP サーバーのテスト

より実践的なテストとして、簡単なWebサーバーを作成してみましょう：

```javascript
// server.js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
  res.end(`
    <h1>Node.js Webサーバーテスト</h1>
    <p>サーバーが正常に動作しています！</p>
    <p>Node.jsバージョン: ${process.version}</p>
    <p>現在時刻: ${new Date().toLocaleString('ja-JP')}</p>
  `);
});

const port = 3000;
server.listen(port, () => {
  console.log(`サーバーが http://localhost:${port} で起動しました`);
  console.log('停止するには Ctrl+C を押してください');
});
```

**実行手順**：
1. ファイルを `server.js` として保存
2. PowerShellで実行：
   ```powershell
   node server.js
   ```
3. ブラウザで `http://localhost:3000` にアクセス
4. 停止：`Ctrl+C`

#### 用語解説：localhost とポート番号
- **localhost**：自分のコンピューター自身を指すアドレス（127.0.0.1と同じ）
- **ポート番号**：コンピューター内でのサービスを識別する番号（3000はNode.js開発でよく使用される）

### npm の動作確認

#### パッケージの検索とインストールテスト

```powershell
# パッケージの検索
npm search moment

# テスト用フォルダでpackage.json作成
npm init -y

# パッケージのインストール
npm install moment

# インストール確認
npm list
```

#### 用語解説：package.json
**package.json**は、Node.jsプロジェクトの設定ファイルです。プロジェクト名、バージョン、依存パッケージなどの情報が記録されます。

#### グローバルパッケージのテスト

```powershell
# グローバルパッケージのインストール
npm install -g http-server

# インストール確認
http-server --version

# 簡単な静的サーバー起動テスト
# HTMLファイルがあるフォルダで実行
http-server -p 8080
```

#### 用語解説：グローバルパッケージ
**グローバルパッケージ**は、システム全体で使用できるパッケージです。コマンドラインツールなどがこれに該当します。

## 企業環境での特別な設定

### プロキシ設定

企業環境では、インターネットアクセスにプロキシサーバーを経由する場合があります：

```powershell
# プロキシ設定の確認
npm config get proxy
npm config get https-proxy

# プロキシの設定（必要な場合のみ）
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080

# 認証が必要な場合
npm config set proxy http://username:password@proxy.company.com:8080
```

### 企業内レジストリの設定

```powershell
# 企業内npmレジストリの設定（必要な場合のみ）
npm config set registry http://npm.company.com/

# 設定の確認
npm config get registry
```

## よくあるエラーと対処法

### エラー1: 'node' は内部コマンドまたは外部コマンドとして認識されていません

**原因**：PATH環境変数が正しく設定されていない

**対処法**：
1. PowerShellを再起動
2. PATH環境変数の確認と再設定
3. 最悪の場合、Node.jsの再インストール

### エラー2: npm ERR! network

**原因**：ネットワーク接続の問題またはプロキシ設定

**対処法**：
```powershell
# npm設定のクリア
npm config delete proxy
npm config delete https-proxy

# キャッシュのクリア
npm cache clean --force

# レジストリの確認
npm config get registry
```

### エラー3: EACCES: permission denied

**原因**：権限の問題

**対処法**：
1. PowerShellを管理者として実行
2. npm の グローバルフォルダの権限確認
3. 必要に応じてユーザーフォルダでの操作に変更

### エラー4: nvm use コマンドが効かない

**原因**：PowerShellの実行ポリシーまたは権限の問題

**対処法**：
```powershell
# 実行ポリシーの確認
Get-ExecutionPolicy

# 必要に応じて変更
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# PowerShellを管理者として再起動
```

## まとめ

この章では、Windows環境でのNode.jsインストール方法を学習しました。

**重要なポイント**：

1. **インストール方法の選択**
   - 初心者：公式インストーラー
   - 開発者：nvm-windows
   - 効率重視：パッケージマネージャー

2. **LTS版の選択推奨**
   - 安定性と長期サポート
   - 企業開発での標準

3. **インストール後の確認**
   - バージョン確認
   - 簡単なプログラムの実行
   - HTTP サーバーのテスト

4. **企業環境への対応**
   - プロキシ設定
   - 企業内レジストリ

5. **トラブルシューティング**
   - よくあるエラーの理解
   - 対処法の把握

次の章では、Node.js開発に最適化されたエディタであるVS Codeのセットアップと設定方法を学習します。インストールしたNode.jsを効率的に活用するための開発環境を整えていきましょう。

## 用語集

| 用語 | 説明 |
|------|------|
| PATH | コンピューターが実行可能なプログラムを探すディレクトリの一覧 |
| nvm | Node Version Manager - 複数のNode.jsバージョンを管理するツール |
| LTS | Long Term Support - 長期サポート版 |
| パッケージマネージャー | ソフトウェアのインストール・管理を自動化するツール |
| レジストリ | npmパッケージが保存されている場所 |
| 実行ポリシー | PowerShellスクリプトの実行に関するセキュリティ設定 |
| シンボリックリンク | 実際のファイルやフォルダを指すショートカットのような仕組み |
| localhost | 自分のコンピューター自身を指すアドレス |
| ポート番号 | コンピューター内でのサービスを識別する番号 |
| package.json | Node.jsプロジェクトの設定ファイル |
| グローバルパッケージ | システム全体で使用できるパッケージ |
| ネイティブモジュール | C++で書かれたNode.jsモジュール |