# 簡単なTodo dapp

下記URLを参考(ほぼコピペ)
<https://zenn.dev/linnefromice/articles/create-simple-dapps-with-hardhat-and-react-ts>

## 使用技術
- スマートコントラクト
  - Solidity (Hardhatを利用)
- フロントエンド
  - ベースフレームワーク: React
  - web3クライアント: ethers

## 仕様
1. 複数のタスクを管理可能
2. タスクを作成する機能
3. 指定したタスクの完了ステータスを変更する機能

## セットアップ
```
  npx hardhat
```

`What do you want to do?` と聞かれるので
"Create an advanced sample project that uses TypeScript"
を選択し
`Do you want to install this sample project's dependencies~?`
と聞かれるので
`y` (yes)
と答える

## 実装順序
1. コントラクト `contracts/TodoList.sol`
2. デプロイ `scripts/deploy.ts`
3. フロントエンド `front/`
4. コントラクトへの接続

### コントラクト
1. `contracts/TodoList.sol`を実装する
2. コントラクトのコンパイル
  2. hardhatではデフォルトで`artifacts/`に生成物を配置


<bold>コンパイル</bold>
```
npx hardhat compile
```

### デプロイ
1. `scripts/deploy.ts`を実装する
2. ローカルネットワークを作成
```
npx hardhat node
```
3. `scripts/deploy.ts`の実行 (ローカルネットワークにデプロイされたコントラクトのアドレスが表示される(0x~))
```
npx hardhat run scripts/deploy.ts --network localhost
```

### フロントエンド
1. ライブラリ取得
```
mkdir front
cd front
yarn init -y
yarn add react react-dom typescript
yarn add --dev parcel @types/react @types/react-dom parcel-bundler
```

2. TypeScript利用のための設定
```
npx tsc --init
```

tsconfig.jsonを修正

3. フロントエンドを起動してブラウザで確認
frontディレクトリ以下に`src`を作成
```
mkdir src
cd src
```
フロントエンド起動はfrontディレクトリで実行
```
yarn dev
```

### コントラクトへの接続
etherjsのインストール
frontディレクトリで実行
```
yarn add etherjs
```

srcディレクトリ以下にabiディレクトリを作成してABIのファイルをコピー
```
mkdir abi
cp -rp ../artifacts/contracts/TodoList.sol/TodoList.json src/abi
```