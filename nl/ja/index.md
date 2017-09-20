---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-07"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Watson Machine Learning の概要
{: #WMLgettingstarted}

IBM® Watson™ Machine Learning を使用すると、予測分析をアプリケーションと統合できます。データ・サイエンティストは機械学習を使用して予測モデルを開発します。一方、開発者は機械学習を使用して、よりスマートな意思決定、難しい問題の解決、ユーザーの成果の向上を実現するアプリケーションを作成します。
{: shortdesc}

## 前提条件

Watson Machine Learning を使用するには、Bluemix カタログから、[サービス・インスタンス](https://console.bluemix.net/catalog/services/ibm-watson-machine-learning/)を作成する必要があります。

## 手順

1. [モデルを作成して保管します](pm_custom_models.html)。
2. [モデルをデプロイします](pm_service_api_spark_online.html)。
3. デプロイされたモデル `scoring endpoint` をアプリケーションで使用して、[予測を取得します](pm_service_api_spark_building.html)。

## 製品情報

Watson Machine Learning サービスは、任意のプログラミング言語から呼び出すことができる一連の REST API からなります。

Watson Machine Learning サービスはデプロイメントに重点を置いていますが、モデルやパイプラインを作成して操作するには、IBM SPSS Modeler または Data Science Experience が必要であることに注意してください。SPSS Modeler と Data Science Experience (Spark MLlib および Python scikit-learn を利用) はどちらも、機械学習、人工知能、統計学から取得したさまざまなモデリング手法を提供します。

## 関連リンク

さあ始めましょう。サービス・インスタンスの作成またはアプリケーションのバインドについては、『[Spark モデルおよび Python モデルを用いたサービスの使用](using_pm_service_dsx.html)』または『[SPSS モデルを用いたサービスの使用](using_pm_service.html)』を参照してください。

API の探索に関心がある場合は、[Spark モデルおよび Python モデル用のサービス API](pm_service_api_spark.html) または [SPSS モデル用のサービス API] (pm_service_api_spss.html) を参照してください。

SPSS Modeler の概要と提供されるモデリング・アルゴリズムについて詳しくは、[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7) を参照してください。

IBM Data Science Experience の概要と提供されるモデリング・アルゴリズムについて詳しくは、[https://datascience.ibm.com](https://datascience.ibm.com) を参照してください。
