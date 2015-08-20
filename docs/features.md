# Desenvolvimento de novas features

A plataforma para desenvolvimento de novas features é uma forma de criar ou extender funcionalidades no aplicativo GVmobile.

## Requisitos para o desenvolvimento

Para o desenvolvimento é necessário ser convidado por uma instituição cliente da GVDASA usuário do GVmobile, para ter o acesso ao [Portal de Desenvolvimento GVmobile](https://painel.gvmobile.net.br/)

Para desenvolver novas features, é necessário um conhecimento prévio de **JavaScript**, **CSS** e **HTML5**. Alem destes, é necessário conhecimentos em:

* [AngularJS](https://angularjs.org/)
* [Ionic Framework](http://ionicframework.com/)

E como conhecimento opcional:

* [SASS](http://sass-lang.com/)

Alem destes conhecimentos, é necessário ter instalado um ambiente de desenvolvimento com os seguintes requisitos:

* [Node.JS e NPM](https://nodejs.org/)

Após este requisito instalado, podemos obter o ```gvmsdk``` via NPM:

```bash
$ npm install -g gvmsdk
```

## Desenvolvendo uma feature

Para desenvolver uma feature, é necessário o download de nosso CORE SDK. Como sugestão temos os seguintes passos:

```bash
$ mkdir minhasFeatures
$ cd minhasFeatures
$ git clone $GITCORE core
$ git clone $GITALUNO aluno.modulo
$ git clone $GITHELLOWORLD feature.helloWorld
```

Na pasta **core** temos a API desenvolvida em nosso aplicativo, usada para levantar o ambiente básico e testar sua nova feature, a pasta **aluno.modulo** contem a implantação do core para o módulo aluno. A pasta **feature.helloWorld** é nossa feature de exemplo (por tanto opcional).

Para testes, você deve levantar o serviço web do **gvmsdk**, dentro da pasta de desenvolvimento (em nosso exemplo a pasta **minhasFeatures**):

```
$ gvmsdk serve
```

Ele irá levantar um servidor web no endereço http://localhost:3000 e sugerimos usar o [Google Chrome](https://www.google.com/chrome/) com as opções de desenvolvedor (F12), pois esta opção fornece meios de debug e emular dispositivos móveis.

## Anatomia de uma feature

Uma feature terá a seguinte estrutura de arquivos:

* [feature.json](#featurejson)
* [helloWorld.module.js](#helloWorldmodulejs)
* [helloWorld.controller.js e helloWorld.service.js](#helloWorldservicejsehelloWorldservicejs)
* [helloWorld.html e helloWorld2.html](#helloWorldhtmlehelloWorld2html)
* [helloWorld.sass](#helloWorldsass)

### feature.json

```json
{
    "id": "GUID",
    "cowner": "GUID",
    "mode": 0,
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

* *id*: Código de identificação de uma feature. Esta propriedade é gerada automaticamente quando usando o *gvmsdk* para envio, ou deve ser obtido pelo no **portal do desenvolvedor**.
* *cowner*: Código identificando o cliente que é proprietário da feature. É um campo automático quando usando o *gvmsdk* para publicar uma feature, ou deve ser obtido no **portal do desenvolvedor**.
* *mode*: Modo de licencimento da feature. Deve ser preenchido conforme tipo de licenciamento:
	* 0: Privado (Uso somente pelo cliente)
	* 1: Licenciado (Features licenciados **somente pela GVDASA**)
	* 2: Público (Features disponíveis para todos os clientes)
* *scripts*: Array que recebe todos os arquivos **Javascript** usados pela feature.
* *styles*: Array que recebe todos os arquivos **CSS** e **SASS** usados pela feature.
* *bower_deps*: Array que recebe pacotes adicionais que devem ser instalados via bower.
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

## Links úteis

* Comandos do [gvmsdk](#)
* [Portal do desenvolvedor](#)
* [GVmobile Core API](#)
* [GVmobile WebAPI](#)
