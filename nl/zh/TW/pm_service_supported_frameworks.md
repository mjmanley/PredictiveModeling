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

# 支援的機器學習架構

IBM Watson Machine Learning 服務支援下列架構，以在模型生命週期管理的過程中進行模型開發和驗證。


## Spark MLlib
針對 Watson Machine Learning 線上、批次（測試版）、串流（測試版）部署及評分服務有 Spark MLlib 支援。只支援特定版本和運行環境。

### 支援的版本
*  Spark 2.0

### 限制：

  *  只支援分類及迴歸模型。
  *  不支援包含對自訂轉換器、使用者定義函數及類別之參照的模型。
  * 現階段不支援在 scikit-learn 模型部署要求期間傳回的 "schema" 端點。
  *  Spark 模型的批次及串流部署為測試版。如果您有興趣參與，請將自己新增到[等待清單](https://www.ibm.biz/mlwaitlist)！
  * Spark 模型的持續學習系統為測試版。如果您有興趣參與，請將自己新增到[等待清單](https://www.ibm.biz/mlwaitlist)！

## Scikit-learn
針對 Watson Machine Learning 線上部署及評分服務有 scikit-learn 支援。只支援特定版本和運行環境。

### 支援的版本

- Anaconda 4.2.x for Python 3.5 運行環境
- Scikit-Learn 0.17

### Python 運行環境

針對需要使用 WML 線上部署及評分服務部署的模型，Python 運行環境為 Python 3.5。

在某些情況下，當模型是以 Python 2.7 運行環境建立時，部署可能會因為 Python2.7 和 Python3.5 之間的不相容性而失敗。

### 支援的 Python 套件

您可以[在這裡](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)找到 WML 線上部署及評分服務支援的 Python 套件清單。

### 限制

有一些限制，其中可能包含下列部分或所有限制：

* 只支援分類及迴歸模型。
* 對於 Python 3.5 運行環境，模型只能包含對 Anaconda 4.2.x 所支援套件（及套件版本）的參照。
* 未實作在部署要求期間傳回的 "schema" 端點。
* 現階段預測的機率不會以評分要求的回應傳回。
* 不支援對於 "predict()" API 需要 Pandas Dataframe 作為輸入類型的模型。
* 不支援包含對自訂轉換器、使用者定義函數及類別之參照的模型。

## XGBoost <span class='tag--beta'>測試版</span>
針對 Watson Machine Learning 線上部署及評分服務有 XGBoost 支援。只支援特定版本和運行環境。

### 支援的版本

- XGBoost 0.6
- Anaconda 4.2.x for Python 3.5 運行環境
- Scikit-Learn 0.17

### Python 運行環境

針對需要使用 WML 線上部署及評分服務部署的模型，Python 運行環境為 Python 3.5。

在某些情況下，當模型是以 Python 2.7 運行環境建立時，部署可能會因為 Python2.7 和 Python3.5 之間的不相容性而失敗。

### 支援的 Python 套件

您可以[在這裡](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35)找到 WML 線上部署及評分服務支援的 Python 套件清單。

### 限制

有一些限制，其中可能包含下列部分或所有限制：
* 對於使用 XGBoost 的 Scikit-Learn 封套（亦即 xgboost.sklearn.XGBClassifier 和 xgboost.sklearn.XGBRegressor）建立的模型，目前有 XGBoost 支援。
* 對於 Python 3.5 運行環境，模型只能包含對 Anaconda 4.2.x 所支援套件（及套件版本）的參照。
* 未實作在部署要求期間傳回的 "schema" 端點。
* 現階段預測的機率不會以評分要求的回應傳回。
* 不支援包含對自訂轉換器、使用者定義函數及類別之參照的模型。

## SPSS Modeler

針對 Watson Machine Learning 線上、批次部署及評分服務有 SPSS Modeler 串流支援。只支援特定版本和運行環境。

### 支援的版本

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### 限制

SPSS Modeler 串流的限制如下：

*  準備好評分分支以用於即時評分時，評分要求上進入的輸入資料必須取代設計到評分分支中的來源節點，而且產生的預測分析輸出必須流回回應流程（實際上會取代評分分支設計中的終端機節點）。
*  因為評分分支是為了在 Bluemix 中進行即時執行而準備，所以不需要連線至外部服務。例如，IBM Analytical Decision Management 評分分支設計無法包含 IBM SPSS Collaboration and Deployment Services 儲存庫中所儲存規則或模型的參照。
*  為了在 Bluemix 中進行即時評分而執行評分分支時，不需要外部服務。例如，您無法針對需要 IBM SPSS Analytic Server 及 Apache Hadoop 資料儲存庫的模型演算法，即時進行部署及評分。
*  Machine Learning 支援 Modeler 內嵌式 Python Scripting。由於在 Machine Learning 中執行之前用於處理串流的方法之故，會有一些限制。一般來說，如果使用者選擇控制串流的執行，則會參照分支的終端機節點。對於 Machine Learning，我們在處理串流時，會識別 JSON 中將置換的節點，然後在串流執行之前執行取代。這會導致串流在 Script 中失敗，因為所參照的輸入及匯出節點已不存在。解決方案是在執行期間使用另一個節點的 ID 來唯一識別分支。這可確保串流會如內嵌式 Python Script 中所定義的方式執行。

## 進一步瞭解

如需 IBM SPSS Analytic Server 訓練之預測模型最新支援的詳細資料，請參閱 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/) 的 [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) 小節。
