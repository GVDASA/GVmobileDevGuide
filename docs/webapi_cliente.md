# WebAPI do cliente

Para acessar as informações do sistema do *GVcollege* do cliente, disponibilizamos uma WebAPI que se comunica com o Banco de Dados e retorna consultas contidas em *views* personalizadas no *SQL Server (2012)*.

## Criando uma view para consulta

Para criar uma view no banco de dados do *GVcollege*, deve se tomar cuidado onde e como será criada. Todas as views **devem** ser criadas no schema **[dbo]**, e alem disto , **devem** ter o prefixo **GVMVW_**. Por exemplo: **[dbo].[GVMVW_PESSOA]**.

Abaixo um exemplo da criação de uma view:

```sql
CREATE VIEW dbo.GVMVW_Pessoa
AS
SELECT
	CODIGOPESSOA AS CodigoPessoa,
	NOME AS Nome,
	NOMEREDUZIDO AS NomeReduzido,
	DATAATUALIZACAO AS DataAtualizacao
FROM dbo.PAD_PESSOA
```

## Consultando uma view

Para acessar uma view e obter seus dados, podemos seguir o exemplo abaixo:

`~/api/views/<nome_da_view>?<odata>`

Onde:

* `<nome_da_view>`: Nome da view criada no banco de dados sem o prefixo 'dbo.GVMVW_' ; Ex.: Para a view [dbo].[GVMVW_PESSOA] utilize pessoa. Obs.: A capitalização não importa.
* `<odata>`: Parâmetros no formato OData. Apenas um conjunto limitado do protocolo está implementado atualmente, portanto use apenas os listados abaixo:
	* `$orderby`: **[obrigatório]** Define a ordenação do resultado da consulta através dos nomes das colunas separados por vírgula.
	* `$select`: Indica quais campos serão retornados na consulta.
	* `$skip`: Indica quantos registros devem ser ignorados, isso influencia a paginação, pois a quantidade de registros de ignorados é a multiplicação de quantidade de páginas anteriores pela quantidade de registros em cada página.
	* `$top`: Indica a quantidade de registros por página.
	* `$filter`: Devem ser passadas as expressões de filtro, geralmente com o nome dos campos e operadores.

**Nota:** Todas as consultas estão **limitadas em 1000 registros**. Utilize a páginação através dos operadores `$skip` e `$top` caso precise obter os demais registros.

### Exemplos de consultas

Consulta sem filtro ou operação alguma.

`~/api/views/pessoa?$orderby=nome`

Consulta com filtro sobre o campo CodigoPessoa, onde CodigoPessoa deve igual a 42.

`~/api/views/pessoa?$orderby=CodigoPessoa&$filter=CodigoPessoa eq 42`

Consulta com filtro sobre o campo CodigoPessoa, onde CodigoPessoa deve ser maior que 1 e CodigoPessoa deve ser menor que 50.

`~/api/views/pessoa?$filter=CodigoPessoa gt 1 and CodigoPessoa lt 50&$orderby=CodigoPessoa&$skip=10&$top=10`

Consulta que retorna também a quantidade total de registros na consulta.

`~/api/views/pessoa?$orderby=CodigoPessoa&$inlinecount=allpages&$skip=10&$top=10`

Consulta que retorna apenas o campo CodigoPessoa devido a operação de select.

`~/api/views/pessoa?$select=CodigoPessoa&$orderby=CodigoPessoa&$skip=10&$top=10`
