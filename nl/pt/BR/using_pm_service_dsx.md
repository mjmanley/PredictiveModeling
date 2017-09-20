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

Observe as informações importantes a seguir sobre o serviço do Machine Learning.

## Etapas para ligar o serviço ao aplicativo Bluemix

É possível fazer download do
[código de
amostra](https://github.com/pmservice/product-line-prediction/blob/master/README.md) do Node.js para tentar o serviço do Machine Learning. Conclua as etapas a seguir para criar seu
aplicativo Bluemix e ligar o serviço Machine Learning. Estes exemplos usam Node.js, por ele ser um tempo
de execução popular. Outros podem ser usados como
iOS, Ruby, Perl ou Java.

Observe que também é possível executar as etapas 1-3 usando a Interface gráfica do Bluemix em vez da ferramenta Cloud Foundry (cf).

1. Use o comando `cf create-service` para criar uma instância de serviço:

   ```
   cf create-service pm-20 Free {local naming}
   ```
   {: codeblock}

   Por exemplo:

   ```
   cf create-service pm-20 Free my_wml_free
   ```
   {: codeblock}

   Esse comando cria uma instância de serviço do Machine Learning com o plano livre chamado
`my_wml_free` em seu espaço do Bluemix.

2. Use o comando `cf create-service-key` para criar credenciais de serviço:

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

3. Use o comando cf bind-service para ligar a instância de serviço `my_wml_free`
ao seu aplicativo.

   ```
   cf bind-service {AppName} my_wml_free
   ```
   {: codeblock}

   Por exemplo:

   ```
   cf bind-service my_app1 my_wml_free
   ```
   {: codeblock}

   Este comando liga a instância de serviço do Machine Learning `my_wml_free`
ao aplicativo Bluemix `my_app1`.



## Credenciais do Machine Learning

Depois que você liga a instância de serviço de Machine Learning ao
aplicativo Bluemix, as credenciais do Machine Learning são
incluídas na variável de ambiente `VCAP_SERVICES`:

```
    {
     "pm-20-dev": [
       {
         "credentials": {
           "url":
           "https://ibm-watson-ml.mybluemix.net",
           "access_key": "**********",
           "username": "**********",
           "password": "**********",
           "instance_id": "**********"
         },
           "label": "pm-20-dev",
           "plan": "Free",
           "name": "IBM Watson Machine Learning”
       }
     ]
    }
```
{: codeblock}

   A variável de ambiente `VCAP_SERVICES` inclui as informações a seguir:

   * `plan` - o plano do Machine Learning que é usado no fornecimento do serviço.
   * `url` - o endereço da instância de serviço do Machine Learning.
   * `access_key` - somente para os fluxos SPSS Modeler.
   * `instance_id` - identificador exclusivo da instância do Machine Learning.
   * `username`, `password` - autorização básica necessária para gerar
um token de acesso para transmitir todas as solicitações para esta instância de serviço. Por exemplo, é possível gerar um token de acesso usando um curl como este:

Exemplo de solicitação:

```
       curl --basic --user {username}:{password} https://ibm-watson-ml.mybluemix.net/v3/identity/token

       Exemplo de saída:

       {"token":"**********"}
```
{: codeblock}

   O código do Node.js a seguir é um exemplo de como obter o nome de usuário e a senha por meio da
variável de ambiente `VCAP_SERVICES`:

```
   if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var credentials = env['pm-20'][0].credentials;
        var username = credentials.username;
        var password = credentials.password;
        var instance_id = credentials.instance_id;
    }
```
{: codeblock}
