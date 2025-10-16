# Envio de E-mails Comerciais para Leads
## Objetivo

Automatizar o processo de nutrição e acompanhamento de leads comerciais, enviando sequências de e-mails em intervalos definidos e solicitando aprovação da equipe de vendas antes de cada novo contato.
O objetivo é manter o relacionamento ativo com o lead, garantindo acompanhamento controlado e aumento da taxa de conversão.

## Gatilho

O fluxo é iniciado quando uma nova resposta é submetida no Microsoft Forms, que automaticamente cria um item na lista “Leads Comerciais” no SharePoint.

## Ações Principais

Obter detalhes do lead
O fluxo coleta os dados preenchidos no Forms (nome, e-mail, empresa, responsável comercial, etc.) e os grava na lista “Leads Comerciais” do SharePoint.

Enviar primeiro e-mail automático
Assim que o lead é registrado, o fluxo dispara o primeiro e-mail comercial com mensagem de boas-vindas e incentivo ao contato. <br>

Esperar 5 dias
O fluxo aguarda 5 dias após o primeiro contato antes de seguir para a próxima etapa. <br>

Solicitar aprovação ao responsável comercial
Antes de cada novo disparo, o fluxo envia uma solicitação de aprovação ao colaborador responsável pelo lead: <br>

Se aprovado, o fluxo envia o próximo e-mail.
Se rejeitado, o processo é encerrado e o status do lead é atualizado para “Contato encerrado”. <br>

Enviar segundo e-mail
Caso aprovado, envia o segundo e-mail com nova abordagem comercial, reforçando o relacionamento. <br>

Esperar 10 dias
O fluxo aguarda mais 10 dias antes do próximo contato.

Repetição de aprovação e envio
O mesmo processo se repete antes de cada e-mail subsequente, garantindo controle humano em todas as etapas. <br>

Atualização de status no SharePoint
Após cada etapa, o campo “Status do Lead” é atualizado automaticamente (ex: “E-mail 1 enviado”, “Aguardando aprovação”, “E-mail 2 enviado”, etc.). <br>

A lista do SharePoint serve também como painel de acompanhamento para a equipe comercial, permitindo visualizar o progresso de cada lead.

Transição para o segundo fluxo

Como o Power Automate possui limite máximo de 30 dias por execução, ao final do primeiro ciclo o fluxo atualiza um campo específico na lista.

Essa alteração dispara automaticamente o segundo fluxo, responsável por continuar o acompanhamento por mais 30 dias.

##Resultado Esperado

O fluxo automatiza todo o follow-up de leads, garantindo: <br>

Contato consistente e programado com cada lead. <br>

Supervisão da equipe de vendas em cada etapa do processo. <br>

Acompanhamento centralizado via lista SharePoint. <br>

Continuidade do acompanhamento mesmo após o limite de execução de 30 dias. <br>

## Visão

![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/26ab610f367503d0e2f82eb5586835fd9d8dceaa/Imagens/EmailComercialParte1.png?raw=true)
![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/26ab610f367503d0e2f82eb5586835fd9d8dceaa/Imagens/EmailComercialParte2.png?raw=true)
![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/26ab610f367503d0e2f82eb5586835fd9d8dceaa/Imagens/EmailComercialParte3.png?raw=true)

## Fluxo2

![Diagrama4](https://github.com/HenriDiego/PowerAutomate/blob/26ab610f367503d0e2f82eb5586835fd9d8dceaa/Imagens/EmailComercialParte4.png?raw=true)


## Observações

A integração entre Microsoft Forms e SharePoint garante entrada automatizada de novos leads. <br>

A lista de acompanhamento no SharePoint permite que a equipe visualize o status, aprovações e histórico de e-mails.<br>

O processo é dividido em duas fases (60 dias) para contornar o limite de 30 dias do Power Automate.<br>

Todo envio de e-mail depende de aprovação do responsável comercial, garantindo personalização e segurança nas comunicações.<br>
