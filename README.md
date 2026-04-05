# Tesco価格トラッカー

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.jp)
[![Tesco Price Tracker](https://img.shields.io/badge/Tesco%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.jp/products/insights/price-tracker/tesco)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.jp/products/insights/price-tracker/tesco)

英国最大のスーパーマーケットチェーンであるTescoの価格をリアルタイムで追跡します。始める方法は2つあります。**フルマネージド**のインテリジェンスプラットフォーム、またはBright DataのAI Scraper Builderで構築する**カスタムスクレイパー**です。

---

## オプション1: Bright Insights - AI搭載の価格トラッキング（推奨）

**[Bright Insights](https://brightdata.jp/products/insights/price-tracker/tesco)** は、Bright Dataのフルマネージドなリテールインテリジェンスプラットフォームです。スクレイパーを構築する必要も、インフラを維持する必要もありません。構造化され、分析可能な価格データがダッシュボード、データフィード、またはBIツールに提供されます。

**チームがBright Insightsを選ぶ理由:**
- 🚀 **セットアップ不要** - すぐに使えるダッシュボードとデータフィードで数分で本番稼働
- 🤖 **AIによるレコメンデーション** - 対話型AIアシスタントが数百万のデータポイントを即座に実用的なインサイトに変換
- ⚡ **リアルタイムモニタリング** - 1時間ごとから日次までの更新頻度と即時アラート（email、Slack、webhook）
- 🌍 **無制限のスケール** - あらゆるWebサイト、あらゆる地域、あらゆる更新頻度に対応
- 🔗 **プラグアンドプレイ統合** - AWS、GCP、Databricks、Snowflakeなど
- 🛡️ **フルマネージド** - Bright Dataがスキーマ変更、サイト更新、データ品質を自動で処理

**主なユースケース:**
- ✅ Tescoのカテゴリ横断で**食料品価格インフレを追跡**
- ✅ **プロモーション**や週間セールを自動で監視
- ✅ バスケット分析のための**価格履歴データベースを構築**
- ✅ MAPポリシー準拠を監視し、価格違反を検出
- ✅ 競合のプロモーションと販促動向を追跡
- ✅ クリーンで正規化されたデータを動的価格設定アルゴリズムやAIモデルに直接投入

> **月額$250から - [最適な見積もりを取得 →](https://brightdata.jp/products/insights/price-tracker/tesco)**

---

## オプション2: 独自のTescoスクレイパーを構築する

事前構築済みのTesco scraper APIがない？問題ありません。Bright Dataの**AI Scraper Builder**なら、数クリックでカスタムTescoスクレイパーを生成できます。コーディングは不要です。

### 数分でTescoスクレイパーを構築

**[Tesco AI Scraper Builderを開く →](https://brightdata.jp/products/web-scraper/tesco)**

ドメインを選択し、必要なデータ要件を指定すれば、AI scraper builderが自動的にAPIを作成します。

1. **必要なデータを平易な英語で記述**
2. **AIが即座にscraper APIを生成**
3. **APIリクエストを実行してすぐに結果を取得**
4. **必要に応じて組み込みIDEでコードを編集**

構築が完了すると、スクレイパーに**Web Scraper ID**（`gd_xxxxxxxxxxxx`）が付与されます。以下のセットアップ手順で使用するため、コピーしておいてください。

### 前提条件

- Python 3.9以上
- [Bright Dataアカウント](https://brightdata.jp)（無料トライアルあり）
- Bright Dataの**API token**（[取得方法](https://docs.brightdata.jp/general/account/account-settings#api-token)）
- Tesco用の**Web Scraper ID**（上記の構築手順で取得）

### セットアップ

1. **このrepositoryをclone**

   ```bash
   git clone https://github.com/bright-jp/tesco-price-tracker.git
   cd tesco-price-tracker
   ```

2. **依存関係をインストール**

   ```bash
   pip install -r requirements.txt
   ```

3. **認証情報を設定**

   `.env.example` を `.env` にコピーし、値を入力します:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Web Scraper ID**
   > [AI Scraper Builderダッシュボード](https://brightdata.jp/products/web-scraper/tesco)のWeb Scraper IDを
   > `BRIGHTDATA_DATASET_ID` に貼り付けてください（形式: `gd_xxxxxxxxxxxx`）。

---

## 使い方

Tescoスクレイパーの構築が完了し、Web Scraper IDを `.env` に設定すると、Pythonインターフェースは同じ方法で動作します。

### 1. URLで特定の商品を追跡

Tescoの商品URLのリストを渡して、構造化された価格データを取得します:

```python
from price_tracker import track_prices

urls = [
    "https://www.tesco.com/products/sample-product",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

または直接実行:

```bash
python price_tracker.py
```

### 2. キーワードで商品を検索

キーワード検索に一致する商品を見つけます:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. カテゴリURLで商品を閲覧

Tescoのカテゴリページからすべての商品を収集します:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://tesco.com/category/example",
    limit=100,
)
```

---

## 出力フィールド

各結果レコードには次のフィールドが含まれます:

| Field | Description |
|-------|-------------|
| `url` | 商品ページURL |
| `name` | 商品名 |
| `brand` | ブランド |
| `price` | 現在価格 |
| `currency` | 通貨コード |
| `unit_price` | 単位/重量あたりの価格 |
| `in_stock` | 在庫状況 |
| `category` | 商品カテゴリ |
| `sku` | SKU / バーコード |
| `images` | 商品画像URL |
| `description` | 商品説明 |
| `timestamp` | 収集タイムスタンプ |

### 出力例

```json
[
  {
    "url": "https://www.tesco.com/products/sample-product",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://tesco.com/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## 高度なオプション

`trigger_collection()` 関数は、データ収集を制御するためのオプションパラメータを受け付けます:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 返されるレコードの最大数 |
| `include_errors` | boolean | `true` | 結果にエラーレポートを含める |
| `notify` | string (URL) | - | スナップショットの準備完了時に呼び出すWebhook URL |
| `format` | string | `json` | 出力形式: `json`、`csv`、または`ndjson` |

オプション付きの例:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.tesco.com/products/sample-product"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## リソース

- 🌟 [Tesco Price Tracker - Bright Insights (Managed)](https://brightdata.jp/products/insights/price-tracker/tesco)
- 🏗️ [Tesco Scraperを構築](https://brightdata.jp/products/web-scraper/tesco)
- 📖 [Bright Data Web Scraper APIドキュメント](https://docs.brightdata.jp/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapersコントロールパネル](https://brightdata.jp/cp/scrapers)
- 🔑 [API tokenの取得方法](https://docs.brightdata.jp/general/account/account-settings#api-token)
- 🌐 [Bright Dataホームページ](https://brightdata.jp)

---

*[Bright Data](https://brightdata.jp)で構築 - 業界をリードするWebデータプラットフォーム。*