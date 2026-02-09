# Monitoramento de Capacidade Storage SharePoint

## Descrição
Fluxo responsável por monitorar automaticamente o consumo de armazenamento do SharePoint Online e gerar alertas quando o limite definido for atingido.  
O fluxo pode registrar um ticket automaticamente via API (Movidesk) ou enviar notificações simples por e-mail ou Teams.

---

## Objetivo
Identificar quando o ambiente SharePoint Online estiver próximo do limite de armazenamento contratado, evitando indisponibilidades, falhas de upload e impactos operacionais.

---

## Tecnologias Utilizadas

- **Power Automate** — Orquestração do fluxo
- **SharePoint API** — Consulta de consumo de armazenamento
- **Movidesk API** — Registro automático de ticket (opcional)
- **Microsoft 365 / SharePoint Online** — Ambiente monitorado

---

## Gatilho do Fluxo
**Recorrência (Recurrence)** — Execução automática em intervalos definidos.

Exemplo: 1x por dia ou 1x por semana.

---

## Variáveis Inicializadas

Logo no início do fluxo são criadas variáveis de controle:

- **LimitePercentual** — Percentual que define o alerta (ex: 80%)
- **Empresa** — Nome da empresa monitorada
- **IdDoCliente** — ID do cliente no sistema de tickets

Essa abordagem permite reutilizar o fluxo para diferentes clientes.

---

## Etapas do Fluxo

### 1. Inicialização de Variáveis
Define parâmetros de controle do monitoramento.

---

### 2. Solicitação HTTP ao SharePoint
É realizada uma requisição HTTP para obter:

- Armazenamento utilizado
- Armazenamento total disponível

---

### 3. Parse do Retorno
O retorno JSON é tratado para facilitar leitura e uso posterior.

Exemplo de retorno:

```json
{
  "d": {
    "results": [
      {
        "GeoUsedStorageMB": "16419",
        "TenantStorageMB": "1089536"
      }
    ]
  }
}
```
### 4. Cálculo do Percentual Utilizado (Compose)
Expressão utilizada:

div(
  mul(
    int(body('Parse_Storage')?['d']?['results']?[0]?['GeoUsedStorageMB']),
    100
  ),
  int(body('Parse_Storage')?['d']?['results']?[0]?['TenantStorageMB'])
)

Esse cálculo retorna o percentual atual de consumo de armazenamento.

### 5. Condição de Limite

Regra simples:

Se percentual ≥ limite definido → Gera alerta

Se percentual < limite → Não executa ação

### 6. Registro de Ticket (Opcional)

Caso o limite seja atingido, o fluxo registra automaticamente um ticket no Movidesk utilizando API.

Exemplo de payload:

```json
{
  "type": "2",
  "subject": "{ALERTA @{variables('Empresa')}} Capacidade Storage SharePoint Online acima de @{variables('LimitePercentual')}%",
  "description": "Foi identificado que o ambiente SharePoint Online atingiu @{outputs('Compor')}% de utilização.",
  "serviceFirstLevel": "Exemplo",
  "clients": [
    {
      "id": "@{variables('IdDoCliente')}"
    }
  ]
}

```

### 7. Benefícios do Fluxo

Monitoramento proativo

Redução de intervenção manual

Prevenção de indisponibilidade

Escalável para múltiplos clientes

Integração com sistemas externos

Governança de ambiente


## Imagens do Fluxo

### Visão Geral
![Visão Geral do Fluxo](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/VisaoCompleta.png?raw=true)

### Parse e Compose
![Inicialização]([./imagens/storage-variaveis.png](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/ParseCompose.png?raw=true))

### Solicitação HTTP Sharepoint
![HTTP SharePoint]([./imagens/storage-http.png](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/GetHTTPSharepoint.png?raw=true))


### 8. Observações

O limite percentual é configurável.

Requer permissões adequadas de API no SharePoint.

Pode ser facilmente adaptado para Teams ou e-mail.

Ideal para ambientes gerenciados de Microsoft 365.
