# Features Guidelines

Este é um guia para manter a padronização e qualidade nos códigos da aplicação GVmobile. Todo o desenvolvedor que estiver envolvido no desenvolvimento de uma feature, **deve** seguir o conteudo abaixo.

## Nomenclaturas

Abaixo seguem os cuidados quanto aos nomes utilizados no desenvolvimento.

### Nome da feature

Quando estivermos criando uma nova feature, é necessário tomar cuidado no nome da mesma. Este nome deve ser o mesmo utilizado no arquivo [*feature.json*](features.md#featurejson) e preferencialmente usado ao nomear arquivos utilizados no projeto. Nomes simples devem ser escritos somente em **minusculo** e nomes compostos deve seguir o padrão **lowerCamelCase**. Por exemplo:

* Nome no portal: **featureTeste**
* Nome no *feature.json*: **featureTeste**

### Nomenclaturas para AngularJS

Afim de evitar colisão de nomes de módulos, controllers, services, etc, é necessário seguir as recomendações do [Angular Style Guide](https://github.com/johnpapa/angular-styleguide) (por [@john_papa](https://twitter.com/john_papa)) juntamente com as recomendações abaixo:

|Método do Angular|Nomenclatura|Exemplo|
|---|---|---|
|Module|featureName + 'Module'|`angular.module('avaliacaoModule', []);`|
|Controller|featureName + ViewName + 'Ctrl'|`angular.controller('avaliacaoListaDisciplinasCtrl', function() {});` |
|Service ou Factory|featureName + ServiceName|`angular.service('avaliacaoDisciplinas' function() {});` `angular.factory('avaliacaoDisciplinas' function() {});`|
|Provider|featureName + ProviderName|`angular.provider('avaliacaoConfig' function() {});`|
|Directive|featureName + DirectiveName|`angular.directive('avaliacaoListaDisciplina' function() {});`|

É valido lembrar que se o desenvolvedor for dividir em mais módulos, lembrar de iniciar com o nome da feature no inicio do módulo, por exemplo: `angular.module('avaliacaoCalendarModule' []);`

