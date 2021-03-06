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

# Distribuzione di modelli online


**Nome scenario**: Previsione linea di prodotti.

**Descrizione scenario**: una società che vende attrezzature esterne vuole
creare un modello che preveda l'interesse dei clienti verso la sua linea di
prodotti. Un data scientist ha preparato
un modello predittivo e lo condivide con te (lo sviluppatore). Il tuo compito è quello di distribuire il modello e
di generare le previsioni dell'interesse del cliente effettuando richieste di punteggio in base al modello distribuito.

## Utilizzo del modello di esempio

1. Vai alla scheda Esempi del dashboard IBM® Watson™ Machine
   Learning.

2. Nella sezione Modelli di esempio, cerca il tile Previsione linea di prodotti
   e fai clic sul pulsante Aggiungi modello (+).

Adesso vedrai il modello di esempio Previsione linea di prodotti nell'elenco
di modelli disponibili sulla scheda Modelli.


## Creazione della distribuzione online

1. Vai alla scheda Modelli del dashboard IBM® Watson™ Machine
   Learning.

2. Dal menu AZIONI, seleziona Crea distribuzione.

3. Nel modulo Crea distribuzione, fornisci Nome, Descrizione e Tipo online.

4. Fai clic sul pulsante Salva.

Adesso vedrai la distribuzione online nell'elenco di distribuzioni disponibili sulla scheda Distribuzioni.


## Recupero dei dettagli di distribuzione

Puoi controllare lo stato, l'indirizzo dell'endpoint di calcolo del punteggio (`Scoring Endpoint`)
e i parametri correlati al modello distribuito.

1. Vai alla scheda Distribuzioni del dashboard IBM® Watson™ Machine
   Learning.

2. Dal menu AZIONI, seleziona Visualizza dettagli.

Nota che il valore `Scoring Endpoint` è necessario per effettuare richieste di calcolo del punteggio nel passo successivo.


## Esecuzione di richieste di punteggio

Dal momento che il tuo endpoint di calcolo del punteggio è stato creato (`Scoring Endpoint`), puoi
ora generare le previsioni effettuando richieste di punteggio. In questo scenario, i record dei clienti vengono passati al
modello predittivo e viene restituita una previsione sui prodotti sportivi.

Intestazione record
di esempio:

```
GENDER,AGE,MARITAL_STATUS,PROFESSION
```
{: codeblock}

Record di
esempio:

```
M,27,Single,Professional
F,56,Unspecified,Hospitality
M,45,Married,Retired
```
{: codeblock}

Esempio di
richiesta:

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer  $token' -d '{"fields": ["GENDER","AGE","MARITAL_STATUS","PROFESSION"],"values": [["M",23,"Single","Student"],["M",55,"Single","Executive"]]}' https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/deployments/{deployment_id}/online
```
{: codeblock}

Esempio di output:

```
{
   "fields": ["GENDER",
      "AGE",
      "MARITAL_STATUS",
      "PROFESSION",
      "PROFESSION_IX",
      "GENDER_IX",
      "MARITAL_STATUS_IX",
      "features",
      "rawPrediction",
      "probability",
      "prediction",
      "predictedLabel"
   ],
   "records":[
      [
         "M",
         23,
         "Single",
         "Student",
         6.0,
         0.0,
         1.0,
         [
            0.0,
            23.0,
            1.0,
            6.0
         ],
         [
            5.600716147152702,
            6.482458372136143,
            6.048004170730676,
            0.20929155492307386,
            1.6595297550574055
         ],
         [
            0.2800358073576351,
            0.32412291860680714,
            0.3024002085365338,
            0.010464577746153694,
            0.08297648775287028
         ],
         1.0,
         "Personal Accessories"
      ],
      [
         "M",
         55,
         "Single",
         "Executive",
         3.0,
         0.0,
         1.0,
         [
            0.0,
            55.0,
            1.0,
            3.0
         ],
         [
            6.227653744886563,
            4.325198862164969,
            8.031953760146816,
            1.2319759269281225,
            0.1832177058735289
         ],
         [
            0.3113826872443282,
            0.2162599431082485,
            0.40159768800734086,
            0.06159879634640614,
            0.009160885293676447
         ],
         2.0,
         "Mountaineering Equipment"
      ]
   ]
}
```
{: codeblock}

Possiamo vedere, ad esempio, che un dirigente di 55 anni è
interessato a Mountaineering Equipment, mentre uno studente di 23 anni
è interessato a Personal Accessories.
