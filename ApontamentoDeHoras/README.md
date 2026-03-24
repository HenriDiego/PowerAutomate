# 📁 Solicitação e Aprovação de Apontamento de Horas

## 📌 Objetivo
Automatizar o processo de solicitação, aprovação e controle de apontamento manual de horas em projetos, garantindo rastreabilidade, padronização e controle de acesso.

---

## 🎯 Problema
O processo de apontamento de horas não possuía padronização e envolvia múltiplas etapas entre diferentes áreas, resultando em:

- Solicitações feitas via e-mail ou Microsoft Teams  
- Falta de visibilidade sobre o status das solicitações  
- Dependência manual entre colaborador, gestor e planejamento  
- Risco de perda de solicitações no processo  
- Tempo elevado para conclusão  

Além disso, não havia controle centralizado nem rastreabilidade do andamento.

---

## ⚙️ Gatilho

**When a new response is submitted (Microsoft Forms)**

O fluxo é iniciado quando um colaborador envia uma solicitação de apontamento de horas.

---

## 🧩 Arquitetura da Solução

O fluxo foi estruturado para automatizar todo o ciclo de solicitação:

---

### 🔹 1. Registro da Solicitação
- Coleta os dados enviados no Microsoft Forms  
- Cria automaticamente um item em uma lista do SharePoint  
- A lista funciona como painel central de controle  

---

### 🔹 2. Controle de Acesso (HTTP + SharePoint)
- Utiliza requisição HTTP para configurar permissões no item  
- Garante que:
  - O colaborador visualize apenas suas solicitações  
  - O planejamento tenha acesso completo para edição  

#### 🔎 Exemplo de requisição HTTP (permissão)

```json
{
  "method": "POST",
  "uri": "/_api/web/lists/getbytitle('<lista>')/items(<id>)/breakroleinheritance(copyRoleAssignments=false, clearSubscopes=true)"
}
```

### 🔹 3. Tratamento de Anexos
Os anexos enviados no Forms são tratados via Parse JSON
Para cada arquivo:
O conteúdo é extraído
O anexo é vinculado ao item no SharePoint

---

### 🔹 4. Processo de Aprovação
O fluxo envia automaticamente uma solicitação ao gestor responsável
Utiliza o conector Approvals

Decisões possíveis:

✅ Aprovado → segue para planejamento
❌ Rejeitado → colaborador é notificado

---

### 🔹 5. Encaminhamento para Planejamento
Apenas solicitações aprovadas seguem no fluxo
O planejamento é acionado automaticamente para execução

---

### 🔹 6. Atualização de Status e Rastreabilidade
O status da solicitação é atualizado ao longo do fluxo:
Em análise
Aguardando aprovação
Aprovado
Rejeitado
Concluído
O colaborador pode acompanhar o andamento em tempo real
### 🔹 7. Notificações Automáticas

---

Envio de e-mails automáticos para:
Colaborador (confirmação / rejeição)
Planejamento (quando aprovado)
🛠️ Tecnologias utilizadas
Power Automate
Microsoft Forms
SharePoint Online
SharePoint REST API (HTTP Request)
Approvals (Power Automate)
✅ Resultado
Padronização completa do processo de apontamento de horas
Eliminação de solicitações perdidas
Redução da dependência manual entre setores
Maior transparência para o colaborador
Controle centralizado via SharePoint
Redução significativa do tempo de processamento
## 🖼️ Fluxo

![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte1.png?raw=true)
![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte2.png?raw=true)
![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte3.png?raw=true)
![Diagrama4](https://github.com/HenriDiego/PowerAutomate/blob/761b6d7b223f5885132a5fd8405061f7dd5a3871/Imagens/ApontamentoManualParte4.png?raw=true)

## ⚠️ Observações
Fluxo anonimizado para fins de portfólio
Controle de acesso implementado via HTTP para maior flexibilidade
Tratamento de anexos via Parse JSON para compatibilidade com Forms
Pode ser integrado com Power BI para análise dos dados
