# 📁 Criação de Subsites e Estrutura Padronizada com Permissionamento

##Visão Geral

Automação para criação de subsites no SharePoint utilizando Microsoft Power Automate, permitindo que o time comercial crie ambientes de projeto de forma rápida e padronizada, sem depender da equipe de TI.

---

## 📌 Objetivo
Automatizar a criação de subsites no SharePoint a partir de uma lista, incluindo estrutura de pastas padronizada e aplicação automática de permissões.

---

## 🎯 Problema
A criação de subsites era feita manualmente pela TI sempre que um novo projeto era iniciado.

Processo levava em média até 3 horas
Dependência total da equipe de TI
Alto volume de tickets operacionais
Risco de inconsistência na configuração

---

## ✅ Solução

Desenvolvi uma automação que permite ao próprio time comercial iniciar a criação de subsites.

Criação automatizada em 2 a 3 minutos
Redução significativa de chamados para TI
Padronização completa dos subsites
Ganho direto de produtividade

---


## 📊 Impacto
⏱️ Tempo reduzido: ~95% mais rápido
📉 Menos carga operacional para TI
⚡ Maior autonomia para o time comercial

---

## ⚙️ Gatilho

**When an item is created (SharePoint)**

O fluxo é iniciado automaticamente quando um novo item é criado em uma lista do SharePoint.

---

## 🧩 Arquitetura da Solução

O fluxo é dividido em quatro etapas principais:

### 🔹 1. Criação do Subsite
- Utiliza requisição HTTP para a API do SharePoint  
- Cria o subsite dinamicamente com base nos dados da lista  
- Define nome, URL, descrição e template
A criação do subsite é realizada via SharePoint REST API, permitindo maior controle do que as ações padrão do Power Automate.

##### 🔎 Exemplo de requisição HTTP

```json
{
  "method": "POST",
  "uri": "/_api/web/webinfos/add",
  "body": {
    "parameters": {
      "__metadata": { "type": "SP.WebInfoCreationInformation" },
      "Title": "<Título + OS>",
      "Url": "<URL Site>",
      "Description": "<Descrição>",
      "WebTemplate": "BDR#0",
      "UseUniquePermissions": false
    }
  }
}
```

---

### 🔹 2. Estrutura de Pastas via Excel
- Consulta uma planilha Excel armazenada no SharePoint  
- A planilha define a hierarquia padrão de pastas  
- Permite manutenção da estrutura sem alterar o fluxo  

---

### 🔹 3. Criação automática de pastas
- Percorre cada linha da tabela (loop)  
- Cria as pastas na biblioteca de documentos  
- Garante padronização entre todos os sites criados  

---

### 🔹 4. Aplicação de Permissões
- Define acesso com base em grupos pré-configurados  
- Tipos de acesso:
  - **Edição:** usuários podem alterar conteúdo  
  - **Visualização:** acesso somente leitura  

---

## 🛠️ Tecnologias utilizadas
- Power Automate  
- SharePoint Online  
- SharePoint REST API (HTTP Request)  
- Excel Online (Business)  

---

## ✅ Resultado
- Criação automatizada de subsites sem necessidade de intervenção da T.I  
- Redução do tempo de provisionamento de horas para poucos minutos  
- Eliminação de erros de permissão  
- Padronização completa da estrutura de pastas  
- Maior eficiência operacional e governança  

---

## 🖼️ Fluxo

### 🔹 Criação do Subsite
![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/9ac2fec1ff77b45be25a5381ed360650e5c132c7/DiagramaCriacaodeSitesParte1.png?raw=true)


![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/d518b1407f243aee71c94d9cdf4390c7e178daec/DiagramaCriacaodeSitesParte2.png?raw=true)


![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/d518b1407f243aee71c94d9cdf4390c7e178daec/DiagramaCriacaodeSitesParte3.png?raw=true)

---

## ⚠️ Observações
- Fluxo anonimizado para fins de portfólio  
- Estrutura adaptável conforme necessidade do negócio  
