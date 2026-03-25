# 📁 CRM com Automação de Leads e Campanhas (Power Platform)

## 📌 Objetivo
Desenvolver um sistema de gestão de contatos e automação de campanhas de e-mail, permitindo controle completo do ciclo de relacionamento com leads, desde o cadastro até o envio automatizado de comunicações.

---

## 🎯 Problema
O processo de gestão de leads e campanhas:

- Era manual e descentralizado  
- Não possuía controle estruturado de contatos  
- Dependia de envios manuais de e-mail  
- Não havia acompanhamento do status dos leads  
- Não existia automação de relacionamento ao longo do tempo  

---

## 🧩 Arquitetura da Solução

| Camada          | Responsabilidade |
|-----------------|-----------------|
| Power Apps      | Interface (CRM) |
| SharePoint      | Dados e configuração |
| Power Automate  | Execução e automação |

---

## 🧱 Módulos do Sistema

---

### 🔹 1. Gestão de Contatos (CRM)

Funcionalidades:

- Cadastro de contatos  
  - Nome  
  - Email  
  - Telefone  
  - Empresa  
- Edição e manutenção dos dados  
- Base centralizada para campanhas  

👉 Funciona como o núcleo do CRM

---

### 🔹 2. Campanhas Pontuais (Envio Manual)

Permite envio de e-mails sob demanda:

- Seleção de múltiplos contatos  
- Definição de:
  - Assunto  
  - Corpo do e-mail  
- Uso de template HTML padronizado  
- Preview do e-mail antes do envio  
- Disparo em massa via Power Automate  

👉 Ideal para comunicações específicas e não recorrentes

---

### 🔹 3. Automação de Leads (Régua de Relacionamento)

Sistema de envio automático de e-mails ao longo de 60 dias, dividido em múltiplas etapas.

---

## ⚙️ Motor de Automação (Power Automate)

### 🔁 Execução Recorrente

- Gatilho: **Recurrence (ex: a cada 1 dia)**  
- Atua como um scheduler baseado em dados  

---

### 🔍 Seleção de Leads Elegíveis

Filtro:

- StatusFluxo = Ativo  
- FluxoAprovado = true  
- DataProximoEnvio <= utcNow()  

---

### 🔄 Processamento

Para cada lead:

1. Calcula próxima etapa  
2. Consulta tabela **SequenciaEmails**  
3. Envia e-mail personalizado (HTML)  
4. Atualiza:
   - EtapaAtual  
   - DataProximoEnvio  

---

### 🛑 Finalização

Sem próxima etapa → Status = Finalizado  

---

## 🧠 Lógica do Sistema

👉 Scheduler baseado em dados

Sem uso de:
- Delay  
- Execuções longas  
- Dependência contínua  

---

## ⚙️ Princípios Técnicos

### 🔹 Idempotência
Evita envios duplicados com base na data

---

### 🔹 Configuração externa
A lógica da régua é controlada via SharePoint

---

### 🔹 Separação de camadas
- UI → Power Apps  
- Dados → SharePoint  
- Execução → Power Automate  

---

### 🔹 Escalabilidade
- Suporta múltiplos leads  
- Execução desacoplada  

---

## 📊 Exemplo de Execução

| Etapa | Dias | Data |
|------|------|------|
| 1    | 0    | 01/03 |
| 2    | 2    | 03/03 |
| 3    | 3    | 06/03 |
| 4    | 10   | 16/03 |

---

## 🛠️ Tecnologias utilizadas

- Power Apps  
- Power Automate  
- SharePoint Online  
- Outlook  

---

## ✅ Resultado

- Centralização dos contatos  
- Automação completa de campanhas  
- Redução de esforço manual  
- Padronização da comunicação  
- Controle total do ciclo do lead  
- Maior eficiência operacional  

---

## ⚠️ Observações

- Estrutura preparada para migração futura para Dataverse  
- Arquitetura adaptável para outros fluxos de comunicação  
