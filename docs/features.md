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

* [Git](https://git-scm.com/)
* [Node.JS e NPM](https://nodejs.org/)
* Um editor de códigos de sua preferência :)

Após instalados estes requisitos, podemos obter o ```gvmsdk``` via NPM:

```bash
$ npm install -g gvmsdk
```

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

```
$ gvmsdk serve
```

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
* *bower_deps*: Array que recebe uma lista de dependências para ser instalado via bower. Para saber a lista de pacotes possiveis, acesse (este link)[feature_bower_deps.md].
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
