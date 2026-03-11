# GCP/Firebase Security & Infra Manager

## 概要
「GCP/Firebase Security & Infra Manager (GCP SecManager)」は、ブラウザ上で完結するGoogle Cloud Platform (GCP) および Firebaseのインフラ・セキュリティ設定管理ツールです。
Firestoreのセキュリティルール、IAMポリシー、Cloud Run / Cloud Functionsなどのサーバーレス設定、さらにFirestoreのモックデータを一つの直感的なインターフェースで管理できます。

最大の特長として、**Gemini 2.5 Flash API** を統合したAIアシスタント（AI Architect）を搭載しています。要件を自然言語で伝えるだけで、複雑なセキュリティルールやインフラ構成コードをAIが自動生成・解説します。また、すべてのデータはブラウザのローカルデータベース（IndexedDB）に安全に保存され、PWAやオフライン動作にも対応しています。

## 主な機能
- **ダッシュボード**
  プロジェクトのID、セキュリティスコア、IAMロール数、Firestoreコレクション数などのプロジェクト概要を素早く把握できます。
- **Firestore Data Explorer**
  Firestoreのコレクションやドキュメントを管理します。ブラウザ上のJSONエディタを使用して、モックデータの作成・編集・削除が可能です。
- **Firestore Rules 管理**
  `firestore.rules` の編集が行えます。GCPからのルール同期（モック検証）やデプロイ（モック）のアクションをサポートします。
- **IAM & Admin**
  プロジェクトのIAMポリシー（メンバーとロール）を一覧で管理し、追加・削除が可能です。
- **サーバーレス環境管理**
  Cloud RunやCloud Functionsのサービス名、タイプ、リージョン、コンテナイメージを視覚的に管理できます。
- **AIアシスタント (AI Architect)**
  画面右下のフローティングボタンからチャットパネルを起動できます。AI処理はWeb Workerを利用して非同期で実行されるため、UIの動作を妨げません。
- **スナップショットとエクスポート機能**
  ワンクリックで現在の設定のバックアップ（最大5世代）を作成・復元できます。また、すべてのデータをJSONファイルとしてエクスポート/インポートし、他の環境へ移行することも可能です。
- **マルチプロジェクト対応**
  複数のGCP/Firebaseプロジェクトを作成し、ドロップダウンから簡単に切り替えて管理できます。

## 使用技術・ライブラリ
本プロジェクトは、Node.jsやnpmなどのビルドプロセスを必要とせず、単一のHTMLファイル内で動作する軽量かつモダンなアーキテクチャを採用しています。

- **フロントエンド**: Vue 3 (Composition API / グローバルビルド)
- **スタイリング**: Tailwind CSS (CDN), FontAwesome 6
- **データベース**: Dexie.js (IndexedDBラッパー)
- **マークダウンレンダリング**: Marked.js, Highlight.js (シンタックスハイライト)
- **AI連携**: Google Gemini API (Gemini 2.5 Flash)
- **ブラウザAPI**: Web Workers (AI非同期処理), PWA (Service Worker), Wake Lock API

## セットアップ・使い方

### 🚀 セットアップ
ビルド環境は不要です。
1. 提供されたHTMLコードを `index.html` という名前で保存します。
2. 保存したファイルをブラウザ（Google Chrome, Edge, Safariなど）で直接開くか、VS Codeの拡張機能「Live Server」などのローカルウェブサーバー経由で起動してください。

### ⚙️ 基本的な使い方

1. **APIキーの設定 (Settings)**
   左サイドバーから「Settings」メニューを開きます。
   AIアシスタントを利用するために、**Gemini API Key** を入力してください。（キーはサーバーには送信されず、お使いのブラウザのIndexedDBにのみ安全に保存されます）
   ※ GCP連携のモック機能を利用する場合は、「GCP Service Account Key (JSON)」もここでアップロードできます。

2. **プロジェクトの作成**
   左サイドバーの「Current Project」ドロップダウンから `+ New Project` を選択し、プロジェクト名を入力して新しい作業環境を作成します。

3. **Firestoreデータの管理 (Firestore Data)**
   「Firestore Data」メニューに移動し、コレクションリスト右上の「+」ボタンから新しいコレクションを作成します。その後「Add Doc」でドキュメントを追加し、中央のJSONエディタでデータを編集して「Save DB」をクリックします。

4. **AIへの相談 (AI Architect)**
   画面右下の「✨」アイコンをクリックしてAIチャットを開きます。
   「Firestoreのブログアプリ用セキュリティルールを作成して」や「Cloud RunのセキュアなIAM設定を教えて」と入力すると、AIがMarkdown形式で解説とコードを生成します。

5. **データのバックアップ**
   画面右上のカメラアイコン（📸）をクリックすると、現在の状態のスナップショットが作成されます。設定を誤った場合は、「Settings」画面の「Restore (5 Gens)」から過去の状態に復元できます。