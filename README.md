# Animalec | Tarefa 3.1 b)

## Sobre o projeto

Este trabalho foi realizado para a unidade curricular de Programação Web Avançada.

O objetivo foi acrescentar duas áreas ao Back-office do Animalec: Sponsors, para gerir patrocinadores de animais, e Experts, para gerir especialistas científicos.

Utilizei como ponto de partida o projeto Animalec disponibilizado por um colega no fórum da unidade curricular. Mantive a estrutura da aplicação e acrescentei as novas opções à área de administração.

## O que foi desenvolvido

Na área Sponsors é possível registar o nome do patrocinador, o tipo, o animal associado e o email.

Na área Experts é possível registar o nome do especialista, a especialidade, o grupo animal e o email.

Em ambas as áreas é possível adicionar, consultar, editar e remover registos. Os formulários têm campos obrigatórios e validação do formato dos endereços de email.

Também adaptei as listagens a diferentes tamanhos de ecrã. Em desktop, os registos aparecem numa tabela. Em mobile, aparecem em cartões com as ações disponíveis.

Para evitar repetir código, os dois módulos utilizam um componente Vue comum para os formulários e as listagens.

## Tecnologias

O projeto utiliza Vue.js 2, Vue Router, BootstrapVue, HTML5, CSS e JavaScript.

Os registos dos novos módulos são guardados no localStorage do navegador.

## Como executar

É necessário ter o Node.js e o npm instalados.

Na pasta do projeto, instalar as dependências:

    npm.cmd ci --legacy-peer-deps

No PowerShell, iniciar a aplicação com:

    $env:NODE_OPTIONS="--openssl-legacy-provider"
    npm.cmd run serve

Depois, abrir no navegador:

- http://localhost:8080/admin
- http://localhost:8080/admin/sponsors
- http://localhost:8080/admin/experts

## Wireframes e mockups

A pasta `docs` contém os wireframes e mockups das duas entidades, nas versões desktop e mobile.

Os desenhos estão disponíveis em HTML e PNG. Para consultar a galeria, basta abrir `docs/index.html` no navegador.

## Limitações

Esta extensão foi desenvolvida como protótipo académico.

Os novos registos são guardados apenas no navegador. Não são partilhados entre dispositivos nem estão integrados na API original do Animalec.

A lista de animais do formulário Sponsors utiliza exemplos dos dados de referência. Não é carregada automaticamente a partir de uma API.

Os restantes módulos e o sistema de autenticação pertencem ao projeto de referência. O funcionamento completo da autenticação não foi validado neste trabalho.

## Projeto de referência

O código de partida foi disponibilizado por José Ramos Silva no fórum da unidade curricular:

https://github.com/josthelvish/Animalec

Sobre essa base foram desenvolvidos os módulos Sponsors e Experts e a respetiva documentação visual.
