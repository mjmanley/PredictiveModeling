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

O sistema de aprendizado contínuo do IBM® Watson™ Machine Learning fornece monitoramento automatizado de
desempenho, novo treinamento e reimplementação do modelo para assegurar a qualidade da predição.

**Nome do cenário**: bons medicamentos para seleção de tratamento cardíaco.

**Descrição do cenário**: uma empresa biomédica que produz remédios para o coração
deseja implementar um modelo que seleciona o melhor medicamento para tratamento cardíaco. Quando surge uma
nova evidência na eficácia de medicamento, uma atualização do modelo deve ser considerada. Um cientista de
dados prepara um modelo preditivo e o compartilha com você (o desenvolvedor). Sua tarefa é implementar o
modelo, definir a configuração do aprendizado e executar a iteração do aprendendo para avaliar, treinar novamente e reimplementar o modelo.

## Usando o modelo de amostra

1. Acesse a guia Amostras do Painel IBM® Watson™ Machine
Learning.

2. Na seção Modelos de Amostra, localize o ladrilho Seleção de Medicamento do Coração e clique no
botão Incluir modelo (+).

Agora você verá o modelo de amostra Seleção de Medicamento do Coração na lista de modelos
disponíveis na guia Modelos.


## Configure o sistema de aprendizado contínuo para o modelo publicado

1.  Acesse a guia Modelos do Painel do IBM® Watson™ Machine Learning.

2.  No menu **Ações**, clique em **Visualizar detalhes**.

3.  Role para baixo até **Detalhes do novo treinamento** e pressione
**Editar**.

4.  Deve-se fornecer as seguintes entradas:

    **Conexão de feedback**: detalhes do Db2 Warehouse on Cloud, que serão
usados como entrada (dados de feedback) para a avaliação e novo treinamento do modelo.
    
    ```
    {
        "connection": {
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

    Use as instruções a seguir para preparar a tabela `DRUG_FEEDBACK_DATA` no
Db2 Warehouse on Cloud.
    - Crie uma instância do
[Db2
Warehouse on Cloud Service](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud/) (um plano de entrada é oferecido).
    - Crie a tabela **DRUG_FEEDBACK_DATA** no **Db2 Warehouse on
Cloud**.
      + Faça download do arquivo
[drug_feedback_data.csv](https://raw.githubusercontent.com/pmservice/wml-sample-models/master/spark/drug-selection/data/drug_feedback_data.csv)
por meio do repositório Git.
      + Clique em **Abrir o console** para iniciar com o ícone **Db2 Warehouse
on Cloud**.
      + Selecione **Carregar dados** e o tipo de carregamento **Área de
trabalho**.
      + **Arraste e solte** o arquivo transferido por download anteriormente e
pressione **Avançar**.
      + Selecione **Esquema** para importar dados e clique em **Nova
tabela**.
      + Escreva um nome para **nova tabela** e, em seguida, clique em
**Avançar** para concluir a importação de dados.
      + Use `;` como o **separador de campo**.
      + Clique em **Avançar** para criar a tabela com os dados transferidos por upload.

    **Nota**: é possível incluir novos registros de feedback no banco de dados de
feedback usando o
[Terminal
da API de REST](http://watson-ml-api.mybluemix.net/#!/Published32Models/post_v3_wml_instances_instance_id_published_models_published_model_id_feedback)

    **Tamanho mínimo de dados**: o número mínimo de registros no conjunto de
dados de feedback para iniciar a avaliação do modelo (parte da iteração do sistema de aprendizado).

    ```
    20
    ```
    {: codeblock}

    **Conexão do Spark**: credenciais de serviço do Spark podem ser localizadas na
guia Credenciais de serviço do painel de serviço do Bluemix Spark.

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

    **Limites**: o valor do limite que acionará o processo de novo treinamento (se calculado quando o
valor de métrica de avaliação está abaixo do limite)
    ```
    0.8
    ```

    **Implementar automaticamente o modelo treinado novamente**: implementará o modelo treinado novamente
se sua qualidade (valor de métrica) for melhor que a de um modelo implementado atualmente.
5.  Clique em **Configurar**.


## Executar iteração do sistema de aprendizado contínuo

O modelo publicado será avaliado dentro da iteração. Se a precisão avaliada estiver abaixo do
modelo de limite especificado, o novo treinamento será acionado. Os conjuntos de dados treinamento e
feedback são usados para novo treinamento e avaliação.

1. Para iniciar uma nova iteração, no formulário **Detalhes** do modelo, na
guia **Monitor**, clique em **Avaliar**.

3. Para verificar o resultado da iteração para a tabela Eventos de avaliação ou visualização de
Gráfico. É possível localizar informações sobre a qualidade do modelo calculada com base nos dados de feedback
(monitoramento) e na qualidade do modelo treinado novamente (nova versão do modelo criada e avaliada).

4. Para ver a lista de modelos treinados automaticamente e sua qualidade, acesso o Histórico de versão
localizado na parte inferior da guia Visão geral (Visualizar detalhes-> Visão geral do modelo).
