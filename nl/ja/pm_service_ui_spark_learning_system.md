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

# 継続学習システム (<span class='tag--beta'>ベータ</span>)

IBM® Watson™ Machine Learning 継続学習システムは、予測品質を確保するため、モデル・パフォーマンスの自動モニタリング、リトレーニング、および再デプロイメントを提供します。

**シナリオ名**: 最適な心臓治療薬品の選択。

**シナリオの説明**: 心臓用の医薬品を製造するバイオ医薬品会社が、心臓治療のために最適な薬品を選択するモデルをデプロイしたいと考えています。薬品の有効性に関する新しいエビデンスが出現した際には、モデル更新が検討される必要があります。データ・サイエンティストが、予測モデルを準備し、それを開発者と共有します。開発者のタスクは、モデルをデプロイし、learning configuration を設定し、learning iteration を実行して、モデルの評価、リトレーニング、および再デプロイを行うことです。

## サンプル・モデルの使用

1. IBM® Watson™ Machine Learning ダッシュボードの「サンプル」タブに移動します。

2. 「サンプル・モデル」セクションで「Heart Drug Selection」タイルを見つけて、「モデルの追加」ボタン (+) をクリックします。

これで、「モデル」タブの使用可能なモデルのリストに、サンプルの「Heart Drug Selection」モデルが表示されるようになります。


## 公開されたモデルの継続学習システムの設定

1.  IBM® Watson™ Machine Learning ダッシュボードの「モデル」タブに移動します。

2.  **「アクション」**メニューで**「詳細の表示」**をクリックします。

3.  **「リトレーニング詳細」**までスクロールダウンし、**「編集」**を押します。

4.  以下を入力する必要があります。

    **フィードバック接続**: モデルの評価およびリトレーニングのための入力 (フィードバック・データ) として使用される、Db2 Warehouse on Cloud の詳細。
    
    ```
    {
        "connection": {
            "username": "dash102204",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "password": "NweTlYwPY6cu",
            "db": "BLUDB"
        },
        "source": {
            "type": "dashdb",
            "tablename": "DRUG_FEEDBACK_DATA"
        }
    }
    ```
    {: codeblock}

    以下の説明に従って、Db2 Warehouse on Cloud に `DRUG_FEEDBACK_DATA` 表を作成してください。
    - [Db2 Warehouse on Cloud サービス](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/)のインスタンスを作成します (入門プランが提供されています)。
    - **Db2 Warehouse on Cloud** に **DRUG_FEEDBACK_DATA** 表を作成します。
      + Git リポジトリーから [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) ファイルをダウンロードします。
      + **「コンソールを開く」**をクリックし、**「Db2 Warehouse on Cloud」**アイコンで開始します。
      + **「データのロード」**および**「デスクトップ」**ロード・タイプを選択します。
      + 前にダウンロードしたファイルを**ドラッグ・アンド・ドロップ**し、**「次へ」**を押します。
      + データをインポートする**スキーマ**を選択し、**「新規表」**をクリックします。
      + **新規表**の名前を入力し、データのインポートを終了するために**「次へ」**をクリックします。
      + **「フィールド分離文字」**には `;` を使用します。
      + **「次へ」**をクリックして、アップロードしたデータで表を作成します。

    **注:** この [REST API エンドポイント](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)を使用して、新規フィードバック・レコードをフィードバック・データベースに追加できます。

    **最小データ・サイズ**: モデルの評価 (学習システムのイテレーションの一部) を開始するための、フィードバック・データ・セット内のレコードの最小数。

    ```
    20
    ```
    {: codeblock}

    **Spark 接続**: Spark サービス資格情報は、Bluemix Spark サービス・ダッシュボードの「サービス資格情報」タブにあります。

    ```
{
    "credentials":{
      "tenant_id": "s745-299dcf850a6390-35c9a7ecf27a",
      "tenant_id_full": "ba3dde5a-ee64-4057-9749-299dcf850a63_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "cluster_master_url": "https://spark.bluemix.net",
      "instance_id": "ba3dde5a-ee64-4057-9749-299dcf850a63",
      "tenant_secret": "c0cba7a4-7b19-46e6-9326-44c4f48aaf08",
      "plan": "ibm.SparkService.PayGoPersonal"
},
    "version":"2.0"
}
    ```
    {: codeblock}

    **しきい値**: リトレーニング・プロセスを (評価中に計算されたメトリック値がしきい値を下回った場合に) トリガーするしきい値

    ```
    0.8
    ```

    **リトレーニングされたモデルの自動デプロイ**: リトレーニングされたモデルが現在デプロイされているモデルよりも品質 (メトリック値) が優れている場合は、リトレーニングされたモデルをデプロイします。

5.  **「セットアップ」**をクリックします。


## 継続学習システムのイテレーションの実行

イテレーション内で、公開されたモデルが評価されます。評価された正確度が指定のしきい値を下回ると、モデルのリトレーニングがトリガーされます。トレーニングとフィードバックの両方のデータ・セットが、リトレーニングおよび評価のために使用されます。

1. 新規イテレーションを開始するには、モデルの**「詳細」**フォームから、**「モニター」**タブで**「評価」**をクリックします。

3. イテレーション結果を確認するには、「Evaluation Events」表または「グラフ」ビューのいずれかに移動します。そこで、フィードバック・データに基づいて計算されたモデル品質 (モニタリング)、リトレーニングされたモデル品質 (作成および評価された新しいモデル・バージョン) についての情報を確認できます。

4. 自動的にトレーニングされたモデルとそれらの品質のリストを表示するには、「概要」タブの下部にある「バージョン履歴」に移動します (モデルの「詳細の表示」->「概要」)。
