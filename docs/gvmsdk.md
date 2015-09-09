# Usando o GVMSDK

O GVMSDK é o nosso pacote NPM para auxiliar no desenvolvimento de novas features para o GVmobile de maneira rápida. Com este pacote instalado podemos executar comandos como enviar uma feature ao portal GVmobile [(upload)](#), publicar suas features para produção [(publish)](#), preparar suas features para testes [(test)](#), preparar a versão de produção de um cliente [(build)](#), verificar o status de um preparo de teste ou produção [(status)](#) e ainda preparar um ambiente simulado com as features locais no desenvolvedor [(serve)](#).

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

#### Modo de uso

* Apenas enviando uma feature que esta na pasta "mediaAlunos":
  * `gvmsdk upload ./mediaAlunos`
* Enviando uma feature que esta na pasta "mediaAlunos" e marcando para testes:
  * `$ gvmsdk upload ./mediaAlunos --test`


featureFolder [--test] [--alias=""]
  publish featureFolder [--cowner=""] [--mode=0]
    Faz o publish de uma feature para uso em produção.
  test packageId
    Inicia o build de testes de uma aplicação para o desenvolvedor.
  build packageId
    Inicia o build de uma aplicação.
  status packageId [--test]
    Verifica o status do build, tanto o de produção, quanto o de testes.
  serve
    Inicia um servidor para testes de features.