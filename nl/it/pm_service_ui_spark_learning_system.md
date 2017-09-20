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

# Sistema di apprendimento continuo <span class='tag--beta'>Beta</span>

Il sistema di apprendimento continuo IBM® Watson™ Machine Learning fornisce il monitoraggio automatizzato delle prestazioni, del riaggiornamento e della ridistribuzione del modello per garantire la qualità delle previsioni.

**Nome scenario**: Selezione dei farmaci migliori per il trattamento di disfunzioni cardiache.

**Descrizione scenario**: una società biomedica che produce farmaci per il cuore vuole distribuire un modello che selezioni il farmaco migliore per il trattamento di disfunzioni cardiache. Quando emergono nuove prove sull'efficacia del farmaco, è opportuno prendere in considerazione un aggiornamento del modello. Un data scientist prepara un modello predittivo e lo condivide con te (lo sviluppatore). Il tuo compito è quello di distribuire il modello, impostare la configurazione di apprendimento ed eseguire l'iterazione di apprendimento per valutare, riaggiornare e ridistribuire il modello. 

## Utilizzo del modello di esempio

1. Vai alla scheda Esempi del dashboard IBM® Watson™ Machine
   Learning.

2. Nella sezione Modelli di esempio, cerca il tile Selezione di farmaci per il cuore
   e fai clic sul pulsante Aggiungi modello (+).

Adesso vedrai il modello di esempio Selezione di farmaci per il cuore nell'elenco di modelli disponibili sulla scheda Modelli.


## Imposta il sistema di apprendimento continuo per il modello pubblicato

1.  Vai alla scheda Modelli del dashboard IBM® Watson™ Machine Learning.

2.  Dal menu **Azioni**, fai clic su **Visualizza dettagli**.

3.  Scorri fino a **Dettagli di riaggiornamento** e fai clic su **Modifica**.

4.  Devi fornire i seguenti input:

    **Connessione feedback**: i dettagli di Db2 Warehouse on Cloud, che verranno utilizzati come input (dati di feedback) per la valutazione e il riaggiornamento del modello.
    
    ```
    {
        "connection":{
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

    Utilizza le seguenti istruzioni per preparare la tabella `DRUG_FEEDBACK_DATA` in Db2 Warehouse on Cloud.
    - Crea un'istanza del [Servizio Db2 Warehouse on Cloud](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (viene offerto un piano di ingresso).
    - Crea la tabella **DRUG_FEEDBACK_DATA** in **Db2 Warehouse on Cloud**.
      + Scarica il file [drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv) dal repository git.
      + Fai clic sull'icona **Apri la console** per iniziare a utilizzare **Db2 Warehouse on Cloud**.
      + Seleziona il tipo di caricamento **Carica dati** e **Desktop**.
      + **Trascina e rilascia** il file precedentemente scaricato e fai clic su **Avanti**.
      + Seleziona **Schema** per importare i dati e fai clic su **Nuova tabella**.
      + Scrivi il nome per la **nuova tabella** e fai quindi clic su **Avanti** per terminare l'importazione dei dati.
      + Utilizza `;` come **separatore campi**.
      + Fai clic su **Avanti** per creare la tabella con i dati caricati.

    **Nota**: puoi aggiungere nuovi record di feedback al database di feedback utilizzando questo [endpoint API REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

    **Dimensione minima dei dati**: il numero minimo di record nel dataset di feedback per avviare la valutazione del modello (parte dell'iterazione del sistema di apprendimento).

    ```
    20
    ```
    {: codeblock}

    **Connessione Spark**: le credenziali del servizio Spark possono essere trovate nella scheda Credenziali del servizio del dashboard del servizio Bluemix Spark.

    ```
{
    "credentials": {
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

    **Soglie**: il valore di soglia che attiverà il processo di riaggiornamento (se calcolato durante la valutazione, il valore di metrica è inferiore alla soglia)

    ```
    0.8
    ```

    **Distribuisci automaticamente il modello riaggiornato**: distribuisci il modello riaggiornato se dimostra una migliore qualità (valore di metrica) rispetto a quello attualmente distribuito.

5.  Fai clic su **Configura**.


## Esegui l'iterazione del sistema di apprendimento continuo

Nell'iterazione, verrà valutato il modello pubblicato. Se l'accuratezza valutata è al di sotto della soglia specificata, verrà attivato il riaggiornamento del modello. Per il riaggiornamento e la valutazione, vengono utilizzati entrambi i dataset: formazione e feedback.

1. Per avviare una nuova iterazione, dal modulo del modello **Dettagli**, sulla scheda **Monitora**, fai clic su **Valuta**.

3. Per controllare il risultato dell'iterazione, vai alla tabella Eventi di valutazione o alla vista Grafico. Lì puoi trovare informazioni sulla qualità del modello calcolata in base ai dati di feedback (monitoraggio) e sulla qualità del modello riaggiornato (una nuova versione del modello creata e valutata).

4. Per vedere l'elenco di modelli formati automaticamente e la loro qualità, vai a Cronologia delle versioni che si trova in fondo alla scheda Panoramica (Visualizza dettagli modello -> Panoramica).
