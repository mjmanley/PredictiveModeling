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

# Usando o serviço

Os métodos de modelagem disponíveis na paleta de modelagem SPSS Modeler permitem derivar novas informações de seus dados e desenvolver modelos preditivos. Cada método possui certas forças e é mais
adequado para certos tipos de problemas.
{: .shortdesc}

Para obter detalhes sobre o SPSS Modeler e a modelagem de algoritmos que ele fornece, consulte o [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SS3RA7).

Depois que os requisitos de entrada e saída de seu aplicativo Bluemix e do design de ramificação de pontuação SPSS Modeler
são implementados, seu Data Analyst pode mudar qualquer aspecto interno da ramificação de pontuação. O
Data Analyst pode até alterar o(s) algoritmo(s) de modelo usado(s) em uma operação de atualização,
assegurando sua capacidade de realizar ajuste fino de suas análises preditivas
sem precisar regravar seus aplicativos.


## Etapas para ligar o serviço ao aplicativo Bluemix
Conclua as etapas a seguir para criar seu aplicativo Bluemix e ligá-lo ao serviço do Machine Learning.

1. Faça download do código do aplicativo de amostra do Node.js no
[repositório github](https://github.com/pmservice/customer-satisfaction-prediction).

2. Use o comando cf create-service para criar uma instância de
serviço:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Por exemplo:

   ```
   cf create-service pm-20 Free my_pm_free
   ```
   {: codeblock}

   Esse comando cria uma instância de serviço de Machine Learning
com o plano grátis denominado my_pm_free no espaço do Bluemix.

3. Use o comando `cf create-service-key` para criar credenciais de serviço:

   ```
   cf create-service-key "{service instance name}" {vcap key name}
   ```
   {: codeblock}

   Por exemplo:

   ```
   cf create-service-key "IBM Watson Machine Learning - my instance" Credentials-1
   ```
   {: codeblock}

   Esse comando cria credenciais do serviço Machine Learning.

4. Use o comando cf bind-service para ligar a instância de serviço
my_pm_free ao aplicativo.

   ```
   cf bind-service AppName my_pm_service
   ```
   {: codeblock}

   Por exemplo:

   ```
   cf bind-service my_app1 my_pm_free
   ```
   {: codeblock}

   Esse comando liga a instância de serviço de Machine Learning
`my_pm_free` ao aplicativo Bluemix my_app1.

5. Credenciais do Machine Learning:

   Depois que você liga a instância de serviço de Machine Learning ao
aplicativo Bluemix, as credenciais do Machine Learning são
incluídas na variável de ambiente `VCAP_SERVICES`:

```
    {   
        "pm-20": {      
            "name": "pm20-1",
            "label": "pm-20",
            "plan": "Free",
            "credentials": {
                "url": "https://ibm-watson-ml.mybluemix.net",
                "access_key": "XXXXXXXXXXXXX"
            }
        }       
    }
```
{: codeblock}

   A variável de ambiente `VCAP_SERVICES` inclui as informações a seguir:

   <dl>

   <dt>plano</dt>
   <dd>O plano do Machine Learning usado no fornecimento de serviço.</dd>

   <dt>url</dt>
   <dd>O endereço da instância de serviço de Machine Learning.</dd>

   <dt>access_key</dt>
   <dd>O parâmetro de consulta accessKey a ser passado em todas as solicitações
para essa instância de serviço.</dd>

   </dl>

Por exemplo:             

```
Get https://ibm-watson-ml.mybluemix.net/pm/v1/model/sales_model2?accesskey=XXXXXXXXXXXXX
```
{: codeblock}

   O código de exemplo Node.js que mostra como obter a accessKey
da variável de ambiente `VCAP_SERVICES`:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var accessKey = credentials.access_key;
    }
```
{: codeblock}
