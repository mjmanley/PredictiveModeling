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

# Política de cotas

O IBM Watson Machine Learning Engine impõe cotas basicamente por instância para assegurar alocação e
uso apropriados de recurso. Essas políticas variam de acordo com os perfis da conta, com o uso de serviço
histórico e com a disponibilidade de recursos. A política de cotas descreve os limites que não são definidos
pelo plano de precificação e que **estão sujeitos a mudanças sem aviso prévio**. 

Os seguintes limites de cota de serviço estão atualmente ativos.

## Uso do Recurso

Os recursos são limitados aos seguintes valores máximos:

-  **Máximo de modelos publicados**: 200 (plano Livre), 1.000 (planos Standard
e Professional)
-  **Tamanho máximo de modelo do Spark ML**: 200 MB
-  **Máximo de modelos implementados**: 1.000 (planos Standard e Professional)

**Nota**: para entender os limites do Plano Livre, consulte a descrição do
[Plano Livre](https://console.bluemix.net/catalog/services/machine-learning) no
[Catálogo do Bluemix](https://console.bluemix.net/catalog/).

## Limites de solicitação de serviço

Você está limitado ao número de solicitações que podem ser feitas por minuto para APIs específicas. Se
seu aplicativo precisar de limites mais altos, você deverá [entre em contato
com o Suporte do IBM Bluemix](https://support.ng.bluemix.net/) para aumentar a cota.

## Solicitações de implementação

Os seguintes limites se aplicam às solicitações da API de implementação:

-  **Período**: 60 segundos
-  **Limite padrão**: 10

## Solicitações de predição on-line

Os seguintes limites se aplicam às solicitações de
[predições on-line](pm_service_api_spark_building.html):

-  **Período**: 60 segundos
-  **Limite padrão**: 500

## Solicitações de gerenciamento de recurso

Os seguintes limites se aplicam ao total de solicitações combinadas nesta lista:

[Token](https://watson-ml-api.mybluemix.net/#/Token): solicitações de post, get, delete,
put, patch

[Implementações](https://watson-ml-api.mybluemix.net/#/Deployments): solicitações
de post, get, delete, put, patch 

-  **Período**: 60 segundos
-  **Limite padrão**: 100
