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

# サポートされる機械学習フレームワーク

IBM Watson Machine Learning サービスでは、モデルのライフサイクル管理の一環としてのモデル開発および検証のために、以下のフレームワークがサポートされています。


## Spark MLlib
Watson Machine Learning Online、Batch (ベータ)、Stream (ベータ) Deployment and Scoring サービス向けに、Spark MLlib のサポートがあります。特定のバージョンおよびランタイム環境のみがサポートされています。

### サポートされるバージョン
*  Spark 2.0

### 制約事項:

  *  分類モデルおよび回帰モデルのみがサポートされます。
  *  カスタム変換関数、ユーザー定義関数、およびクラスへの参照を含んでいるモデルはサポートされません。
  * scikit-learn モデル・デプロイメント要求中に返される "schema" エンドポイントは、このステージではサポートされません。
  *  Spark モデルのバッチおよびストリームのサポートはベータ版です。参加をご希望の場合は、ご自身を[待機リスト](https://www.ibm.biz/mlwaitlist)に追加してください。
  * Spark モデルの継続学習システムはベータ版です。参加をご希望の場合は、ご自身を[待機リスト](https://www.ibm.biz/mlwaitlist)に追加してください。

## Scikit-learn
Watson Machine Learning Online Deployment and Scoring サービス向けに、scikit-learn のサポートがあります。特定のバージョンおよびランタイム環境のみがサポートされています。

### サポートされるバージョン

- Python 3.5 ランタイム用 Anaconda 4.2.x
- Scikit-Learn 0.17

### Python ランタイム

WML Online Deployment and Scoring サービスを使用してデプロイされる必要のあるモデル用の Python ランタイムは、Python 3.5 です。

モデルが Python 2.7 ランタイムで作成された場合には、Python2.7 と Python3.5 の間の非互換性が原因でデプロイメントが失敗することがあります。

### サポートされる Python パッケージ

WML Online Deployment and Scoring サービスによってサポートさる Python パッケージのリストは、
[こちら](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)にあります。

### 制約事項

以下の制限の一部またはすべてを含んでいるいくつかの制約があります。

* 分類モデルおよび回帰モデルのみがサポートされます。
* モデルは、Python 3.5 ランタイム用 Anaconda 4.2.x によってサポートされるパッケージ (およびパッケージ・バージョン) への参照のみを含むことができます。
* デプロイメント要求中に返される "schema" エンドポイントは実装されません。
* このステージでは、スコアリング要求の応答として予測の確率は返されません。
* "predict()" API の入力タイプとして Pandas データ・フレームを必要とするモデルはサポートされません。
* カスタム変換関数、ユーザー定義関数およびクラスへの参照を含んでいるモデルはサポートされません。

## XGBoost (<span class='tag--beta'>ベータ</span>)
Watson Machine Learning Online Deployment and Scoring サービス向けに、XGBoost のサポートがあります。特定のバージョンおよびランタイム環境のみがサポートされています。

### サポートされるバージョン

- XGBoost 0.6
- Python 3.5 ランタイム用 Anaconda 4.2.x
- Scikit-Learn 0.17

### Python ランタイム

WML Online Deployment and Scoring サービスを使用してデプロイされる必要のあるモデル用の Python ランタイムは、Python 3.5 です。

モデルが Python 2.7 ランタイムで作成された場合には、Python2.7 と Python3.5 の間の非互換性が原因でデプロイメントが失敗することがあります。

### サポートされる Python パッケージ

WML Online Deployment and Scoring サービスによってサポートされる Python パッケージのリストは、
[こちら](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)にあります。

### 制約事項

以下の制限の一部またはすべてを含んでいるいくつかの制約があります。
* XGBoost サポートは、現在のところ、XGBoost の Scikit-Learn ラッパー (つまり、xgboost.sklearn.XGBClassifier および xgboost.sklearn.XGBRegressor) を使用して作成されたモデルに対して使用可能です。
* モデルは、Python 3.5 ランタイム用 Anaconda 4.2.x によってサポートされるパッケージ (およびパッケージ・バージョン) への参照のみを含むことができます。
* デプロイメント要求中に返される "schema" エンドポイントは実装されません。
* このステージでは、スコアリング要求の応答として予測の確率は返されません。
* カスタム変換関数、ユーザー定義関数およびクラスへの参照を含んでいるモデルはサポートされません。

## SPSS Modeler

Watson Machine Learning Online、Batch Deployment and Scoring サービス向けに、SPSS Modeler ストリームのサポートがあります。特定のバージョンおよびランタイム環境のみがサポートされています。

### サポートされるバージョン

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### 制約事項

SPSS Modeler ストリームには以下の制約事項があります。

*  スコアリング枝をリアルタイム・スコアリングで使用するために準備する場合、スコア要求で取得される入力データによって、スコアリング枝に入るように設計されたソース・ノードが置き換えられる必要があります。また、その結果の予測分析出力は、応答フローに戻る必要があります (事実上、スコアリング枝設計の端末ノードが置き換えられます)。
*  Bluemix でのリアルタイム実行のためにスコアリング枝を準備するときには、外部サービスへの接続を要求できません。例えば、IBM Analytical Decision Management スコアリング枝設計には、IBM SPSS Collaboration and Deployment Services リポジトリーに保管されたルールやモデルへの参照を含めることはできません。
*  スコアリング枝を Bluemix でリアルタイム・スコアリングのために実行する場合、外部サービスを要求できません。例えば、リアルタイムで IBM SPSS
Analytic Server および Apache Hadoop データ・ストアを必要とするモデル・アルゴリズムのデプロイとスコアリングを行うことはできません。
*  Machine Learning では、Modeler の組み込みの Python スクリプトがサポートされます。ストリームを Machine Learning での実行前に処理するために使用する方法が原因で、いくつかの制限があります。通常、ユーザーがストリームの実行を制御することを選択した場合、枝の端末ノードが参照されます。Machine Learning では、ストリームの処理時に、オーバーライドされる JSON のノードを識別してから、ストリームの実行前に置換を行います。これによって、参照される入力ノードとエクスポート・ノードが存在しなくなるためにストリームはスクリプトで失敗します。解決方法は、別のノードの ID を使用して、実行中に枝を一意的に識別することです。これで、組み込みの Python スクリプトで定義されたようにストリームが実行されるようになります。

## 詳細はこちら

IBM SPSS Analytic Server の学習された予測モデルの現行サポートに関する詳細については、[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/) の [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) セクションを参照してください。
