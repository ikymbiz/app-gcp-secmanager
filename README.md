# GCP/Firebase Security & Infra Manager (GCP SecManager)

## 概要・説明

**GCP SecManager** は、Google Cloud Platform (GCP) および Firebase のセキュリティルールやインフラストラクチャ設定を、ブラウザ上で直感的に管理・編集・デプロイできるシングルページアプリケーション (SPA) です。

本アプリケーションは、ローカル環境（ブラウザの IndexedDB）で動作する完全なクライアントサイドツールであり、PWA（Progressive Web App）およびオフラインでの利用に対応しています。さらに、Gemini 2.5 Flash エンジンを搭載した **AI アシスタント** が組み込まれており、自然言語による指示で Firestore のセキュリティルールや IAM ポリシーの自動生成が可能です。

GCP のサービスアカウントキーとバックエンド API URL を設定することで、実際の GCP プロジェクトとリアルタイムに同期・デプロイを行うことができます（未設定の場合はモックモードとして安全に試用可能です）。

## 主な機能一覧

* 📊 **ダッシュボード (Dashboard)**
  * プロジェクトのサマリー（プロジェクトID、セキュリティスコア、IAMロール数、コレクション数）をひと目で確認。
* 🗄️ **Firestore データエクスプローラ (Firestore Data)**
  * Firestore のコレクションとドキュメントを階層表示。
  * ドキュメントデータの JSON 形式での閲覧・編集・デプロイ機能。
  * GCP からのリアルタイムデータ同期（Sync DB）。
* 🛡️ **Firestore ルールマネージャー (Firestore Rules)**
  * `firestore.rules` のコードエディタ。
  * 現在のルールの同期（Sync）と、クラウドへの直接デプロイ（Deploy）。
* 🔐 **IAM & 権限管理 (IAM & Admin)**
  * ユーザーやサービスアカウントに対する IAM ロールの割り当て・管理。
* ⚡ **サーバーレス管理 (Cloud Run/Func)**
  * Cloud Run や Cloud Functions のサービス定義（リージョン、イメージ/ソースソース）の構成と管理。
* 🤖 **AI アーキテクト (AI Assistant)**
  * 画面右下のボタンからいつでも呼び出せる AI チャットアシスタント（Web Worker 非同期処理）。
  * インフラ設計、セキュリティルールの作成、Terraform コードの提案などを Gemini API がサポート。
* 💾 **バックアップ＆復元 (Data & Backup)**
  * カメラアイコンからいつでもローカルスナップショット（直近5世代）を自動保存・復元。
  * プロジェクト設定の JSON エクスポート / インポート機能。

## 使用技術・ライブラリ

* **フロントエンド・フレームワーク**: Vue 3 (Composition API)
* **スタイリング**: Tailwind CSS, FontAwesome 6
* **ローカルデータベース**: Dexie.js (IndexedDB)
* **マークダウンパース & ハイライト**: Marked.js, Highlight.js
* **AI・非同期処理**: Web Worker, Google Gemini API (2.5 Flash)
* **その他**: PWA 対応 (Service Worker, Web App Manifest)

## セットアップ・使い方

### 1. アプリケーションの起動
特別なビルド環境やサーバーは不要です。提供された HTML ファイルを Chrome, Edge, Safari などのモダンブラウザで開くだけですぐに利用を開始できます。

### 2. 初期設定 (Settings)
サイドバーの「Settings」メニューから、以下の設定を行ってください。

* **Gemini API Key (必須)**
  * AI アシスタントを利用するために必要です。Google AI Studio などで取得した API キーを入力してください。（キーはローカルの IndexedDB に安全に保存されます）
* **GCP Service Account Key (オプション)**
  * 実際の GCP リソースと連携する場合、GCP コンソールからダウンロードしたサービスアカウントの JSON キーをアップロードしてください。
* **Backend API URL (オプション)**
  * セキュアなサーバーサイド API（Cloud Functions など）のエンドポイントを設定します。未設定の場合は、すべての同期・デプロイ機能が **モックモード（テストモード）** として動作します。

### 3. プロジェクトの管理
* サイドバーの「Current Project」ドロップダウンから、管理したいプロジェクトを切り替えるか、「+ New Project」から新規作成します。
* サービスアカウントキーをアップロードすると、キーに含まれる `project_id` を読み取り、自動的にプロジェクト設定と紐付けることができます。

### 4. 日常のオペレーション
* 各画面右上にある **「Sync...」** ボタンで、クラウド上の最新状態をローカルに取り込みます。
* 設定を変更した後は、**「Deploy...」** ボタンをクリックして変更を GCP プロジェクトへ反映させます。
* 右上の **カメラアイコン** をクリックすると、作業中の状態をスナップショットとしてバックアップできます（「Settings」画面からリストア可能）。