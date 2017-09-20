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

# Implementando modelos de fluxo <span class='tag--beta'>Beta</span>

**Nota**: essa funcionalidade no momento está em beta e disponível somente
para uso com o Spark MLlib. Se estiver interessado em participar, inclua-se na lista de espera! Para obter mais informações, veja: [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Nome do cenário**: análise de sentimentos.

**Descrição do cenário**: uma agência de marketing quer saber a
impressão sobre um tópico específico. A agência gostaria que
desenvolvêssemos um modelo que classifique uma instrução fornecida como POSITIVA ou
NEGATIVA. Um Cientista de dados prepara um
modelo preditivo e o compartilha com você (o desenvolvedor). Sua tarefa é implementar
o modelo e gerar análise preditiva fazendo solicitações de
pontuação em relação ao modelo implementado.

Consulte este [documento](https://github.com/pmservice/tweet-sentiment-prediction) para obter mais informações.

## Usando o modelo de amostra

1. Acesse a guia Amostras do Painel IBM® Watson™ Machine
   Learning.
2. Na seção Modelos de amostra, localize o quadro Predição de impressão
   e clique no botão Incluir modelo (+).

Agora você verá a amostra do modelo de Predição de impressão na lista
de modelos disponíveis na guia Modelos.


## Criando uma implementação de fluxo com o IBM Message Hub

1.  Acesse a guia Modelos do Painel do IBM® Watson™ Machine Learning.
2.  No menu AÇÕES, selecione Criar implementação.
3.  No formulário Criar implementação, forneça o Nome, a Descrição e o Tipo de fluxo.
4.  Deve-se fornecer as seguintes entradas:

    **Conexão de entrada**: detalhes de tópicos do IBM Message Hub que são usados como entrada (tweets) para o modelo e armazenamento para a saída de modelo (resultados de predição).

    ```
  {
     "connection":{
        "kafka_brokers_sasl":[
           "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
           "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
           "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
           "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
           "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
        ],
        "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
        "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
        "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
        "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
        "user":"Dv5kEVNNsbuJ9RFE",
        "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
     },
     "source":{
        "topic":"sinput",
        "type":"kafka"
     }
  }
    ```
    {: codeblock}

    **Conexão de saída**

    ```
 {
    "connection":{
       "kafka_brokers_sasl":[
          "kafka01-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka02-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka03-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka04-prod01.messagehub.services.us-south.bluemix.net:9093",
          "kafka05-prod01.messagehub.services.us-south.bluemix.net:9093"
       ],
       "kafka_admin_url":"https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443",
       "api_key":"Dv5kEVNNsbuJ9RFEKdUhIn2hruipIrsBolge6v1uQmTzEQti",
       "mqlight_lookup_url":"https://mqlight-lookup-prod01.messagehub.services.us-south.bluemix.net/Lookup?serviceId=5448397d-cb22-4698-8a2b-ffb04f43a4cb",
       "kafka_rest_url":"https://kafka-rest-prod01.messagehub.services.us-south.bluemix.net:443",
       "user":"Dv5kEVNNsbuJ9RFE",
       "password":"KdahIn2hruipIrsBolge6v1uQmTzEQti"
    },
    "target":{
       "topic":"soutput",
       "type":"kafka"
    }
 }
    ```
    {: codeblock}

    **Conexão do Spark**: credenciais de serviço do Spark podem ser localizadas na guia Credenciais de serviço do painel de serviço do Bluemix Spark.

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

5. Clique em **Salvar**.

O resultado da predição é enviado para o tópico MessageHub definido (conexão de saída).

## Obtendo detalhes da implementação

É possível verificar o status e os parâmetros relacionados ao modelo implementado.

1. Acesse a guia Implementações do Painel do IBM® Watson™ Machine
   Learning.
2. No menu **Ações**, clique em **Visualizar detalhes**.

## Excluindo um fluxo de implementação

É possível excluir a implementação, se ela não é mais
necessária, usando uma consulta como a amostra a seguir.

1. Acesse a guia Implementações do Painel do IBM® Watson™ Machine
   Learning.
2. No menu AÇÕES, selecione Excluir.
