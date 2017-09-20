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

# Estruturas de aprendizado por máquina suportadas

O serviço do IBM Watson Machine Learning suporta as seguintes estruturas para desenvolvimento e
validação de modelo como parte do gerenciamento do ciclo de vida do modelo.


## Spark MLlib
Há suporte para o Spark MLlib para o serviço de implementação e pontuação Batch (beta) e Stream (beta)
on-line do Watson Machine Learning. Somente versões e ambientes de tempo de execução específicos são suportados.

### Versões suportadas
*  Spark 2.0

### Restrições:

  *  Somente modelos de classificação e de regressão são suportados.
  *  Os modelos que contêm referências a transformadores customizados, funções definidas pelo usuário
e classes não são suportados.
  * O terminal "schema" retornado durante a solicitação de implementação do modelo scikit-learn
não é suportado neste estágio.
  *  O suporte em lote e de fluxo para modelos do Spark está em beta. Se estiver interessado em
participar, inclua-se na [lista de espera](https://www.ibm.biz/mlwaitlist)!
  * O sistema de aprendizado contínuo para modelos Spark está em beta. Se estiver interessado em
participar, inclua-se na [lista de espera](https://www.ibm.biz/mlwaitlist)!

## Scikit-learn
Há suporte para scikit-learn para o serviço de implementação e pontuação on-line do Watson Machine
Learning. Somente versões e ambientes de tempo de execução específicos são suportados.

### Versões suportadas

- Tempo de execução do Anaconda 4.2.x for Python 3.5
- Scikit-Learn 0.17

### Tempo de execução Python

O tempo de execução Python para modelos que precisam ser implementados usando o serviço de implementação
e pontuação on-line do WML é o Python 3.5.

Em alguns casos, em que modelos foram criados no tempo de execução Python 2.7, a
implementação pode falhar devido a incompatibilidades entre o Python 2.7 e o Python 3.5.

### Pacotes Python suportados

Uma lista de pacotes Python suportados pelo serviço de implementação
e pontuação on-line do WML pode ser localizada [aqui](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrições

Há algumas restrições, que podem incluir algumas ou todas as limitações a seguir:

* Somente modelos de classificação e de regressão são suportados.
* Os modelos podem conter referências somente a esses pacotes (e à versão do pacote) suportados pelo
tempo de execução do Anaconda 4.2.x for Python 3.5.
* O terminal "schema" retornado durante a solicitação de implementação não está implementado.
* A probabilidade de predição não é retornada como uma resposta de solicitação de pontuação neste
estágio.
* Os modelos que requerem o Pandas Dataframe como o tipo de entrada para a API "predict()" não são
suportados.
* Os modelos que contêm referências a transformadores customizados, funções definidas pelo usuário e
classes não são suportados.

## XGBoost <span class='tag--beta'>Beta</span>
Há suporte para XGBoost para o serviço de implementação e pontuação on-line do Watson Machine Learning.
Somente versões e ambientes de tempo de execução específicos são suportados.

### Versões suportadas

- XGBoost 0.6
- Tempo de execução do Anaconda 4.2.x for Python 3.5
- Scikit-Learn 0.17

### Tempo de execução Python

O tempo de execução Python para modelos que precisam ser implementados usando o serviço de implementação
e pontuação on-line do WML é o Python 3.5.

Em alguns casos, em que modelos foram criados no tempo de execução Python 2.7, a implementação pode
falhar devido a incompatibilidades entre o Python 2.7 e o Python 3.5.

### Pacotes Python suportados

Uma lista de pacotes Python suportados pelo serviço de implementação e pontuação on-line do WML pode ser
localizada [aqui](https://docs.continuum.io/anaconda/packages/old-pkg-lists/4.2.0/py35).

### Restrições

Há algumas restrições, que podem incluir algumas ou todas as limitações a seguir:
* O suporte do XGBoost está atualmente disponível para modelos criados usando wrappers Scikit-Learn
do XGBoost, por exemplo, xgboost.sklearn.XGBClassifier e xgboost.sklearn.XGBRegressor.
* Os modelos podem conter referências somente a esses pacotes (e à versão do pacote) suportados
pelo tempo de execução do Anaconda 4.2.x for Python 3.5.
* O terminal "schema" retornado durante a solicitação de implementação não está implementado.
* A probabilidade de predição não é retornada como uma resposta de solicitação de pontuação neste
estágio.
* Os modelos que contêm referências a transformadores customizados, funções definidas pelo usuário e
classes não são suportados.

## SPSS Modeler

Há suporte para fluxos do SPSS Modeler para o serviço de implementação e pontuação em lote on-line do
Watson Machine Learning. Somente versões e ambientes de tempo de execução específicos são suportados.

### Versões suportadas

*  SPSS Modeler 17.1
*  SPSS Modeler 18.0

### Restrições

As seguintes restrições existem para os fluxos do SPSS Modeler:

*  Quando uma ramificação de pontuação é preparada para uso em pontuação em tempo
real, os dados de entrada vindos da solicitação de escore devem substituir o nó de origem
projetado na ramificação de pontuação e a saída da análise preditiva resultante deve
fluir de volta para o fluxo de resposta (substituindo efetivamente o nó terminal no
design de ramificação de pontuação).
*  Conforme a ramificação de pontuação é preparada para execução em tempo real no
Bluemix, ela não pode requerer uma conexão com um serviço externo. Por exemplo, um design
de ramificação de pontuação do IBM Analytical Decision Management não pode conter
referências a regras ou modelos armazenados em um repositório do IBM SPSS Collaboration
and Deployment Services.
*  A execução de uma ramificação de pontuação para pontuação em tempo real no Bluemix
não pode requerer um serviço externo. Por exemplo, não é possível implementar e pontuar
com relação a algoritmos de modelo que exijam um armazenamento de dados IBM SPSS
Analytic Server e Apache Hadoop em tempo real.
*  O Machine Learning suporta o script Python integrado do Modeler. Há algumas restrições em razão do método usado para
processar fluxos antes que eles sejam executados no Machine Learning. Normalmente, se
um usuário optar pelo controle da execução do fluxo, eles referenciarão o nó terminal da
ramificação. Para o Machine Learning, quando processamos o fluxo, identificamos
os nós do JSON que serão substituídos e, em seguida, executamos a
substituição antes que o fluxo seja executado. Isso faz com que o
fluxo falhe no script porque os nós de entrada e exportação referenciados não existem mais. A
solução é usar o ID de outro nó para identificar exclusivamente a ramificação durante a
execução. Isso assegura que o fluxo seja executado conforme definido no script Python
integrado.

## Saiba mais

Para obter mais detalhes sobre o suporte atual para modelos preditivos treinados pelo IBM SPSS Analytic
Server, consulte a seção [SPSS Analytic
Server](https://www.ibm.com/support/knowledgecenter/SSWLVY) do [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/).
