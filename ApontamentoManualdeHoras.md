# Apontamento Manual de Horas
## Objetivo

Automatizar o processo de **apontamento manual de horas em projetos**, permitindo que colaboradores enviem solicitações de lançamento via **Microsoft Forms**, com **aprovação do gestor** e **atualização automática de status no SharePoint**.

---

## Gatilho

O fluxo é iniciado **quando uma resposta é submetida no Microsoft Forms**.

---

## Ações Principais

- **Obter detalhes da resposta**
  - Coleta as informações enviadas no Forms, incluindo o colaborador, projeto e gestor responsável.

- **Inicializar variável de anexos**
  - Cria uma variável para armazenar temporariamente os arquivos anexados na resposta do Forms.

- **Criar item na lista do SharePoint**
  - Registra as informações enviadas na lista “Apontamento Manual Navis”, utilizada como painel de acompanhamento.

- **Enviar solicitação HTTP ao SharePoint**
  - Configura o item criado para permitir acesso personalizado: <br>
    - O colaborador que respondeu tem permissão de **visualização apenas nos próprios lançamentos**. <br>
    - O grupo de Planejamento tem **permissão de edição** em todos os itens. <br>

- **Tratar anexos com Parse JSON**
  - Faz a leitura dos anexos enviados via Forms, interpretando o conteúdo em JSON para posterior gravação.

- **Salvar anexos**
  - Para cada arquivo identificado: <br>
    - Obtém o conteúdo do arquivo. <br>
    - Adiciona o anexo ao item correspondente na lista SharePoint. <br>

- **Analisar gestor indicado**
  - Identifica o gestor informado na resposta para direcionar a solicitação de aprovação.

- **Etapa de aprovação**
  - Envia uma solicitação de aprovação para o gestor responsável. <br>
  - Caso aprovado, envia: <br>
    - Um e-mail de confirmação ao colaborador. <br>
    - Um e-mail de notificação à equipe de Planejamento para realizar o lançamento manual no sistema. <br>
  - Caso rejeitado, envia um e-mail ao colaborador informando o motivo. <br>

- **Atualização de status**
  - Atualiza o item na lista do SharePoint conforme o andamento (em análise, aprovado, rejeitado, concluído).

---

## Resultado Esperado

O fluxo automatiza o processo de **apontamento manual de horas**, garantindo: <br>
- Controle centralizado via lista no SharePoint. <br>
- Comunicação automática entre colaborador, gestor e equipe de Planejamento. <br>
- Transparência no acompanhamento de status, funcionando como um painel de controle atualizado em tempo real. <br>

## Visão

![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte1.png?raw=true)
![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte2.png?raw=true)
![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte3.png?raw=true)
![Diagrama4](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte4.png?raw=true)

## Observações

- Fluxo anonimizado para exemplo público. <br>
- A estrutura de permissões garante acesso restrito por colaborador. <br>
- Os anexos são manipulados via **Parse JSON** para compatibilidade com Forms. <br>
- Pode ser integrado com Power BI para análise dos dados. <br>

![Diagrama5](https://github.com/HenriDiego/PowerAutomate/blob/45889eb8f82dd18c648d02fd4b8baaa2a18c759e/Imagens/ApontamentoManualParte6.png?raw=true)

