# Comunicação em Massa via Teams

## Descrição
Fluxo responsável por realizar o envio de comunicados em massa no Microsoft Teams utilizando uma inbox de comunicados cadastrados em lista do SharePoint.  
Permite que a equipe de comunicação envie mensagens padronizadas para todos os usuários internos de forma centralizada, visual e controlada.

---

## Objetivo
Realizar disparo de comunicados institucionais no Microsoft Teams para todos os colaboradores da organização, facilitando ações internas e avisos gerais.

---

## Tecnologias Utilizadas

- **Power Automate** — Orquestração do fluxo
- **SharePoint** — Armazenamento das listas
- **Microsoft Teams** — Canal de envio das mensagens
- **GitHub** — Hospedagem pública de imagens
- **Adaptive Cards** — Estrutura visual das mensagens

---

## Estrutura no SharePoint

### Lista de Comunicados
Lista utilizada como inbox de mensagens que serão disparadas.

**Campos:**
- **Título**
- **Texto**
- **URL** (imagem ou link de ação)

---

### Lista de Contatos
Lista simplificada contendo apenas o destinatário da mensagem.

**Campos:**
- **Pessoa** (campo do tipo *Person*)

Essa abordagem reduz complexidade, melhora a experiência de uso e evita inconsistências de dados.

---

## Gatilho do Fluxo
**Quando um item é selecionado na lista de Comunicados (SharePoint).**

O envio é manual, garantindo controle total sobre o momento do disparo.

---

## Etapas do Fluxo

1. **Trigger**
   - Item selecionado na lista de comunicados.

2. **Obter Comunicado**
   - Leitura do título, texto e URL.

3. **Obter Lista de Contatos**
   - Consulta na lista contendo o campo *Pessoa*.

4. **Montagem do Adaptive Card**
   - Inserção de:
     - Título
     - Texto
     - Imagem ou botão usando a URL
     - Layout institucional

5. **Loop de Envio**
   - Para cada pessoa da lista:
     - Enviar mensagem no Microsoft Teams.

6. **Finalização (Opcional)**
   - Atualização de status ou registro de envio.

---

## Adaptive Card
Os Adaptive Cards permitem:

- Padronização visual
- Inserção de imagem
- Botões clicáveis
- Melhor experiência para o usuário final

---

## Observações

- As imagens podem ser hospedadas no GitHub para geração de link público.
- Estrutura de listas propositalmente simples para facilitar manutenção.
- Fluxo indicado para comunicados institucionais e avisos internos.
- Permissões da lista devem ser restritas à equipe de comunicação.

---

## Imagens do Fluxo

### Visão Geral
![Visão Geral do Fluxo](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/FluxoCompleto.png?raw=true)

### Montagem do Card
![Adaptive Card](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/AdaptativeCard.png?raw=true)

### Loop de Envio
![Loop de Envio](https://github.com/HenriDiego/PowerAutomate/blob/main/Imagens/MensagensEmMassa.gif?raw=true)
