# Boas práticas no AngularJS

----------------------------------------------------------------------

## "Regras e dicas gerais"
- Utilize funções auto invocadas, para evitar o contexto global.
  ```javascript
  (function () {
    "use strict";

    angular.module("app").factory("storage", storage);

    function storage() {}
  })();
  ```
- Não crie controllers que são reutilizados em milhares de views, ao invés disso, crie factories que encapsulem essas lógicas reaproveitáveis e mantenha o controller simples, focado para uma única view.
- Crie uma pasta `Layout` para conter componentes gerais da aplicação que são reutilizados em toda aplicação, como menus, navegações, tabelas, etc...

----------------------------------------------------------------------

## Módulos - coisas que devemos fazer
- São utilizados para declarar a view e o controller.
- Ao criar um módulo evite o uso de váriaveis, prefira um encadeamento, para evitar a colisão de váriaveis e tornar o código mais legível.
 ```javascript
  /* evite */
  var app = angular.module('app');
  app.controller('SomeController' , SomeController);

  function SomeController() { }
  ```

 ```javascript
  /* recomendado */
  angular
    .module('app')
    .controller('SomeController' , SomeController);

  function SomeController() { }
  ```
- Crie pequenos módulos independentes, facilitando o desenvolvimento com uma equipe maior, podendo desenvolver tudo de forma separada e juntar depois de uma só vez.
- Mantenha o módulo principal da aplicação leve, assim como todos os outros pequenos módulos.
- Caso existam funções e objetos do javascript, porém implementados pelo angularjs, prefira estes. Por exemplo: `$timeout`, ao invés de `setTimeout` e `$document` ao invés de `document`.
  - Estes serviços são mais fáceis de testar.

----------------------------------------------------------------------

## View / template - o que é?
- Basicamente a apresentação dos dados.
- Podemos renderizar dados do controller dentro da sua determinada view.

----------------------------------------------------------------------

## Controllers - coisas que NÃO devemos fazer
- Utilizar regra de negócio no controller.
- Utilizar funções anônimas ao declarar um controller.
- Utilizar sempre o $scope e preferir por escopos globais/compartilhados.
- Declarar as váriaveis em qualquer ordem / qualquer lugar, sem nenhuma lógica envolvida.
- Colocar lógicas complexas no controller.

## Controllers - coisas que devemos fazer
- Colocar apenas lógicas que envolvam a view no controller.
- Utilizar funções nomeadas ao declarar um controller.
- Criar uma váriavel `vm` no controller e a utilizar a sintaxe `controller as vm`.
- Colocar váriaveis que serão "bindadas" no ínicio do controller em ordem alfabética.
- Colocar as declarações de funções no ínicio do código, porém a função propriamente dita, apenas no final.
  - Isso é positivo por alguns pontos, como:
  - Remover a complexidade de funções do topo do controller, focando nas váriaveis bindadas.
  - Funções são içadas, isso é, "levadas ao topo" não importa onde forem declaradas em javascript.
  - Ex:
  - ```javascript
    var sum = sum;

    function getUsers(a, b) {
      return a + b;
    }
  ```
- Remover lógicas do controller, sempre coloca-lá em services com apenas uma responsabilidade cada.

----------------------------------------------------------------------

## Services - coisas que NÃO devemos fazer
- Utilizar todas as lógicas que envolvam a view dentro de um service.
- Não utilize nomes com prefixo `$`, pois são utilizados para factories do AngularJS.

## Services - coisas que devemos fazer
- Utilizar os services para chamadas a API e regras de negócio.
- Colocar lógicas dentro do service, sempre mantendo-os com uma única responsabilidade.
- No angular utilizamos "factories" como services, portanto devemos retornar sempre um objeto, podendo conter métodos, etc...
- Manter sempre com apenas uma responsabilidade.

----------------------------------------------------------------------

## Diretivas - coisas que devemos fazer
- Utilizadas para encapsular comportamentos e tornar mais fácil o reuso dos mesmos.
- Utilize prefixos que remetam a algum escopo, facilitando a identificação das diretivas pelo prefixo.
- Evite o prefixo `ng`, pois são preservados para o AngularJS.
- Restrinja diretivas para elementos e atributos ( EA ), porém perceba pontos específicos para limitar a apenas uma forma.
  - Por exemplo, normalmente quando ela tem um controlador próprio é utilizado "elemento" ( E ).
- Utilize a sintaxe `controller as` para as diretivas, para manter o padrão com o controller e view, já comentados acima.

----------------------------------------------------------------------

## Testes no AngularJS
- Utilize testes unitários e conte uma "breve história" dentro da sua descrição, por exemplo: should return 1 person when filtered by name. Isso irá facilitar o entendimento dos testes.

!!!! em em desenvolvimento....

----------------------------------------------------------------------

## Créditos
- Um ótimo repositório sobre styleguide no AngularJS, o qual tirei várias inspirações para desenvolver esse breve resumo foi o: https://github.com/johnpapa/angular-styleguide/blob/master/a1/i18n/pt-BR.md#iife