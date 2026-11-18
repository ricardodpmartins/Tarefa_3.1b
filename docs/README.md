# Tarefa 3.1 b) · Documentação de prototipagem Animalec

Esta pasta contém os oito ecrãs solicitados para as novas entidades **Sponsors** e **Experts**.

## Organização

- `wireframes/`: dois ecrãs por entidade (desktop e mobile), com estrutura simplificada e sem identidade visual final.
- `mockups/`: dois ecrãs por entidade (desktop e mobile), utilizando uma aproximação às cores, tipografia, cabeçalhos e tabelas da implementação Animalec.
- `assets/prototype.css`: estilos partilhados dos documentos HTML de prototipagem.
- `index.html`: galeria de consulta dos oito ecrãs.

Cada ecrã tem uma versão HTML, que pode ser editada, e uma imagem PNG para visualização e entrega. Os mockups são representações estáticas da interface e **não** substituem a aplicação funcional em Vue.

## Critérios de desenho

A estrutura acompanha os novos módulos implementados no projeto: identificação da entidade, navegação para administração, ação de adicionar, tabela com campos próprios e ações de consultar, editar e remover. No desktop são apresentadas tabelas e no mobile os registos são apresentados em cartões. Cada ecrã inclui também uma representação do formulário com os campos atuais, incluindo as listas de animais e grupos. A seleção de patrocinadores apresenta os quatro animais de exemplo do Animalec (Cão, Gato, Pardal e Cavalo); não consulta a API original. Os HTML da documentação são estáticos; a interação e a persistência estão no projeto Vue.

## Consulta

Abrir `docs/index.html` num browser. Os HTML também podem ser abertos individualmente sem servidor. As imagens PNG são capturas dos respetivos documentos HTML, com larguras de referência de 1440 px (desktop) e 390 px (mobile).

## Limites

Os conteúdos apresentados são exemplos fictícios. A persistência real do projeto é local no browser (`localStorage`), sem integração com API nem base de dados. Esta documentação não pressupõe autenticação funcional nem gestão de dados reais.
