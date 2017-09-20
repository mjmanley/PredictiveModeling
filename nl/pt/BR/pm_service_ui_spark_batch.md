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

# Implementando modelos em lote <span class='tag--beta'>Beta</span>

**Nota**: essa funcionalidade no momento está em beta e disponível somente
para uso com o Spark MLlib. Se estiver interessado em participar, inclua-se na lista de espera! Para obter mais informações, veja: [https://www.ibm.biz/mlwaitlist](https://www.ibm.biz/mlwaitlist).

**Nome do cenário**: predição de satisfação do cliente.

**Descrição do cenário**: uma empresa de telecomunicações quer saber
quais clientes estão prestes a sair. O modelo apresentado prevê a perda de
clientes. Um cientista de dados desenvolve um modelo preditivo e o compartilha com você
(o desenvolvedor). Sua tarefa é implementar
o modelo e gerar análise preditiva fazendo solicitações de
pontuação em relação ao modelo implementado.

## Usando o modelo de amostra

1.  Acesse a guia Amostras do Painel IBM® Watson™ Machine
Learning.

2.  Na seção Modelos de amostra, localize o quadro Predição de
satisfação do cliente e clique no botão Incluir modelo (+).

Agora você verá o modelo de amostra Predição de satisfação do cliente
na lista de modelos disponíveis na guia Modelos.

## Criando uma implementação em lote com o Object Storage

1.  Acesse a guia Modelos do Painel do IBM® Watson™ Machine Learning.

2.  No menu **Ações**, clique em **Criar implementação**.

3.  No formulário Criar implementação, forneça o Nome, a Descrição e o Tipo de lote.

4.  Deve-se fornecer as seguintes entradas:

    **Conexão de entrada**: os detalhes do armazenamento de objetos que serão
usados como entrada (dados do cliente para pontuação) para o modelo e o armazenamento para a saída do modelo
(neste caso, results.csv, que é criado automaticamente).

    ```
       {
          "source":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"TelcoCustomerData.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **Conexão de saída**

    ```
       {
          "target":{
             "fileformat":"csv",
      "firstlineheader":"true",
      "container":"batchjob",
      "inferschema":"1",
      "filename":"result.csv",
      "type":"bluemixobjectstorage"
          },
          "connection":{
             "projectid":"252341ed707d4558b5b2da245e785cd7",
             "userid":"b2d83cf6056e040ddb91ca00a2686c7d3",
             "region":"dallas",
             "authurl":"https://identity.open.softlayer.com",
             "password":"eJ_y9R^OE{j?8Ub!!"
          }
       }
    ```
    {: codeblock}

    **Conexão do Spark**: credenciais de serviço do Spark podem ser
localizadas na guia Credenciais de serviço do painel de serviço do Bluemix Spark.

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

5.  Clique em **Salvar**.

O resultado da predição é salvo em um arquivo .csv no IBM Object
Storage. Segue uma linha de amostra.

Visualização de arquivo de entrada:

```
customerID,gender,SeniorCitizen,Partner,Dependents,tenure,PhoneService,MultipleLines,InternetService,OnlineSecurity,OnlineBackup,DeviceProtection,TechSupport,StreamingTV,StreamingMovies,Contract,PaperlessBilling,PaymentMethod,MonthlyCharges,TotalCharges,Churn
7590-VHVEG,Female,0,Yes,No,1,No,No phone service,DSL,No,Yes,No,No,No,No,Month-to-month,Yes,Electronic check,29.85,29.85,No
5575-GNVDE,Male,0,No,No,34,Yes,No,DSL,Yes,No,Yes,No,No,No,One year,No,Mailed check,56.95,1889.5,No
3668-QPYBK,Male,0,No,No,2,Yes,No,DSL,Yes,Yes,No,No,No,No,Month-to-month,Yes,Mailed check,53.85,108.15,Yes
```
{: codeblock}

Visualização do arquivo de saída:

```
InternetService, Contract, tenure, MonthlyCharges, Churn
Fiber optic, Month-to-month, 2, 70.7, 1
DSL, Two year, 58, 59.9, 0
DSL, Month-to-month, 1, 30.2, 1
DSL, Month-to-month, 17, 64.7, 1
DSL, Month-to-month, 13, 76.2, 0
DSL, Month-to-month, 25, 69.5, 1
Fiber optic, Month-to-month, 8, 80.65, 1
No, One year, 52, 20.4, 0
Fiber optic, Two year, 64, 111.6, 0
Fiber optic, Month-to-month, 1, 79.35, 1
```
{: codeblock}


## Obtendo detalhes da implementação

É possível verificar o status e os parâmetros relacionados ao modelo implementado.

1. Acesse a guia Implementações do Painel do IBM® Watson™ Machine
   Learning.

2. No menu AÇÕES, selecione Visualizar detalhes.


## Excluindo uma implementação em lote

É possível excluir a implementação, se ela não é mais
necessária, usando uma consulta como a amostra a seguir.

1. Acesse a guia Implementações do Painel do IBM® Watson™ Machine
   Learning.

2. No menu AÇÕES, selecione Excluir.
