---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# サービス API


Machine Learning サービスは、任意のプログラミング言語から呼び出される一連の REST API からなり、Data Science Experience で作成された分析をアプリケーションに統合することを可能にします。Bluemix アプリケーションを Machine Learning サービス・インスタンスにバインドして、アプリケーションがより高い価値をユーザーに提供するために必要な予測分析を生成します。[管理ダッシュボード](pm_service_ui_spark.html)でモデルを管理し、そのダッシュボードを使用して、アプリケーションと統合されたオンライン・デプロイメント、バッチ・デプロイメント、またはストリーミング・デプロイメントを作成します。

強力な [REST API](https://watson-ml-api.mybluemix.net/) を使用して、サービス・インスタンスにデプロイされた Data Science Experience ファイル (Spark モデルおよび Python モデル) に対するアプリケーションを開発します。

*  特定の予測モデル用のメタデータの取得
*  モデルのデプロイおよびデプロイされたモデルの管理
    *  オンライン・デプロイメント (スコアリング)
    *  バッチ・デプロイメント (Db2 Warehouse on Cloud をサポート)
    *  ストリーミング・デプロイメント (IBM MessageHub をサポート)
*  特定のデプロイメント用のメタデータの取得
*  デプロイされたモデルにスコア要求を出すことによる予測分析の生成

REST API の使用例については、以下のセクションを参照してください。

*  [オンライン・デプロイメントおよびスコアリング](pm_service_api_spark_online.html)
*  [Db2 Warehouse on Cloud を使用するバッチ・デプロイメント](pm_service_api_spark_batch.html)
*  [MessageHub を使用するストリーミング・デプロイメント](pm_service_api_spark_streaming.html)
