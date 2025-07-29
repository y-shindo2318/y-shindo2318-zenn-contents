---
title: "第4章: プロジェクト作成と基本的な開発ワークフロー"
---

# 新規プロジェクトの作成

この章では、実際にNode.jsプロジェクトを作成し、基本的な開発ワークフローを体験します。これまで構築した環境（Node.js + VS Code）を活用して、実践的な開発の流れを学んでいきましょう。

## Node.jsプロジェクトの基本構造

### プロジェクトとは

**プロジェクト**とは、関連するファイルやフォルダをまとめた作業単位のことです。Node.jsプロジェクトには以下のような特徴があります：

1. **package.json**: プロジェクトの設定ファイル
2. **node_modules**: 依存パッケージが保存されるフォルダ
3. **src または lib**: ソースコードを格納するフォルダ
4. **.gitignore**: Gitで管理しないファイルを指定

### 典型的なプロジェクト構造

```
my-first-node-project/
├── package.json          # プロジェクト設定ファイル
├── package-lock.json     # 依存関係の詳細情報
├── node_modules/         # 依存パッケージ（自動生成）
├── src/                  # ソースコードフォルダ
│   ├── index.js         # メインファイル
│   └── utils/           # ユーティリティ関数
├── test/                # テストファイル
├── docs/                # ドキュメント
├── .gitignore           # Git除外設定
└── README.md            # プロジェクト説明
```

## npm init によるプロジェクト初期化

### プロジェクトフォルダの作成

まず、新しいプロジェクト用のフォルダを作成します。

```powershell
# プロジェクト格納用のフォルダに移動
cd C:\
mkdir nodejs-projects
cd nodejs-projects

# 新しいプロジェクトフォルダを作成
mkdir my-first-node-project
cd my-first-node-project
```

### VS Codeでフォルダを開く

```powershell
# 現在のフォルダをVS Codeで開く
code .
```

#### 用語解説：カレントディレクトリ
**カレントディレクトリ**とは、現在作業しているフォルダのことです。`code .` の `.` は現在のフォルダを指します。

### npm init の実行

**npm init**は、新しいNode.jsプロジェクトを初期化するコマンドです。対話形式でプロジェクトの基本情報を設定できます。

```powershell
npm init
```

実行すると、以下のような質問が表示されます：

```
package name: (my-first-node-project) 
version: (1.0.0) 
description: 私の最初のNode.jsプロジェクト
entry point: (index.js) 
test command: 
git repository: 
keywords: node.js, 初心者, 学習
author: あなたの名前
license: (ISC) 
```

**各項目の説明**：

- **package name**: パッケージ名（フォルダ名がデフォルト）
- **version**: バージョン番号（セマンティックバージョニング）
- **description**: プロジェクトの説明
- **entry point**: メインファイル（通常は index.js）
- **test command**: テスト実行コマンド
- **git repository**: GitリポジトリのURL
- **keywords**: 検索用キーワード
- **author**: 作成者名
- **license**: ライセンス（ISC、MIT、GPL等）

#### 用語解説：セマンティックバージョニング
**セマンティックバージョニング**とは、バージョン番号を `メジャー.マイナー.パッチ`（例：1.2.3）の形式で管理する方法です。
- **メジャー**: 互換性のない変更
- **マイナー**: 後方互換性のある機能追加
- **パッチ**: 後方互換性のあるバグ修正

### package.json の内容確認

初期化が完了すると、`package.json` ファイルが作成されます：

```json
{
  "name": "my-first-node-project",
  "version": "1.0.0",
  "description": "私の最初のNode.jsプロジェクト",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "node.js",
    "初心者",
    "学習"
  ],
  "author": "あなたの名前",
  "license": "ISC"
}
```

#### package.json の重要な項目

**main**: 
- プロジェクトのエントリーポイント
- 他のプロジェクトから require() で読み込まれる際のファイル

**scripts**: 
- カスタムコマンドを定義
- `npm run <script-name>` で実行

**dependencies**: 
- 本番環境で必要なパッケージ
- `npm install <package>` でインストールしたパッケージが記録

**devDependencies**: 
- 開発時のみ必要なパッケージ
- `npm install <package> --save-dev` でインストール

### npm init の高速化

毎回質問に答えるのが面倒な場合は、デフォルト値で初期化できます：

```powershell
# すべてデフォルト値で初期化
npm init -y
# または
npm init --yes
```

## プロジェクト構造の設計

### ディレクトリ構造の作成

基本的なプロジェクト構造を作成しましょう：

```powershell
# フォルダ作成
mkdir src
mkdir test
mkdir docs

# ファイル作成（Windows）
echo. > src\index.js
echo. > test\index.test.js
echo. > .gitignore
echo. > README.md
```

VS Codeのエクスプローラーパネルから直接作成することも可能です：

1. **新しいフォルダ**: フォルダアイコンをクリック
2. **新しいファイル**: ファイルアイコンをクリック

### .gitignore ファイルの設定

`.gitignore` ファイルには、Gitで管理しないファイルやフォルダを指定します：

```gitignore
# .gitignore

# 依存関係
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# 環境設定
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# ログファイル
logs/
*.log

# OS生成ファイル
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# エディタ設定
.vscode/
.idea/
*.sublime-workspace
*.sublime-project

# ビルド結果
dist/
build/
```

#### 用語解説：.gitignore
**.gitignore**は、Gitによるバージョン管理から除外するファイルやフォルダを指定するファイルです。`node_modules`や設定ファイルなど、共有する必要のないファイルを除外します。

### README.md の作成

**README.md**は、プロジェクトの説明を記載するファイルです：

```markdown
# My First Node.js Project

私の最初のNode.jsプロジェクトです。

## 概要

このプロジェクトは、Node.js開発の基本的なワークフローを学習するために作成されました。

## 必要な環境

- Node.js v22.x 以上
- npm v10.x 以上

## インストール

```bash
# リポジトリをクローン
git clone <repository-url>

# プロジェクトフォルダに移動
cd my-first-node-project

# 依存関係をインストール
npm install
```

## 使用方法

```bash
# アプリケーションの実行
npm start

# テストの実行
npm test
```

## 作成者

あなたの名前

## ライセンス

ISC
```

#### 用語解説：Markdown
**Markdown**は、簡単な記法でフォーマットされた文書を作成できる軽量マークアップ言語です。GitHubなどでドキュメント作成によく使用されます。

## 依存関係の管理

### パッケージのインストール

Node.js開発では、他の開発者が作成したパッケージを活用することが一般的です。

#### 本番依存関係のインストール

```powershell
# express（Webフレームワーク）をインストール
npm install express

# 複数パッケージを同時インストール
npm install express body-parser cors
```

**インストール後の変化**：
1. `node_modules` フォルダが作成される
2. `package.json` の `dependencies` に追加される
3. `package-lock.json` が作成/更新される

```json
{
  "dependencies": {
    "express": "^4.18.2",
    "body-parser": "^1.20.2",
    "cors": "^2.8.5"
  }
}
```

#### 開発依存関係のインストール

開発時のみ必要なパッケージは `--save-dev` フラグを使用：

```powershell
# 開発時のみ必要なパッケージ
npm install --save-dev nodemon jest eslint prettier

# 短縮形
npm install -D nodemon jest eslint prettier
```

**結果**：
```json
{
  "devDependencies": {
    "nodemon": "^3.0.2",
    "jest": "^29.7.0",
    "eslint": "^8.55.0",
    "prettier": "^3.1.0"
  }
}
```

#### 用語解説：依存関係のタイプ
- **dependencies**: アプリケーション動作に必要（本番環境）
- **devDependencies**: 開発・ビルド・テストに必要（開発環境のみ）

### バージョン指定の理解

**npm**では、セマンティックバージョニングと組み合わせて柔軟なバージョン指定が可能です：

```json
{
  "dependencies": {
    "express": "4.18.2",      // 厳密なバージョン
    "body-parser": "^1.20.2", // 互換性のあるバージョン
    "cors": "~2.8.5",         // パッチレベルの更新のみ
    "lodash": "*",            // 最新版（非推奨）
    "moment": ">=2.29.0"      // 指定バージョン以上
  }
}
```

**記号の意味**：
- **なし**: 厳密なバージョン
- **^**: メジャーバージョンが同じ範囲で最新
- **~**: マイナーバージョンが同じ範囲で最新
- *****: 常に最新（危険）
- **>=**: 指定バージョン以上

### package-lock.json の役割

**package-lock.json**は、依存関係の正確なバージョンを記録するファイルです：

```json
{
  "name": "my-first-node-project",
  "version": "1.0.0",
  "lockfileVersion": 2,
  "requires": true,
  "packages": {
    "": {
      "name": "my-first-node-project",
      "version": "1.0.0",
      "dependencies": {
        "express": "^4.18.2"
      }
    },
    "node_modules/express": {
      "version": "4.18.2",
      "resolved": "https://registry.npmjs.org/express/-/express-4.18.2.tgz",
      "integrity": "sha512-5/PsL6iGPdfQ/lKM1UuielYgv3BUoJfz1aUwU9vHZ+J7gyvwdQXFEBIEIaxeGf0GIcreATNyBExtalisDbuMqQ==",
      "dependencies": {
        "accepts": "~1.3.8",
        // ... 他の依存関係
      }
    }
  }
}
```

**重要性**：
1. **再現可能なビルド**: 同じバージョンでの動作保証
2. **セキュリティ**: 已知的な安全なバージョンを使用
3. **チーム開発**: 全員が同じ環境で開発

## npm スクリプトの活用

### scripts セクションの設定

`package.json` の `scripts` セクションには、プロジェクト固有のコマンドを定義できます：

```json
{
  "scripts": {
    "start": "node src/index.js",
    "dev": "nodemon src/index.js",
    "test": "jest",
    "test:watch": "jest --watch",
    "lint": "eslint src/**/*.js",
    "lint:fix": "eslint src/**/*.js --fix",
    "format": "prettier --write src/**/*.js",
    "build": "echo 'ビルド処理を実行'",
    "clean": "rm -rf node_modules && rm package-lock.json"
  }
}
```

### スクリプトの実行

```powershell
# start スクリプトの実行（特別なコマンド）
npm start

# その他のスクリプト実行
npm run dev
npm run test
npm run lint

# 複数スクリプトの連続実行
npm run lint && npm run test && npm start
```

### よく使われるスクリプトパターン

#### 1. 開発用スクリプト

```json
{
  "scripts": {
    "dev": "nodemon --watch src src/index.js",
    "dev:debug": "nodemon --inspect src/index.js"
  }
}
```

#### 用語解説：nodemon
**nodemon**は、ファイルの変更を監視して、自動的にNode.jsアプリケーションを再起動するツールです。開発効率を大幅に向上させます。

#### 2. テスト用スクリプト

```json
{
  "scripts": {
    "test": "jest",
    "test:unit": "jest --testPathPattern=unit",
    "test:integration": "jest --testPathPattern=integration",
    "test:coverage": "jest --coverage"
  }
}
```

#### 3. コード品質管理スクリプト

```json
{
  "scripts": {
    "lint": "eslint src",
    "lint:fix": "eslint src --fix",
    "format": "prettier --write src",
    "check": "npm run lint && npm run test"
  }
}
```

#### 4. ビルド・デプロイ用スクリプト

```json
{
  "scripts": {
    "build": "webpack --mode production",
    "prebuild": "npm run clean",
    "postbuild": "npm run test",
    "deploy": "npm run build && npm run upload"
  }
}
```

#### 用語解説：pre/post スクリプト
**pre/post スクリプト**は、特定のスクリプト実行前後に自動実行されるスクリプトです。`prebuild`、`posttest` などの命名規則に従います。

## 実際のコードを書いてみよう

### Hello World アプリケーション

最初に、シンプルなHello Worldアプリケーションを作成しましょう：

```javascript
// src/index.js
console.log('Hello, Node.js!');
console.log('現在の時刻:', new Date().toLocaleString('ja-JP'));
console.log('Node.jsバージョン:', process.version);
console.log('作業ディレクトリ:', process.cwd());

// プロセス終了時の処理
process.on('exit', (code) => {
  console.log(`プロセスが終了しました。終了コード: ${code}`);
});

// Ctrl+C での終了を捕捉
process.on('SIGINT', () => {
  console.log('\nCtrl+C が押されました。アプリケーションを終了します。');
  process.exit(0);
});
```

**実行**：
```powershell
npm start
```

### 簡単なHTTPサーバー

Node.jsの強力な機能であるHTTPサーバーを作成してみましょう：

```javascript
// src/server.js
const http = require('http');
const url = require('url');

// サーバー設定
const hostname = 'localhost';
const port = 3000;

// リクエストハンドラー
const server = http.createServer((req, res) => {
  // URLを解析
  const parsedUrl = url.parse(req.url, true);
  const pathname = parsedUrl.pathname;
  const query = parsedUrl.query;

  // レスポンスヘッダーを設定
  res.writeHead(200, { 
    'Content-Type': 'text/html; charset=utf-8',
    'Access-Control-Allow-Origin': '*'
  });

  // ルーティング
  if (pathname === '/') {
    res.end(`
      <!DOCTYPE html>
      <html>
      <head>
        <title>Node.js Server</title>
        <meta charset="utf-8">
      </head>
      <body>
        <h1>Node.js HTTP サーバー</h1>
        <p>現在時刻: ${new Date().toLocaleString('ja-JP')}</p>
        <p>Node.js バージョン: ${process.version}</p>
        <ul>
          <li><a href="/about">About</a></li>
          <li><a href="/api/info">API Info</a></li>
        </ul>
      </body>
      </html>
    `);
  } else if (pathname === '/about') {
    res.end(`
      <h1>About</h1>
      <p>これは学習用のNode.jsサーバーです。</p>
      <a href="/">戻る</a>
    `);
  } else if (pathname === '/api/info') {
    // JSON APIの例
    res.writeHead(200, { 'Content-Type': 'application/json' });
    const info = {
      server: 'Node.js HTTP Server',
      version: process.version,
      timestamp: new Date().toISOString(),
      uptime: process.uptime(),
      memory: process.memoryUsage()
    };
    res.end(JSON.stringify(info, null, 2));
  } else {
    // 404 Not Found
    res.writeHead(404, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end(`
      <h1>404 - ページが見つかりません</h1>
      <p>要求されたページ "${pathname}" は存在しません。</p>
      <a href="/">ホームに戻る</a>
    `);
  }
});

// エラーハンドリング
server.on('error', (err) => {
  if (err.code === 'EADDRINUSE') {
    console.error(`ポート ${port} は既に使用されています。`);
  } else {
    console.error('サーバーエラー:', err);
  }
});

// サーバー起動
server.listen(port, hostname, () => {
  console.log(`サーバーが起動しました: http://${hostname}:${port}/`);
  console.log('停止するには Ctrl+C を押してください');
});
```

**package.json にスクリプトを追加**：
```json
{
  "scripts": {
    "start": "node src/index.js",
    "server": "node src/server.js",
    "dev": "nodemon src/server.js"
  }
}
```

**実行**：
```powershell
npm run server
```

ブラウザで `http://localhost:3000` にアクセスして動作確認してください。

### モジュールの作成と活用

Node.jsでは、コードを**モジュール**として分割して管理できます：

```javascript
// src/utils/datetime.js
/**
 * 日時関連のユーティリティ関数
 */

/**
 * 現在の日時を日本語形式で取得
 * @returns {string} 日本語形式の日時文字列
 */
function getCurrentDateTimeJP() {
  return new Date().toLocaleString('ja-JP', {
    year: 'numeric',
    month: '2-digit',
    day: '2-digit',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit'
  });
}

/**
 * Unix タイムスタンプを取得
 * @returns {number} Unix タイムスタンプ
 */
function getUnixTimestamp() {
  return Math.floor(Date.now() / 1000);
}

/**
 * 指定した日数後の日付を取得
 * @param {number} days - 日数
 * @returns {Date} 指定日数後の日付
 */
function getDateAfterDays(days) {
  const date = new Date();
  date.setDate(date.getDate() + days);
  return date;
}

// 複数の関数をエクスポート
module.exports = {
  getCurrentDateTimeJP,
  getUnixTimestamp,
  getDateAfterDays
};
```

```javascript
// src/utils/system.js
/**
 * システム情報取得ユーティリティ
 */

/**
 * システム情報を取得
 * @returns {object} システム情報オブジェクト
 */
function getSystemInfo() {
  return {
    platform: process.platform,
    architecture: process.arch,
    nodeVersion: process.version,
    memory: process.memoryUsage(),
    uptime: process.uptime(),
    pid: process.pid,
    cwd: process.cwd()
  };
}

/**
 * メモリ使用量を人間が読める形式で取得
 * @returns {object} メモリ使用量
 */
function getMemoryUsage() {
  const usage = process.memoryUsage();
  return {
    rss: `${Math.round(usage.rss / 1024 / 1024 * 100) / 100} MB`,
    heapTotal: `${Math.round(usage.heapTotal / 1024 / 1024 * 100) / 100} MB`,
    heapUsed: `${Math.round(usage.heapUsed / 1024 / 1024 * 100) / 100} MB`,
    external: `${Math.round(usage.external / 1024 / 1024 * 100) / 100} MB`
  };
}

module.exports = {
  getSystemInfo,
  getMemoryUsage
};
```

**モジュールを使用するメインファイル**：
```javascript
// src/app.js
// 自作モジュールのインポート
const datetime = require('./utils/datetime');
const system = require('./utils/system');

// 内蔵モジュールのインポート
const http = require('http');

console.log('=== Node.js アプリケーション開始 ===');
console.log('現在時刻:', datetime.getCurrentDateTimeJP());
console.log('Unix タイムスタンプ:', datetime.getUnixTimestamp());

console.log('\n=== システム情報 ===');
const sysInfo = system.getSystemInfo();
console.log('プラットフォーム:', sysInfo.platform);
console.log('アーキテクチャ:', sysInfo.architecture);
console.log('Node.js バージョン:', sysInfo.nodeVersion);
console.log('プロセスID:', sysInfo.pid);

console.log('\n=== メモリ使用量 ===');
const memUsage = system.getMemoryUsage();
console.log('RSS:', memUsage.rss);
console.log('Heap Total:', memUsage.heapTotal);
console.log('Heap Used:', memUsage.heapUsed);

// 5秒後の日付を表示
const futureDate = datetime.getDateAfterDays(5);
console.log('\n5日後の日付:', futureDate.toLocaleDateString('ja-JP'));
```

#### 用語解説：module.exports と require
- **module.exports**: モジュールから外部に公開する機能を定義
- **require()**: 他のモジュールを読み込む関数

## 環境変数の活用

### .env ファイルの作成

機密情報や環境固有の設定は、環境変数で管理するのがベストプラクティスです：

```bash
# .env
# データベース設定
DB_HOST=localhost
DB_PORT=5432
DB_NAME=myapp
DB_USER=admin
DB_PASSWORD=secret123

# サーバー設定
PORT=3000
HOST=localhost
NODE_ENV=development

# API設定
API_KEY=your-secret-api-key
API_URL=https://api.example.com

# セキュリティ設定
JWT_SECRET=super-secret-jwt-key
SESSION_SECRET=session-secret-key
```

### dotenv パッケージの使用

```powershell
# dotenv パッケージをインストール
npm install dotenv
```

```javascript
// src/config.js
require('dotenv').config();

const config = {
  server: {
    port: process.env.PORT || 3000,
    host: process.env.HOST || 'localhost',
    env: process.env.NODE_ENV || 'development'
  },
  database: {
    host: process.env.DB_HOST,
    port: process.env.DB_PORT,
    name: process.env.DB_NAME,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD
  },
  api: {
    key: process.env.API_KEY,
    url: process.env.API_URL
  }
};

module.exports = config;
```

```javascript
// src/server-with-config.js
const config = require('./config');
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  
  // 機密情報は除外して返却
  const safeConfig = {
    server: config.server,
    api: {
      url: config.api.url
    }
  };
  
  res.end(JSON.stringify(safeConfig, null, 2));
});

server.listen(config.server.port, config.server.host, () => {
  console.log(`サーバーが起動しました: http://${config.server.host}:${config.server.port}/`);
  console.log(`環境: ${config.server.env}`);
});
```

#### 用語解説：環境変数
**環境変数**は、オペレーティングシステムが管理する動的な値で、アプリケーションの設定を外部から与えるために使用されます。

## Git による バージョン管理

### Git リポジトリの初期化

```powershell
# Git リポジトリの初期化
git init

# 現在の状態を確認
git status
```

### 最初のコミット

```powershell
# すべてのファイルをステージに追加
git add .

# コミットメッセージと共にコミット
git commit -m "Initial commit: プロジェクトの初期設定"
```

### .gitignore の効果確認

```powershell
# 依存関係をインストール
npm install express

# Git status で node_modules が除外されていることを確認
git status
```

### コミットの履歴確認

```powershell
# コミット履歴を表示
git log --oneline
```

## トラブルシューティング

### よくある問題と解決方法

#### 問題1: npm install が失敗する

**症状**: パッケージのインストール中にエラーが発生

**考えられる原因**:
- ネットワーク接続の問題
- npm cache の破損
- 権限の問題

**解決方法**:
```powershell
# npm cache をクリア
npm cache clean --force

# レジストリの確認
npm config get registry

# 管理者権限でPowerShellを実行
```

#### 問題2: node コマンドが認識されない

**症状**: `'node' は内部コマンドとして認識されていません`

**解決方法**:
1. Node.js が正しくインストールされていることを確認
2. PATH 環境変数に Node.js が追加されていることを確認
3. PowerShell を再起動

#### 問題3: ポートが既に使用されている

**症状**: `EADDRINUSE: address already in use`

**解決方法**:
```powershell
# 使用中のポートを確認
netstat -ano | findstr :3000

# プロセスを終了（プロセスIDが必要）
taskkill /PID <プロセスID> /F

# 別のポートを使用
```

#### 問題4: モジュールが見つからない

**症状**: `Cannot find module 'module-name'`

**解決方法**:
```powershell
# node_modules を再インストール
rm -rf node_modules package-lock.json
npm install

# 特定のパッケージを再インストール
npm uninstall <package-name>
npm install <package-name>
```

## まとめ

この章では、Node.jsプロジェクトの作成から基本的な開発ワークフローまでを学習しました。

**重要なポイント**:

1. **プロジェクト初期化**
   - `npm init` による package.json 作成
   - 適切なディレクトリ構造の設計
   - .gitignore と README.md の作成

2. **依存関係管理**
   - dependencies と devDependencies の違い
   - セマンティックバージョニング
   - package-lock.json の重要性

3. **npm スクリプト**
   - カスタムコマンドの定義
   - よく使われるスクリプトパターン
   - pre/post スクリプトの活用

4. **実践的なコーディング**
   - モジュールの作成と活用
   - HTTP サーバーの構築
   - 環境変数の管理

5. **バージョン管理**
   - Git を使った変更履歴の管理
   - 適切な .gitignore 設定

次の章では、VS Code を使ったデバッグ機能とテスト環境の構築を学習します。作成したプロジェクトをより効率的に開発・管理するためのツールを活用していきましょう。

## 用語集

| 用語 | 説明 |
|------|------|
| カレントディレクトリ | 現在作業しているフォルダ |
| セマンティックバージョニング | メジャー.マイナー.パッチ形式のバージョン管理方法 |
| .gitignore | Gitによるバージョン管理から除外するファイルを指定 |
| Markdown | 簡単な記法でフォーマットされた文書を作成できる言語 |
| nodemon | ファイル変更を監視して自動再起動するツール |
| pre/post スクリプト | 特定スクリプト実行前後に自動実行されるスクリプト |
| module.exports | モジュールから外部に公開する機能を定義 |
| require() | 他のモジュールを読み込む関数 |
| 環境変数 | OSが管理する動的な値、アプリケーション設定に使用 |