# Monitoramento de Atividades <br>
## Objetivo

Garantir que os colaboradores do turno de operação estejam ativos e atentos durante o período de monitoramento das barragens, enviando perguntas aleatórias em intervalos irregulares e registrando o tempo de resposta. <br>

O fluxo permite identificar possíveis falhas de atenção ou períodos de inatividade, especialmente no turno da noite.  <br>

## Gatilho

O fluxo é agendado e executado automaticamente a cada 30 minutos. <br>
Antes de enviar a pergunta, ele gera um número aleatório entre 1 e 30, aguardando esse tempo adicional — o que cria um intervalo real entre 30 e 60 minutos entre as execuções.

## Ações Principais

Gerar número aleatório (1–30) <br>
Define o tempo de espera variável entre as execuções do fluxo.

Registrar hora atual <br>
Armazena o horário em que o ciclo iniciou, para referência no cálculo de tempo de resposta.

Verificar horário de refeição (almoço/janta) <br>
Avalia se o horário atual coincide com o período de pausa configurado. <br>
Se estiver dentro do horário de refeição, o fluxo é interrompido para evitar envio de mensagens indevidas.

Consultar lista de Turnos <br>
Obtém os dados dos turnos ativos, incluindo colaboradores, horário de início e término.

Selecionar turno correspondente ao horário atual <br>
Identifica automaticamente qual operador está em serviço no momento da execução.

Consultar lista de Perguntas <br>
Obtém o conjunto de perguntas disponíveis, armazenadas em uma lista dedicada.

Selecionar pergunta aleatória (via Parse JSON) <br>
Utiliza uma ação de Parse JSON para manipular o retorno da lista de perguntas. <br>
O fluxo gera um número aleatório entre 1 e 10, que representa o ID da pergunta a ser usada. <br>
Essa técnica garante que a escolha da pergunta seja totalmente dinâmica, sem necessidade de expressões complexas ou ações manuais adicionais.

Consultar lista de Operadores <br>
Recupera informações de contato do colaborador do turno atual, como nome, e-mail.

Registrar tentativa na lista de Respostas <br>
Cria um novo item na lista “Respostas” com data, hora, operador e pergunta enviada.

Enviar mensagem via Teams **(Adaptive Card)** <br>
O fluxo utiliza o Flow bot do Microsoft Teams para enviar um Adaptive Card diretamente ao colaborador. <br>
Esse card contém a pergunta aleatória e botões de resposta, permitindo que o operador responda sem sair do chat. <br>
A estrutura do card foi montada em JSON, contendo o texto da pergunta e campos de entrada, tornando o processo de resposta rápido e rastreável.

Registrar resposta <br>
Quando o colaborador envia a resposta pelo Teams, o fluxo captura automaticamente o retorno e armazena na lista “Respostas”.

Calcular tempo de resposta (via Parse JSON) <br>
Usa novamente o Parse JSON para interpretar a resposta recebida e calcular a diferença entre o horário de envio e o horário de resposta. <br>
Essa abordagem permite trabalhar com dados precisos de data/hora em formato ISO, facilitando o cálculo e a análise de desempenho.

Verificar se respondeu no tempo esperado <br>
Aplica uma condição para identificar se a resposta foi enviada dentro do prazo definido.

Enviar alerta ao gestor (caso de atraso ou ausência) <br>
Se o colaborador não responder dentro do tempo limite, o fluxo envia um e-mail automático ao gestor informando o atraso.

## Estrutura de Listas Utilizadas

Turnos: guarda os horários de início/fim e o operador responsável. <br>

Perguntas: contém o conjunto de perguntas aleatórias a serem enviadas. <br>

Operadores: informações cadastrais e dados de contato. <br>

Respostas: registra todos os envios, respostas e tempos de reação. <br>

## Resultado Esperado

Ao final de cada execução, o fluxo: 

Seleciona o colaborador ativo no turno.<br>

Envia uma pergunta aleatória via Teams.<br>

Calcula e registra o tempo de resposta.<br>

## Visão

![Diagrama1](https://github.com/HenriDiego/PowerAutomate/blob/38a096af59fed63fbc9ee5387b02d1e2e8d59eee/Imagens/CMIParte1.png?raw=true)
![Diagrama2](https://github.com/HenriDiego/PowerAutomate/blob/38a096af59fed63fbc9ee5387b02d1e2e8d59eee/Imagens/CMIParte2.png?raw=true)
![Diagrama3](https://github.com/HenriDiego/PowerAutomate/blob/38a096af59fed63fbc9ee5387b02d1e2e8d59eee/Imagens/CMIParte3.png?raw=true)
![Diagrama4](https://github.com/HenriDiego/PowerAutomate/blob/38a096af59fed63fbc9ee5387b02d1e2e8d59eee/Imagens/CMIParte4.png?raw=true)

##Observações

Fluxo anonimizado para exemplo público. <br>

Intervalo de execução ajustável conforme necessidade operacional.<br>

Pode ser integrado com Power BI para análise dos tempos de resposta.<br>
