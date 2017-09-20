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

# Framework di machine learning supportati

Il servizio IBM Watson Machine Learning supporta i seguenti framework per lo sviluppo e la convalida dei modelli come parte della gestione della durata del modello.


## Spark MLlib
È disponibile il supporto di Spark MLlib per il servizio Distribuzione e punteggio online, batch (beta) e stream (beta) di Watson Machine Learning. Sono supportati solo specifici ambienti di runtime e versioni.

### Versioni supportate
*  Spark 2.0

### Limitazioni:

  *  Sono supportati solo i modelli di classificazione e regressione.
  *  I modelli che contengono riferimenti a trasformatori personalizzati, funzioni definite dall'utente e classi non sono supportati.
  * L'endpoint "schema" restituito durante la richiesta di distribuzione del modello scikit-learn non è supportato in questa fase.
  *  Il supporto batch e streaming per i modelli Spark è in versione beta. Se sei interessato a partecipare, aggiungi il tuo nome alla [lista di attesa](https://www.ibm.biz/mlwaitlist).
  * Il sistema di apprendimento continuo per i modelli Spark è in versione beta. Se sei interessato a partecipare, aggiungi il tuo nome alla [lista di attesa](https://www.ibm.biz/mlwaitlist).

## Scikit-learn
È disponibile il supporto di scikit-learn per il servizio Distribuzione e punteggio online di Watson Machine Learning. Sono supportati solo specifici ambienti di runtime e versioni.

### Versioni supportate

- Anaconda 4.2.x per il runtime Python 3.5
- Scikit-Learn 0.17

### Runtime Python

Il runtime Python per i modelli che devono essere distribuiti utilizzando il servizio Distribuzione e punteggio online WML è Python 3.5.

In alcuni casi, dove i modelli sono stati creati nel runtime Python 2.7, la distribuzione potrebbe non riuscire a causa di incompatibilità tra Python 2.7 e Python 3.5.

### Pacchetti Python supportati

Un elenco di pacchetti Python supportati dal servizio Distribuzione e punteggio online WML è disponibile [qui](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Limitazioni

Esistono diverse limitazioni che possono includere alcune o tutte quelle riportate di seguito:

* Sono supportati solo i modelli di classificazione e regressione.
* I modelli possono contenere riferimenti solo ai pacchetti (e versione pacchetto) supportati da Anaconda 4.2.x per il runtime Python 3.5.
* L'endpoint "schema" restituito durante la richiesta di distribuzione non è implementato.
* La probabilità di previsione non viene restituita come risposta della richiesta di calcolo del punteggio in questa fase.
* I modelli che richiedono Pandas Dataframe come tipo di input per l'API "predict()" non sono supportati.
* I modelli che contengono riferimenti a trasformatori personalizzati, funzioni definite dall'utente e classi non sono supportati.

## XGBoost <span class='tag--beta'>Beta</span>
È disponibile il supporto di XGBoost per il servizio Distribuzione e punteggio online di Watson Machine Learning. Sono supportati solo specifici ambienti di runtime e versioni.

### Versioni supportate

- XGBoost 0.6
- Anaconda 4.2.x per il runtime Python 3.5
- Scikit-Learn 0.17

### Runtime Python

Il runtime Python per i modelli che devono essere distribuiti utilizzando il servizio Distribuzione e punteggio online WML è Python 3.5.

In alcuni casi, dove i modelli sono stati creati nel runtime Python 2.7, la distribuzione potrebbe non riuscire a causa di incompatibilità tra Python 2.7 e Python 3.5.

### Pacchetti Python supportati

Un elenco di pacchetti Python supportati dal servizio Distribuzione e punteggio online WML è disponibile [qui](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Limitazioni

Esistono diverse limitazioni che possono includere alcune o tutte quelle riportate di seguito:
* Il supporto XGBoost è attualmente disponibile per i modelli creati utilizzando i wrapper Scikit-Learn di XGBoost, ad esempio xgboost.sklearn.XGBClassifier e xgboost.sklearn.XGBRegressor.
* I modelli possono contenere riferimenti solo ai pacchetti (e versione pacchetto) supportati da Anaconda 4.2.x per il runtime Python 3.5.
* L'endpoint "schema" restituito durante la richiesta di distribuzione non è implementato.
* La probabilità di previsione non viene restituita come risposta della richiesta di calcolo del punteggio in questa fase.
* I modelli che contengono riferimenti a trasformatori personalizzati, funzioni definite dall'utente e classi non sono supportati.

## SPSS Modeler

È disponibile il supporto dei flussi SPSS Modeler per il servizio Distribuzione e punteggio online e batch di Watson Machine Learning. Sono supportati solo specifici ambienti di runtime e versioni.

### Versioni supportate

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### Limitazioni

Per i flussi SPSS Modeler esistono le seguenti limitazioni:

*  Quando un ramo di calcolo viene preparato per l'utilizzo per il calcolo in tempo reale, i dati di input ricevuti nella richiesta di calcolo
devono sostituire il nodo di origine creato nel ramo di calcolo e l'output di analisi predittiva risultante
deve ritornare al flusso della risposta (sostituendo di fatto il nodo del terminale
nella progettazione del ramo di calcolo).
*  Quando il ramo di calcolo è stato preparato per l'esecuzione in tempo reale in Bluemix, non può richiedere una connessione
a un servizio esterno. Ad esempio, una progettazione del ramo di calcolo di IBM Analytical Decision Management
non può contenere i riferimenti alle regole o ai modelli archiviati in un repository IBM SPSS Collaboration e
Deployment Services.
*  L'esecuzione di un ramo di calcolo per il calcolo in tempo reale in Bluemix non può richiedere un servizio
esterno. Ad esempio, non puoi distribuire e calcolare gli algoritmi del modello che richiedono un server IBM SPSS
Analytic e un archivio dati Apache Hadoop in tempo reale.
*  Machine Learning supporta lo script Modeler integrato con Python. Esistono alcune restrizioni dovute al metodo utilizzato per
   l'elaborazione dei flussi prima di essere eseguiti in Machine Learning. Normalmente, se un utente sceglie
di controllare l'esecuzione del flusso, fa riferimento al nodo del terminale del ramo. Per Machine Learning, quando elaboriamo il flusso, identifichiamo
   i nodi da JSON che saranno sovrascritti e quindi eseguiamo
   la sostituzione prima dell'esecuzione del flusso. Questo causa il malfunzionamento del flusso nello script perché i nodi di esportazione e l'input di riferimento
non esistono più. La soluzione è di utilizzare l'ID di un altro nodo per identificare univocamente il ramo
durante l'esecuzione. Ciò assicura che il flusso eseguito sia definito nello script Python integrato.

## Ulteriori informazioni

Per ulteriori dettagli sul supporto corrente per i modelli predittivi eseguiti dal server IBM SPSS Analytic, consulta la sezione [SPSS Analytic Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) in [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/).
