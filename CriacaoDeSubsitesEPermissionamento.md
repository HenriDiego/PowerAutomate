# Criação de sites e Permissionamento.

## Objetivo

Automatizar a criação de subsites no SharePoint a partir de uma lista, configurando automaticamente uma estrutura padrão de pastas de documentos (definida em uma planilha do Excel) e aplicando permissões específicas para grupos de usuários.

## Gatilho

O fluxo é iniciado quando um novo item é criado em uma lista específica do SharePoint.

## Ações Principais

-Enviar solicitação HTTP ao SharePoint <br>
Cria o subsite com base nas informações fornecidas na lista.

-Listar itens em uma tabela do Excel <br>
Consulta uma planilha que contém a estrutura de pastas padrão a ser criada em cada subsite.

-Criar nova pasta <br>
Cria automaticamente as pastas listadas no Excel dentro da biblioteca de documentos do subsite.

-Obter metadados usando um caminho <br>
Recupera as propriedades e informações do item recém-criado para uso nas etapas seguintes.

-Permitir acesso a um item <br>
Aplica as permissões de acesso para os grupos definidos: <br>
**Edição:** usuários com permissão para modificar documentos e pastas. <br>
**Visualização:** usuários com acesso apenas para leitura. <br>

## Estrutura de Pastas

A estrutura de pastas é mantida em uma planilha do Excel, onde cada linha representa uma pasta a ser criada.
Essa abordagem facilita a manutenção e permite ajustar a hierarquia sem precisar editar o fluxo no Power Automate.

## Resultado Esperado

Ao criar um novo item na lista, o fluxo:

Gera automaticamente um subsite com o nome especificado.

Cria toda a estrutura de pastas definida no Excel.

Aplica permissões personalizadas de acordo com os grupos configurados.

## Visão


![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/9ac2fec1ff77b45be25a5381ed360650e5c132c7/DiagramaCriacaodeSitesParte1.png?raw=true)


![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/d518b1407f243aee71c94d9cdf4390c7e178daec/DiagramaCriacaodeSitesParte2.png?raw=true)


![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/d518b1407f243aee71c94d9cdf4390c7e178daec/DiagramaCriacaodeSitesParte3.png?raw=true)







##Observações
- Fluxo anonimizado para exemplo público.

