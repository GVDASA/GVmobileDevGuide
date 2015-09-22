# Desenvolvimento de novas features

A plataforma para desenvolvimento de novas features é uma forma de criar ou extender funcionalidades no aplicativo GVmobile.

## Requisitos para o desenvolvimento

Para o desenvolvimento é necessário ser convidado por uma instituição cliente da GVDASA usuário do GVmobile, para ter o acesso ao [Portal de Desenvolvimento GVmobile](portal_desenvolvedor.md)

Para desenvolver novas features, é necessário um conhecimento prévio de **JavaScript**, **CSS** e **HTML5**. Alem destes, é necessário conhecimentos em:

* [AngularJS](https://angularjs.org/)
* [Ionic Framework](http://ionicframework.com/)

E como conhecimento opcional:

* [SASS](http://sass-lang.com/)

Alem destes conhecimentos, é necessário ter instalado um ambiente de desenvolvimento com os seguintes requisitos:

* [Git](https://git-scm.com/)
* [Node.JS e NPM](https://nodejs.org/)
* Um editor de códigos de sua preferência :)

Após instalados estes requisitos, podemos obter o ```gvmsdk``` via NPM:

```bash
$ npm install -g gvmsdk
```

**Atenção**: O pacote NPM *gvmsdk* é um conjunto de pacotes para facilitar o desenvolvimento de uma feature. Com isso, alguns pacotes podem ocasionalmente apresentar alguma mensagem de "erro" em pacotes opcionais. Isso é considerado normal, e abaixo segue uma lista de erros mapeados e que devem ser desconsiderados:

* Erro na compilação de pacotes ***gulp-sass***
    * Neste erro é comentado na falta do interpretador Python ou Visual Studio 2013, estas dependências são **opcionais**.

## Desenvolvendo uma feature

Para desenvolver uma feature, é necessário o download de nosso CORE SDK. Como sugestão temos os seguintes passos:

```bash
$ mkdir minhasFeatures
$ cd minhasFeatures
$ git clone https://github.com/GVDASA/GVmobileFeature-core.git core
$ git clone https://github.com/GVDASA/GVmobileFeature-alunoModulo.git aluno.modulo
$ git clone https://github.com/GVDASA/GVmobileFeature-HelloWorld.git feature.helloWorld
```

Na pasta **core** temos a API desenvolvida em nosso aplicativo, usada para levantar o ambiente básico e testar sua nova feature, a pasta **aluno.modulo** contem a implantação do core para o módulo aluno. A pasta **feature.helloWorld** é nossa feature de exemplo (por tanto opcional).

Para testes, você deve levantar o serviço web do **gvmsdk**, dentro da pasta de desenvolvimento (em nosso exemplo a pasta **minhasFeatures**):

* Levantando um ambiente para API do desenvolvedor (Não requer que o desenvolvedor tenha vínculo com um cliente)

```
$ gvmsdk serve
```


* Levantando um ambiente para API do cliente (Requer vínculo do desenvolvedor com um cliente)

*(Informe suas credenciais de desenvolvedor)*

```
$ gvmsdk login
``` 

*Obtenha o [packageId do cliente](packageid.md)*

```
$ gvmsdk serve PackageId

Ele irá levantar um servidor web no endereço http://localhost:3000 acessando nossa API de testes. Sugerimos usar o [Google Chrome](https://www.google.com/chrome/) com as opções de desenvolvedor (F12), pois esta opção fornece meios de debug e emular dispositivos móveis.

Para acessar, use um dos usuários e senhas abaixo:

|Usuário|Senha|
|---|---|
|aluno|123|
|responsavel|123|
|professor|123|

## Anatomia de uma feature

Uma feature terá a seguinte estrutura de arquivos:

* [feature.json](#featurejson)
* [helloWorld.module.js](#helloworldmodulejs)
* [helloWorld.controller.js e helloWorld.service.js](#helloworldcontrollerjs-e-helloworldservicejs)
* [helloWorld.html e helloWorld2.html](#helloworldhtml-e-helloworld2html)
* [helloWorld.scss](#helloworldscss)

Para o desenvolvimento, é necessário seguir nossa [Feature Guidelines](features_guidelines.md) para manter a padronização e qualidade do aplicativo.

### feature.json

```json
{
    "scripts": [
        "**/*.module.js",
        "**/*.js"
    ],
    "styles": [
        "**/*.scss"
    ],
    "bower_deps": [],
    "deps": [
        "core"
    ],
    "alias": "HelloWorldTest2"
}
```

JSON de configuração da feature. A relação de propriedades são:

* *scripts*: Array que recebe todos os arquivos **Javascript** usados pela feature.
* *styles*: Array que recebe todos os arquivos **CSS** e **SASS** usados pela feature.
* *bower_deps*: Array que recebe uma lista de dependências para ser instalado via bower. Para saber a lista de pacotes possiveis, acesse [este link](features_bower_deps.md).
* *deps*: Array com as dependencias de features do GVmobile.
* *alias*: Nome da feature

### helloWorld.module.js

Arquivo utilizado para inicializar o módulo angular responsável pela feature. Normalmente ficam neste arquivo as cargas do *run* e *config* da feature.

```javascript
angular.module('feature.helloWorld', ['core'])

.run(function() {
    // implantação que deverá rodar automaticamente quando a feature inicializar
})

.config(function() {
    // implantação de providers
});
```

### helloWorld.controller.js e helloWorld.service.js

Arquivos *opcionais* onde ficam os controllers e serviços da feature.

### helloWorld.html e helloWorld2.html

São arquivos de views.

### helloWorld.scss

Arquivo *opcional* para criação de estilo (CSS)

## Como criar e consumir uma VIEW para consulta de dados através da Web API do cliente.

Para consumir uma VIEW é necessário criá-la na base de dados do cliente seguindo os passos da seguinte documentação
[Web API do cliente](webapi_cliente.md)


## Enviando sua feature para um cliente

Para efetuar o envio, é necessário que seja enviado os arquivos para o portal GVmobile. Este procedimento pode ser feito [usando o portal GVmobile](portal_desenvolvedor.md#envioupload-de-features) ou com o [gvmsdk](#).

## Testando sua feature enviada

Para testar sua feature enviada em modo de teste para um cliente, conheça o [aplicativo em modo desenvolvedor](https://github.com/GVDASA/GVmobileDevGuide/blob/master/docs/aplicativo_desenvolvedor.md).

## Links úteis

* Comandos do [gvmsdk](gvmsdk.md)
* [Portal do desenvolvedor](portal_desenvolvedor.md)
* [GVmobile Core API](http://gvdasa.github.io/GVmobileFeature-core/)
* [Web API do cliente](webapi_cliente.md)
* [OData Version 3.0 - URL Conventions](http://www.odata.org/documentation/odata-version-3-0/url-conventions/)

