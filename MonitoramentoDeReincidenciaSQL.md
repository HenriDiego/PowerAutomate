# Monitoramento de Reincidência de Incidentes 

## Descrição
Fluxo responsável por identificar automaticamente incidentes recorrentes registrados no Sistema e abrir tickets de análise preventiva quando um mesmo alerta ultrapassa um limite de ocorrências dentro de um período de 7 dias.

A automação consulta diretamente o banco SQL do sistema, identifica padrões de reincidência e registra automaticamente chamados de investigação para a equipe técnica.

---

## Objetivo
Detectar reincidência de incidentes operacionais de forma automática, permitindo que a equipe técnica identifique problemas estruturais antes que se tornem incidentes críticos ou recorrentes em larga escala.

---

## Tecnologias Utilizadas

- **Power Automate** — Orquestração do fluxo
- **SQL Server** — Fonte de dados dos tickets
- **Movidesk API** — Criação automática de tickets
- **GitHub** — Hospedagem da documentação

---

## Fonte de Dados

**Banco de Dados:** SQL Server  
**Tabela:** `dbo.Sistema`

Campos utilizados:

| Campo | Descrição |
|---|---|
| id | Identificador do ticket |
| subject | Título do chamado |
| category | Tipo do ticket |
| ownerTeam | Equipe responsável |
| createdDate | Data de criação |

---

## Estrutura de Controle de Recorrência

Para evitar abertura repetida de tickets para o mesmo alerta, foi criada uma tabela auxiliar responsável por armazenar o estado da última execução da automação.

### Tabela de Controle

```sql
CREATE TABLE controle_recorrencia_alertas (
    subject NVARCHAR(500),
    ultima_qtd INT,
    ultima_verificacao DATETIME
)
```
Essa tabela permite identificar se a quantidade de ocorrências aumentou desde a última execução do fluxo.

## Regra de Identificação de Reincidência

A automação identifica incidentes recorrentes considerando:

Categoria do ticket = _Incidente

Equipe responsável = SGN360

Período analisado = últimos 7 dias

Mínimo de 5 ocorrências do mesmo subject

Query utilizada

```sql

SELECT 
    subject,
    COUNT(id) AS total
FROM dbo.Sistema
WHERE 
    category = 'XXXX'
    AND ownerTeam = 'XXXXX'
    AND createdDate >= DATEADD(DAY, -7, GETDATE())
GROUP BY subject
HAVING COUNT(id) >= 5
ORDER BY total DESC

```

## Gatilho do Fluxo

Execução agendada (Recurrence).

O fluxo executa periodicamente a consulta SQL para verificar novos padrões de reincidência.

##Etapas do Fluxo
1. Trigger

Execução automática baseada em agendamento.

2. Consulta SQL

Execução da query responsável por identificar incidentes recorrentes.

3. Loop de Processamento

Para cada subject retornado pela consulta:

Verificação na tabela controle_recorrencia_alertas

Recuperação da última quantidade registrada

4. Comparação de Recorrência

A lógica de decisão segue:

Situação	Ação
Alerta novo	Criar ticket
Recorrência aumentou	Criar ticket
Recorrência manteve	Ignorar
Recorrência diminuiu	Ignorar
5. Criação de Ticket via API

Quando a reincidência aumenta, o fluxo cria automaticamente um ticket no Movidesk através de integração HTTP.

Estrutura do POST da API
```JSON
{
  "type": "2",
  "subject": "[REINCIDENCIA] - @{items('Apply_to_each')?['subject']}",
  "description": "Foi identificada reincidência do alerta \"@{items('Apply_to_each')?['subject']}\".\n\nNos últimos 7 dias foram registradas @{items('Apply_to_each')?['total']} ocorrências.\n\nRecomenda-se análise técnica para mitigação e prevenção de novos eventos.",
  "serviceFirstLevel": "XXXXXXX ",
  "clients": [
    {
      "id": "INSIRA O ID AQUI"
    }
  ],
  "createdBy": {
    "id": "INSIRA O ID AQUI"
  }
}
```

## Benefícios da Automação

Detecção automática de incidentes recorrentes

Redução da análise manual da equipe técnica

Identificação precoce de problemas estruturais

Monitoramento contínuo da base de incidentes

Prevenção de falhas recorrentes em ambiente produtivo


---

## Monitoramento Gerencial (Power BI)

Além da automação de criação de tickets, foi desenvolvido um **dashboard em Power BI** para permitir que gestores acompanhem a recorrência de incidentes de forma visual e analítica.

O dashboard utiliza a mesma base de dados do Movidesk, permitindo análise contínua da saúde operacional dos ambientes monitorados.

---

## Objetivo do Dashboard

Fornecer visibilidade gerencial sobre padrões de incidentes e recorrências, permitindo que gestores e equipes técnicas identifiquem rapidamente problemas estruturais.

O dashboard permite acompanhar:

- Incidentes mais recorrentes
- Tendência de crescimento ou redução de alertas
- Volume de incidentes ao longo do tempo
- Alertas críticos que exigem atenção imediata

---

## Indicadores Monitorados

O dashboard apresenta os seguintes indicadores principais:

| Indicador | Descrição |
|---|---|
| Incidentes últimos 7 dias | Total de incidentes recentes |
| Incidentes recorrentes | Alertas que ultrapassaram o limite definido |
| Alertas críticos | Incidentes com crescimento significativo |
| Tendência semanal | Evolução de incidentes ao longo do tempo |

---

## Ranking de Incidentes

Foi implementado um ranking de incidentes recorrentes, permitindo identificar rapidamente quais alertas estão ocorrendo com maior frequência.

Esse ranking permite:

- Identificar problemas estruturais
- Priorizar análises técnicas
- Detectar novos padrões de falhas

---

## Análise de Tendência

O dashboard também apresenta gráficos de tendência para acompanhar a evolução dos incidentes ao longo do tempo.

Isso permite verificar:

- Crescimento de incidentes
- Redução após correções
- Comportamento histórico dos alertas

---

## Integração com a Automação

A automação e o dashboard se complementam:

| Automação | Dashboard |
|---|---|
Detecta reincidências automaticamente | Permite análise gerencial |
Abre tickets automaticamente | Permite monitoramento visual |
Reduz análise manual | Apoia tomada de decisão |

---

## Imagens do Dashboard

### Visão Geral

![Dashboard](./Imagens/dashboard_recorrencia.png)

### Ranking de Incidentes

![Ranking](./Imagens/ranking_incidentes.png)

### Tendência de Incidentes

![Tendência](./Imagens/tendencia_incidentes.png)
