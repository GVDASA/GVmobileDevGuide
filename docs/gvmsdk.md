# Usando o GVMSDK

O GVMSDK é o nosso pacote NPM para auxiliar no desenvolvimento de novas features para o GVmobile de maneira rápida. Com este pacote instalado podemos executar comandos como enviar uma feature ao portal GVmobile [(upload)](#upload), publicar suas features para produção [(publish)](#publish), preparar suas features para testes [(test)](#build--test), preparar a versão de produção de um cliente [(build)](#build--test), verificar o status de um preparo de teste ou produção [(status)](#status) e ainda preparar um ambiente simulado com as features locais no desenvolvedor [(serve)](#serve).

**Execução básica**

```bash
$ gvmsdk <comando> [opções]
```

## Comandos

Abaixo os comandos e suas opções.

### upload

Faz o upload de uma feature para build ou teste.

#### Opções

* featureFolder
  * Pasta onde esta sua feature. Se omitir este valor, é necessário estar dentro da pasta onde se encontra sua feature.
* --test
  * Faz o upload e marca como "em teste", para ser homologada pelo desenvolvedor.
* --alias=""
  * Parametro obrigatório quando não existe a opção *alias* no arquivo [feature.json](features.md#featurejson).

#### Modo de uso

* Apenas enviando uma feature que esta na pasta "mediaAlunos":
  * `gvmsdk upload ./mediaAlunos`
* Enviando uma feature que esta na pasta "mediaAlunos" e marcando para testes:
  * `gvmsdk upload ./mediaAlunos --test`


### publish

Faz o publish de uma feature para uso em produção.

#### Opções

* featureFolder
  * Pasta onde esta sua feature. Se omitir este valor, é necessário estar dentro da pasta onde se encontra sua feature.
* --cowner=""
  * É o código do cliente que receberá a feature. Usado na primeira vez em que publicamos uma nova feature. Ele pode ser obtido no [portal do desenvolvedor](portal_desenvolvedor.md).
* --mode=0
  * É o tipo de licenciamento que uma feature pode ter. Este valor não pode ser alterado no futuro. Os valores possíveis são:
    * 0 (Privada): Licenciada somente para uso do cliente.
    * 1 (Licenciada): São features desenvolvidas pela GVDASA, uso exclusivo.
    * 2 (Pública): São features que podem ser usadas por todos os clientes GVmobile.

#### Modo de uso

* Publicando uma feature
  * `gvmsdk publish ./mediaAlunos --cowner="498b9d58-0960-441a-8be5-86905af2e78a" --mode=0`
* Publicando uma feature já publicada anteriormente
  * `gvmsdk publish ./mediaAlunos`

### build / test

* `build`: Inicia o build de produção de uma aplicação.
* `test`: Inicia o build de testes de uma aplicação para o desenvolvedor.

#### Opções

* packageId
  * É o ID do aplicativo. Pode ser obtido no [portal do desenvolvedor](portal_desenvolvedor.md).

#### Modo de uso

* Gerando um build de produção
  * `gvmdsk build br.com.gvdasa.gvmobile.meucliente`
* Gerando um teste
  * `gvmdsk test br.com.gvdasa.gvmobile.meucliente`

### status

Verifica o status do build, tanto o de produção, quanto o de testes.

#### Opções

* packageId
  * É o ID do aplicativo. Pode ser obtido no [portal do desenvolvedor](portal_desenvolvedor.md).
* --test
  * Visualiza o status do ultimo build de testes

#### Modo de uso

* Obtendo o status do seu ultimo build de produção
  * `gvmdsk status`
* Obtendo o status do seu ultimo build de teste
  * `gvmdsk status --test`

### serve

Inicia um servidor para testes de features.

#### Opções

Não há

#### Modo de uso

* Iniciando o servidor com o conteúdo da pasta local
  * `gvmsdk serve`
