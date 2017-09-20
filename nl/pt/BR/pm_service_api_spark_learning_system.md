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

# Sistema de aprendizado contínuo <span class='tag--beta'>Beta</span>

O sistema de aprendizado contínuo fornece monitoramento automatizado de desempenho,
novo treinamento e reimplementação de modelo para assegurar a qualidade certa das predições.


**Nome do cenário**: bons medicamentos para seleção de tratamento cardíaco.

**Descrição do cenário**: uma empresa biomédica que produz remédios para o coração
deseja implementar um modelo que seleciona o melhor medicamento para tratamento cardíaco. Quando surge uma
nova evidência na eficácia de medicamento, uma atualização do modelo deve ser considerada. Um
cientista de dados preparou um modelo preditivo e o compartilha com você (o
desenvolvedor). Sua tarefa é implementar o modelo, definir a configuração do aprendizado e executar a iteração
do aprendendo para avaliar, treinar novamente e reimplementar o modelo.

**Nota**: também é possível trabalhar com o
[bloco
de notas](https://apsportal.ibm.com/analytics/notebooks/a97cde0b-5bb8-436a-ae82-83e96adc45e0/view?access_token=6baf4c722e452836f7b505205bc96d9a24b9333ee9b5c39453f6d7751987f798) de amostra do Python, que cria um modelo de amostra, configura o sistema de aprendizagem e,
por fim, executa a iteração do aprendizado.

## Usando o modelo de amostra

1. Acesse a guia **Amostras** do Painel do IBM® Watson™ Machine Learning.

2. Na seção **Modelos de amostra**, localize o ladrilho da Seleção de
Medicamento do Coração e clique no ícone **Incluir modelo** (+).

Agora você verá o modelo de amostra Seleção de Medicamento do Coração na lista de modelos disponíveis na
guia Modelos.

## Gerando o token de acesso

Gere um token de acesso usando o usuário e a senha disponíveis
na guia Credenciais de serviço da instância de serviço do IBM Watson Machine
Learning.

Exemplo de solicitação:

```
curl --basic --user <username>:<password> https://ibm-watson-ml.mybluemix.net/v3/identity/token
```
{: codeblock}

Exemplo de saída:

```
{"token":"**********"}
```
{: codeblock}

Use o comando do terminal a seguir para designar seu valor do token para o token de variável de ambiente:

```
token="<token_value>"
```
{: codeblock}

## Trabalhando com modelos publicados

Utilize a chamada de API a seguir para obter detalhes de sua instância, como:

* `url` de modelos publicados 
* `url` de implementações
* informações de uso

Exemplo de solicitação:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}
```
{: codeblock}

Exemplo de saída:

```
{
   "metadata" : {
      "guid":"360c510b-012c-4793-ae3f-063410081c3e",
      "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e",
      "created_at":"2017-08-04T09:15:48.344Z",
      "modified_at":"2017-08-22T08:34:47.759Z"
   },
   "entity":{
      "source":"Bluemix",
      "published_models":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models"
      },
      "usage":{
         "expiration_date":"2017-09-01T00:00:00.000Z",
         "computation_time":{
            "current":4
         },
         "model_count":{
            "limit":1000,
            "current":2
         },
         "prediction_count":{
            "current":16
         },
         "deployment_count":{
            "limit":1000,
            "current":1
         }
      },
      "plan_id":"0f2a3c2c-456b-40f3-9b19-726d2740b11c",
      "status":"Active",
      "organization_guid":"b0e61605-a82e-4f03-9e9f-2767973c084d",
      "region":"us-south",
      "account":{
         "id":"f52968f3dbbe7b0b53e15743d45e5e90",
         "name":"Umit Cakmak's Account",
         "type":"TRIAL"
      },
      "owner":{
         "ibm_id":"31000292EV",
         "email":"umit.cakmak@pl.ibm.com",
         "user_id":"43e0ee0e-6bfb-48fc-bcd8-d61e40d19253",
         "country_code":"POL",
         "beta_user":true
      },
      "deployments":{
         "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/deployments"
      },
      "space_guid":"4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
      "plan":"standard"
   }
}
```
{: codeblock}


Com a `url` de **published_models**, use a chamada de API a seguir
para obter detalhes do modelo:

Exemplo de solicitação:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer  $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models
```
{: codeblock}

Exemplo de saída:

```
{  
   "count":1,
   "resources":[  
      {  
         "metadata":{  
      "guid":"361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d",
            "created_at":"2017-08-22T08:34:47.597Z",
            "modified_at":"2017-08-22T08:34:47.691Z"
         },
   "entity":{  
      "runtime_environment":"spark-2.0",
            "author":{  

            },
            "name":"Best Heart Drug Selection",
            "label_col":"DRUG",
            "training_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"DRUG"
                     },
                     "type":"string",
                     "name":"DRUG",
                     "nullable":true
                  }
               ],
               "type":"struct"
            },
            "latest_version":{  
               "url":"https://ibm-watson-ml.mybluemix.net/v2/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "guid":"8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3",
               "created_at":"2017-08-22T08:34:47.691Z"
            },
            "model_type":"sparkml-model-2.0",
            "deployments":{  
               "count":0,
               "url":"https://ibm-watson-ml.mybluemix.net/v3/wml_instances/360c510b-012c-4793-ae3f-063410081c3e/published_models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/deployments"
            },
            "input_data_schema":{  
               "fields":[  
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"AGE"
                     },
                     "type":"integer",
                     "name":"AGE",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"SEX"
                     },
                     "type":"string",
                     "name":"SEX",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"BP"
                     },
                     "type":"string",
                     "name":"BP",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":0,
                        "name":"CHOLESTEROL"
                     },
                     "type":"string",
                     "name":"CHOLESTEROL",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"NA"
                     },
                     "type":"decimal(12,6)",
                     "name":"NA",
                     "nullable":true
                  },
                  {  
                     "metadata":{  
      "scale":6,
                        "name":"K"
                     },
                     "type":"decimal(13,6)",
                     "name":"K",
                     "nullable":true
                  }
               ],
               "type":"struct"
            }
         }
      }
}
```
{: codeblock}


## Configure o sistema de aprendizado contínuo para o modelo publicado

Nesta subseção, você aprenderá como configurar o sistema de aprendizado contínuo para seu modelo.

### Preparar o cabeçalho de autorização

Para preparar o cabeçalho de autorização que combina o token do Watson Machine Learning e as credenciais
da instância do Spark, forneça os seguintes detalhes:

*  O token de acesso criado na etapa anterior
*  As credenciais de serviço do Spark, que podem ser localizadas na guia
Credenciais de serviço do painel de serviço do Bluemix Spark. Antes de fazer a solicitação de implementação,
as credenciais do Spark devem ser codificadas como base64. Elas são transmitidas no cabeçalho da solicitação
no campo X-Spark-Service-Instance.

   Dependendo do sistema operacional que você está utilizando, um dos seguintes
comandos de terminal deve ser emitido para executar codificação base64 e designá-la à variável de ambiente.

   No sistema operacional macOS, use o comando a seguir:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64)
   ```
   {: codeblock}

   Em sistemas operacionais Microsoft Windows ou Linux, deve-se usar o parâmetro
`--wrap=0` com o comando `base64` para executar a codificação base64:

   ```
   spark_credentials=$(echo '{"credentials": {"tenant_id": "s068-ade10277b64956-05b1d10fv12b","tenant_id_full": "00fd89e6-8cf2-4712-a068-ade10277b649_41f37bf2-1b95-4c65-a156-05b1d10fb12b","cluster_master_url": "https://spark.bluemix.net","instance_id": "00fd89e6-8cf2-4712-a068-ade10277b649","tenant_secret": "c74c37cf-482a-4da4-836e-f32ca26ccbb9","plan": "ibm.SparkService.PayGoPersonal"},"version": "2.0"}' | base64 --wrap=0)
   ```
   {: codeblock}


### Preparar o conjunto de dados de feedback

O Learning System requer conexão com os dados de treinamento (dados usados no treinamento de
modelo) e também com os dados de feedback (dados que serão usados para avaliar o modelo treinado). Use a
instrução abaixo para preparar a tabela **DRUG_FEEDBACK_DATA** no **Db2
Warehouse on Cloud**.

- Crie uma instância do
[Db2 Warehouse on Cloud
Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (um plano de entrada é oferecido).
- Crie a tabela **DRUG_FEEDBACK_DATA** no **Db2 Warehouse on
Cloud**.
  + Faça download do arquivo
[drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv)
por meio do repositório Git.
  + Clique em **Abrir o console** para iniciar com o ícone **Db2 Warehouse
on Cloud**.
  + Selecione **Carregar dados** e o tipo de carregamento **Área de
trabalho**.
  + **Arraste e solte** o arquivo transferido por download anteriormente e pressione
**Avançar**.
  + Selecione **Esquema** para importar dados e clique em **Nova
tabela**.
  + No campo **Nova tabela**, digite um nome e clique em
**Avançar**.
  + Use um ponto e vírgula (;) para o **Separador de campo**.
  + Clique em **Avançar** para criar a tabela com os dados transferidos por upload.

**Nota**: é possível incluir novos registros de feedback no banco de dados de
feedback usando o
[Terminal
da API de REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

### Preparar a carga útil de configuração

Para especificar a configuração de aprendizado, é necessário usar o terminal a seguir:

```
https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```
   {: codeblock}


Defina os valores dos seguintes campos para finalizar a carga útil:

* `min_feedback_data_size` - este é o número mínimo de registros no conjunto de dados
de feedback para iniciar a iteração do sistema de aprendizado contínuo
* `auto_retrain` [nunca, sempre, condicionalmente] - este parâmetro especifica
quando o processo de novo treinamento deve ser acionado. [condicionalmente] acionará o processo de novo treinamento
quando a qualidade do modelo estiver abaixo do limite especificado.
* `auto_redeploy` [nunca, sempre, condicionalmente] - este parâmetro especifica
quando o modelo treinado novamente deve ser implementado. [condicionalmente] acionará a reimplementação do modelo
quando a qualidade do modelo recém-treinado for melhor que a de um modelo implementado atualmente.


Exemplo de solicitação:

```
curl -v -X PUT \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer $token" \
    -H "X-Spark-Service-Instance: $spark_credentials" \
    -d '{
          "definition": {
            "method": "binary",
            "metrics": [
              {
                "name": "areaUnderROC",
        "threshold": 0.8
      }
            ]
          },
          "feedback_data_ref": {
           "connection": {
            "db": "BLUDB",
            "host": "awh-yp-small02.services.dal.bluemix.net",
            "username": "dash102204",
            "password": "NweTlYwPY6cu"
           },
    "source": {
            "tablename": "DRUG_FEEDBACK_DATA",
            "type": "dashdb"
           }
          },
          "min_feedback_data_size": 100,
          "auto_retrain": "conditionally",
          "auto_redeploy": "conditionally",
          "schedule": {
            "expression": "0/15 * * * * ? *",
            "start": "2017-02-01T10:11:12Z",
            "until": "2017-06-01T10:11:12Z"
          },
          "last_training_record": 0
        }' \
    https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_configuration
```

{: codeblock}

Exemplo de saída:
```
{
   "min_feedback_data_size":100,
   "auto_retrain":"conditionally",
   "schedule":{
      "expression":"0/15 * * * * ? *",
      "start":"2017-02-01T10:11:12Z",
      "until":"2017-06-01T10:11:12Z"
   },
   "definition":{
      "method":"binary",
      "metrics":[
         {
            "name": "areaUnderROC",
        "threshold": 0.8
      }
      ]
   },
      "spark_service":{
      "credentials": {
         "tenant_id":"s971-2eeb9ffe2a3090-35c9a7ecf27a",
         "cluster_master_url":"https://spark.bluemix.net",
         "tenant_id_full":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30_4c55eb1c-d6fe-4f0a-9390-35c9a7ecf27a",
         "tenant_secret":"5e7fc568-e94e-4689-b623-fe62e9ceedd2",
         "instance_id":"55f1492d-b385-4fdd-b971-2eeb9ffe2a30",
         "plan":"ibm.SparkService.PayGoPersonal"
      },
         "version":"2.0"
   },
   "feedback_data_ref":{
      "connection": {
         "db":"BLUDB",
         "host":"awh-yp-small02.services.dal.bluemix.net",
         "username":"dash102204",
         "password":"NweTlYwPY6cu"
      },
      "source":{
         "tablename":"DRUG_FEEDBACK_DATA",
         "type":"dashdb"
      }
   },
   "auto_redeploy":"conditionally"
}
```
{: codeblock}

**Nota**: nesse exemplo, foram usados os valores padrão para os parâmetros
`auto_retrain` e `auto_redeploy`. Mais informações sobre esses parâmetros
podem ser localizadas aqui na
[Documentação
da API de REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/put_v3_wml_instances_instance_id_published_models_published_model_id_learning_configuration) para o parâmetro learning_configuration.

## Executar iteração do sistema de aprendizado contínuo

Para iniciar a iteração do sistema de aprendizado, use o método da API de REST mostrado abaixo. O modelo
publicado será avaliado dentro da iteração. Se a precisão avaliada estiver abaixo do modelo de limite
especificado, o novo treinamento será acionado. Os conjuntos de dados treinamento e feedback são usados para
novo treinamento e avaliação.

Exemplo de solicitação:

```
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Exemplo de saída:

```
A solicitação foi preenchida e resultou em um novo recurso que
está
sendo criado.
```
{: codeblock}

Para verificar o status da iteração, emita a seguinte solicitação:

Exemplo de solicitação:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/learning_iterations
```
{: codeblock}

Exemplo de saída:

```
{
   "count":1,
   "resources":[
      {
         "metadata" : {
            "guid":"4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908/learning_iterations/4091f245-0f0b-42c6-aec9-6ab68185c47f",
            "created_at":"2017-07-07T11:18:46.742Z",
            "modified_at":"2017-07-07T11:18:48.100Z"
         },
   "entity":{
            "stage":"StartingKernel",
            "published_model":{
               "url":"https://ibm-watson-ml-dev.stage1.mybluemix.net/v3/wml_instances/87452a37-6a8f-4d59-bf88-59c66b5463e4/published_models/9894c3d5-e923-4544-9a7c-2fdb3e4d0908",
               "guid":"9894c3d5-e923-4544-9a7c-2fdb3e4d0908"
            },
            "status":"RUNNING",
            "kernel_id":"db56fc3b-a200-4455-aa70-392aa8ae98b3",
            "spark_service":{
               "credentials": {
                  "tenant_id":"s702-faa29053b44952-01f17dcd4c8c",
                  "cluster_master_url":"https://spark.stage1.bluemix.net",
                  "tenant_id_full":"81d716eb-3c8c-40ef-9702-faa29053b449_a2485898-8ed5-43df-8352-01f17dcd4c8c",
                  "tenant_secret":"9f18945c-8e4b-4d2b-8104-f429b27a896d",
                  "instance_id":"81d716eb-3c8c-40ef-9702-faa29053b449",
                  "plan":"ibm.SparkService.PayGoPersonal"
               }, "version": "2.0"}
         }
      },
   ]
}
```
{: codeblock}

Também é possível obter a lista de métricas e valores de avaliação emitindo a seguinte solicitação:

Exemplo de solicitação:

```
curl -X GET --header "Content-Type: application/json" --header "Accept: application/json" --header "Authorization: Bearer $token" https://ibm-watson-ml.mybluemix.net/v3/wml_instances/{instance_id}/published_models/{published_model_id}/evaluation_metrics
```
{: codeblock}

Exemplo de saída:

```
{
  "count": 1,
  "resources": [
    {
      "phase": "training",
      "values": [
        {
          "name": "areaUnderROC",
          "value": 0.94,
          "threshold": 0.8
        }
      ],
      "timestamp": "2017-08-08T10:11:12.000Z",
      "artifactVersionHref": "https://ibm-watson-ml.mybluemix.net/v3/artifacts/models/361d0edb-c5c9-4b8c-b353-d968e7dc0b8d/versions/8dfe9548-57ec-4768-8d3e-6c1e7e5cdfc3"
    }
  ]
}
```
{: codeblock}
