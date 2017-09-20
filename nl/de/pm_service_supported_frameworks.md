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

# Unterstützte Frameworks für Machine Learning

Der IBM Watson Machine Learning-Service unterstützt die folgenden Frameworks für Modellentwicklung und - überprüfung als Teil der Modelllebenszyklusverwaltung. 


## Spark MLlib
Es gibt Unterstützung für Spark MLlib für den Watson Machine Learning Online-, Batch- (Beta), Stream- (Beta) Deployment and Scoring-Service. Nur bestimmte Versionen und Laufzeitumgebungen werden unterstützt. 

### Unterstützte Versionen
*  Spark 2.0

### Einschränkungen:

  *  Nur Klassifizierungs- und Regressionsmodelle werden unterstützt. 
  *  Modelle, die Verweise zu angepassten Transformern, benutzerdefinierten Funktionen und Klassen enthalten, werden nicht unterstützt. 
  * Der Endpunkt "schema" wurde zurückgegeben, während die Modellbereitstellungsanforderung scikit-learn zu diesem Zeitpunkt nicht unterstützt wird. 
  *  Stapel- und Datenstromunterstützung für Spark-Modelle in der Betaversion. Wenn Sie an der Teilnahme interessiert sind, fügen Sie sich selbst zur [Warteliste](https://www.ibm.biz/mlwaitlist) hinzu!
  * Das Continuous Learning System für Spark-Modelle ist in der Betaversion verfügbar. Wenn Sie an der Teilnahme interessiert sind, fügen Sie sich selbst zur [Warteliste](https://www.ibm.biz/mlwaitlist) hinzu!

## Scikit-learn
Es gibt Unterstützung für scikit-learn für den Watson Machine Learning Online Deployment and Scoring-Service. Nur bestimmte Versionen und Laufzeitumgebungen werden unterstützt. 

### Unterstützte Versionen

- Anaconda 4.2.x für Python 3.5 Runtime
- Scikit-Learn 0.17

### Python Runtime

Die Python-Laufzeit für Modelle, die mithilfe des WML Online Deployment and Scoring-Service bereitgestellt werden müssen, ist Python 3.5.

In einigen Fällen, in denen Modelle in der Laufzeit Python 2.7 erstellt wurden, kann die Bereitstellung wegen Inkompatibilitäten zwischen Python 2.7 und Python 3.5 fehlschlagen.

### Unterstützte Python-Pakete

Eine Liste mit Python-Paketen, die von WML Online Deployment and Scoring-Service unterstützt werden, finden Sie [hier](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Einschränkungen

Es gibt einige Einschränkungen, die einige oder alle der folgenden Begrenzungen enthalten können:

* Es werden nur Klassifizierungs- und Regressionsmodelle unterstützt. 
* Modelle können nur Verweise auf die Pakete (und Paketversionen) enthalten, die von Anaconda 4.2.x für die Laufzeit Python 3.5 unterstützt werden.
* Der Endpunkt "schema" wurde zurückgegeben, während die Bereitstellungsanforderung nicht implementiert wurde.
* Die Wahrscheinlichkeit der Prognose wird zu diesem Zeitpunkt nicht als Antwort der Scoring-Anforderung zurückgegeben. 
* Modelle, die Pandas Dataframe als Eingabetyp für die API "predict()" erfordern, werden nicht unterstützt.
* Modelle, die Verweise zu angepassten Transformern, benutzerdefinierten Funktionen und Klassen enthalten, werden nicht unterstützt. 

## XGBoost <span class='tag--beta'>Beta</span>
Es gibt Unterstützung für XGBoost für den Watson Machine Learning Online Deployment and Scoring-Service. Nur bestimmte Versionen und Laufzeitumgebungen werden unterstützt. 

### Unterstützte Versionen

- XGBoost 0.6
- Anaconda 4.2.x for Python 3.5 Runtime
- Scikit-Learn 0.17

### Python Runtime

Die Python-Laufzeit für Modelle, die mithilfe des WML Online Deployment and Scoring-Service bereitgestellt werden müssen, ist Python 3.5.

In einigen Fällen, in denen Modelle in der Laufzeit Python 2.7 erstellt wurden, kann die Bereitstellung wegen Inkompatibilitäten zwischen Python 2.7 und Python 3.5 fehlschlagen.

### Unterstützte Python-Pakete

Eine Liste mit Python-Paketen, die von WML Online Deployment and Scoring-Service unterstützt werden, finden Sie [hier](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Einschränkungen

Es gibt einige Einschränkungen, die einige oder alle der folgenden Begrenzungen enthalten können:
* XGBoost-Unterstützung ist aktuell für Modelle verfügbar, die mithilfe der Scikit-Learn-Wrapper wie z. B. xgboost.sklearn.XGBClassifier und xgboost.sklearn.XGBRegressor von XGBoost erstellt wurden.
* Modelle können nur Verweise auf die Pakete (und Paketversionen) enthalten, die von Anaconda 4.2.x für die Laufzeit Python 3.5 unterstützt werden.
* Der Endpunkt "schema" wurde zurückgegeben, während die Bereitstellungsanforderung nicht implementiert wurde.
* Die Wahrscheinlichkeit der Prognose wird zu diesem Zeitpunkt nicht als Antwort der Scoring-Anforderung zurückgegeben. 
* Modelle, die Verweise zu angepassten Transformern, benutzerdefinierten Funktionen und Klassen enthalten, werden nicht unterstützt. 

## SPSS Modeler

Es gibt Unterstützung für SPSS Modeler-Datenströme für den Watson Machine Learning Online, bzw. Batch Deployment and Scoring-Service. Nur bestimmte Versionen und Laufzeitumgebungen werden unterstützt. 

### Unterstützte Versionen

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### Einschränkungen

Die folgenden Einschränkungen gelten für SPSS Modeler-Datenströme:

*  Beim Vorbereiten einer Scoring-Verzweigung für die Verwendung im Echtzeit-Scoring müssen Eingabedaten, die mit der Scoring-Anforderung eingehen, den Quellenknoten ersetzen, der in der Scoring-Verzweigung entworfen wurde, und die sich ergebene Vorhersageanalyse muss wieder in den Antwortablauf übergeben werden (wobei sie den Endknoten in der Gestaltung der Scoring-Verzweigung ersetzt).
*  Da die Scoring-Verzweigung für die Echtzeitausführung in Bluemix vorbereitet ist, kann sie keine Verbindung zu einem externen Service anfordern. Ein IBM Analytical Decision Management-Scoring-Verzweigungsdesign kann keine Referenzen auf Regeln oder andere Modelle enthalten, die in einem IBM SPSS Collaboration- oder
Deployment Services-Repository gespeichert sind.
*  Die Ausführung einer Scoring-Verzweigung für Echtzeit-Scoring in Bluemix kann keinen externen Service erfordern. Sie können keine Modellalgorithmen bereitstellen oder bewerten, die einen IBM SPSS
Analytic Server und Apache Hadoop-Data-Store in Echtzeit erfordern.
*  Machine Learning unterstützt Modeler-integriertes Python-Scripting. Es gibt einige Einschränkungen wegen der Methode,
die für die Verarbeitung von Datenströmen vor deren Ausführung in Machine Learning verwendet wird. Wenn ein Benutzer auswählt, dass er die Ausführung des Datenstroms steuert, wird in der Regel der Endknoten des Zweigs referenziert. Wenn bei Machine Learning der Datenstrom verarbeitet wird, kennzeichnen wir die Knoten von JSON,
die überschrieben werden, und ersetzen diese dann, bevor der Datenstrom ausgeführt
wird. Auf diese Weise schlägt der Datenstrom im Script fehl, da die referenzierten Eingabe- und Ausgabeknoten nicht mehr vorhanden sind. Die Lösung ist die Verwendung der ID eines anderen Knotens, um den Zweig während der Ausführung eindeutig anzugeben. Dies stellt sicher, dass der Datenstrom wie im integrierten Python-Script definiert ausgeführt wird.

## Weitere Informationen

Weitere Details zur aktuellen Unterstützung für IBM SPSS Analytic Server-trainierte Vorhersagemodelle finden Sie im Abschnitt [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) im [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/).
