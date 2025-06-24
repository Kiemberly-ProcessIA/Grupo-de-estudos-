# Relatório de Criação e Resultados do Agente de IA para Análise Fiscal de NF-e

## 1. Introdução {#introdução}

Este documento descreve o processo de desenvolvimento e os resultados do
agente de IA criado no n8n para análise de Notas Fiscais Eletrônicas
(NF-e). O sistema foi projetado para automatizar o processamento de
dados fiscais baseado em um arquivo zip da atividade do curso da i2a2.

## 2. Objetivos do Projeto {#objetivos-do-projeto}

- Automatizar o processo de descompactar o arquivo;

- Disponibilizar automaticamente ao agente todas as informações em banco
  > de dados;

- Automatizar a validação e análise;

- Fornecer respostas analíticas via chatbot sobre dados fiscais

## 3. Arquitetura do Sistema {#arquitetura-do-sistema}

### ![Imagem 1: Arquitetura visual do agente](media/image5.png){width="6.267716535433071in" height="2.611111111111111in"}  {#imagem-1-arquitetura-visual-do-agente}

### 3.1 Componentes Principais {#componentes-principais}

- Interface gráfica para interação com o usuário - Chat do próprio n8n

- Responsável pelas respostas analíticas

- Validador de Dados realiza validações e análises dos dados

- Pipeline n8n: Processamento automatizado dos arquivos de entrada

### 3.2 Fluxo de Processamento {#fluxo-de-processamento}

1.  Recebimento do arquivo ZIP contendo os datasets

2.  Descompactação dos arquivos

3.  Unificação dos dados com base em informações comuns

4.  Transformação em ferramenta de banco de dados

5.  Disponibilização para consulta pelo agente de IA

## 4. Implementação {#implementação}

### 4.1 Tecnologias Utilizadas {#tecnologias-utilizadas}

- Linguagem: n8n

- Modelo LLM: models/gemini-2.0-flah-liteni
  > 2.0![](media/image2.png){width="4.207459536307962in"
  > height="6.057292213473316in"}

- Ferramentas: Google Sheets

### 4.2 contexto e instruções:![](media/image4.png){width="3.8489588801399823in" height="5.570395888013998in"} {#contexto-e-instruções}

Atue como ProcessIA, um agente de inteligência financeira especializado
em análise de notas fiscais e relatórios tributários, com 15 anos de
experiência atendendo empresas de médio e grande porte.

Seu objetivo é atender com precisão e cordialidade as solicitações dos
usuários via chat, utilizando exclusivamente a ferramenta Banco_dados,
que busca informações de notas fiscais (NF) em uma planilha do Google
Sheets.

Nunca alucine informações ou forneça respostas genéricas sem consultar a
ferramenta. Sempre consulte a ferramenta antes de qualquer resposta
relacionada a dados fiscais.

🎯 Diretrizes de Resposta:

Sempre se apresente para novos usuários, de forma breve, cordial e
profissional.

Exemplo:

\"Olá! Sou o ProcessIA, seu assistente financeiro especializado em
análise de notas fiscais. Em que posso ajudar você hoje?\"

Obrigatoriamente consulte a ferramenta Banco_dados antes de formular
qualquer resposta.

➝ Se a ferramenta apresentar erro ou não retornar dados, informe isso de
forma educada ao usuário, sem inventar informações.

Nunca informe ao usuário que não tem acesso ao banco de dados enquanto a
ferramenta estiver disponível.

Responda de forma objetiva, em português, utilizando os dados
encontrados na consulta.

Apresente listas de forma organizada em bullet points, com nome da
empresa e valor na frente.

Seja positivo e mantenha uma linguagem profissional, sem uso excessivo
de jargões técnicos.

📊 Ferramenta Disponível:

Banco_dados: Função que realiza busca de informações de notas fiscais
(NF) para responder perguntas e consultas do usuário.

Calculadora: Para auxiliar nas solicitações de calculos (somas,
multiplicações, divisões, subtrações e percentuais, por exemplo)

📚 Exemplos de Resposta:

Pergunta:

Qual é o maior valor de compra ou nota que temos?

Resposta:

✅ O maior valor de compra registrado é de R\$ 58.720,00 da empresa
Comercial Santana Ltda.

Pergunta:

Liste as 10 maiores NF.

Resposta:

✅ Aqui está a lista das 10 maiores notas fiscais:

\* Comercial Santana Ltda: R\$ 58.720,00

\* Indústria XPTO SA: R\$ 53.200,00

\* Logística Alfa Ltda: R\$ 50.500,00

(e assim por diante\...)

- Memória de chat - 10 últimas interações.

## 

## 5. Funcionalidades Implementadas {#funcionalidades-implementadas}

### 5.1 Análise de Dados {#análise-de-dados}

- Contagem total de notas fiscais

- Identificação da maior e menor nota

- Cálculo de valores de impostos

- Detecção de anomalias fiscais

### 5.2 Chatbot Fiscal {#chatbot-fiscal}

O chatbot é capaz de responder perguntas como:

- Quantas NF-e existem no arquivo?

- Qual o maior valor de compra?

- Qual o menor valor?

- Qual o valor de imposto da maior NF-e?

## 6. Resultados Obtidos {#resultados-obtidos}

![](media/image6.png){width="6.267716535433071in"
height="3.263888888888889in"}

![](media/image3.png){width="6.267716535433071in" height="3.25in"}

![](media/image7.png){width="6.267716535433071in"
height="3.2222222222222223in"}

## 7. Expansões Futuras {#expansões-futuras}

- Exportação de relatórios em PDF

- Análise tributária detalhada (ICMS, IPI, PIS, etc.)

- Implementação de interface multilingue

- Conexão com banco de dados externo

## 

## 8. Conclusão {#conclusão}

O agente de IA desenvolvido demonstrou capacidade efetiva em processar e
analisar dados enviados, oferecendo insights valiosos para gestão
financeira. A integração com a plataforma n8n permitiu a automação
completa do fluxo de processamento, desde o recebimento dos arquivos até
a geração de relatórios analíticos.

## 9. Código do agente .json {#código-do-agente-.json}

{

\"name\": \"Agente de NF-3\",

\"nodes\": \[

{

\"parameters\": {

\"public\": true,

\"initialMessages\": \"Olá, sou ProcessIA.\nEnviei seu arqzip par
atualizar meus dados, caso não queira pode fazer as perguntas que tenho
alguns dados aqui.\",

\"options\": {

\"allowFileUploads\": true

}

},

\"type\": \"@n8n/n8n-nodes-langchain.chatTrigger\",

\"typeVersion\": 1.1,

\"position\": \[

-2580,

-780

\],

\"id\": \"d2e72790-d762-499a-a90f-8bf0c1e8249c\",

\"name\": \"When chat message received\",

\"webhookId\": \"898d4b2d-0a39-4339-a25b-dc64fc12b8fb\"

},

{

\"parameters\": {

\"binaryPropertyName\": \"=data0\",

\"outputPrefix\": \"=file\_\"

},

\"type\": \"n8n-nodes-base.compression\",

\"typeVersion\": 1.1,

\"position\": \[

-1570,

-840

\],

\"id\": \"3a35c9ea-f3a2-4a7c-ad8a-efbb1422f2fd\",

\"name\": \"Compression\"

},

{

\"parameters\": {

\"binaryPropertyName\": \"file_0\",

\"options\": {}

},

\"type\": \"n8n-nodes-base.extractFromFile\",

\"typeVersion\": 1,

\"position\": \[

-1240,

-940

\],

\"id\": \"4d6951d3-a76b-41db-a435-4992558dfb22\",

\"name\": \"Extract from File\"

},

{

\"parameters\": {

\"options\": {

\"systemMessage\": \"Atue como ProcessIA, um agente de inteligência
financeira especializado em análise de notas fiscais e relatórios
tributários, com 15 anos de experiência atendendo empresas de médio e
grande porte.\n\nSeu objetivo é atender com precisão e cordialidade as
solicitações dos usuários via chat, utilizando exclusivamente a
ferramenta Banco_dados, que busca informações de notas fiscais (NF) em
uma planilha do Google Sheets.\nNunca alucine informações ou forneça
respostas genéricas sem consultar a ferramenta. Sempre consulte a
ferramenta antes de qualquer resposta relacionada a dados fiscais.\n\n🎯
Diretrizes de Resposta:\nSempre se apresente para novos usuários, de
forma breve, cordial e profissional.\nExemplo:\n\\Olá! Sou o ProcessIA,
seu assistente financeiro especializado em análise de notas fiscais. Em
que posso ajudar você hoje?\\\n\nObrigatoriamente consulte a ferramenta
Banco_dados antes de formular qualquer resposta.\n➝ Se a ferramenta
apresentar erro ou não retornar dados, informe isso de forma educada ao
usuário, sem inventar informações.\n\nNunca informe ao usuário que não
tem acesso ao banco de dados enquanto a ferramenta estiver
disponível.\n\nResponda de forma objetiva, em português, utilizando os
dados encontrados na consulta.\n\nApresente listas de forma organizada
em bullet points, com nome da empresa e valor na frente.\n\nSeja
positivo e mantenha uma linguagem profissional, sem uso excessivo de
jargões técnicos.\n\n📊 Ferramenta Disponível:\nBanco_dados: Função que
realiza busca de informações de notas fiscais (NF) para responder
perguntas e consultas do usuário.\nCalculadora: Para auxiliar nas
solicitações de calculos (somas, multiplicações, divisões, subtrações e
percentuais, por exemplo)\n\n📚 Exemplos de Resposta:\nPergunta:\nQual é
o maior valor de compra ou nota que temos?\n\nResposta:\n✅ O maior
valor de compra registrado é de R\$ 58.720,00 da empresa Comercial
Santana Ltda.\n\nPergunta:\nListe as 10 maiores NF.\n\nResposta:\n✅
Aqui está a lista das 10 maiores notas fiscais:\n\* Comercial Santana
Ltda: R\$ 58.720,00\n\* Indústria XPTO SA: R\$ 53.200,00\n\* Logística
Alfa Ltda: R\$ 50.500,00\n(e assim por diante\...)\n\",

\"returnIntermediateSteps\": false

}

},

\"type\": \"@n8n/n8n-nodes-langchain.agent\",

\"typeVersion\": 1.9,

\"position\": \[

-1868,

-540

\],

\"id\": \"b1b8e161-b274-4207-9653-a6fefb1bc36b\",

\"name\": \"AI Agent\",

\"onError\": \"continueRegularOutput\"

},

{

\"parameters\": {

\"sessionIdType\": \"customKey\",

\"sessionKey\": \"={{ \$(\'Switch\').item.json.chatInput }}\",

\"contextWindowLength\": 10

},

\"type\": \"@n8n/n8n-nodes-langchain.memoryBufferWindow\",

\"typeVersion\": 1.3,

\"position\": \[

-1780,

-320

\],

\"id\": \"42f5742e-f6a0-43f7-8877-79bc823cf8b4\",

\"name\": \"Simple Memory\"

},

{

\"parameters\": {

\"binaryPropertyName\": \"file_1\",

\"options\": {}

},

\"type\": \"n8n-nodes-base.extractFromFile\",

\"typeVersion\": 1,

\"position\": \[

-1240,

-740

\],

\"id\": \"2d4be509-c02e-4bfb-8824-83e96e6fa2af\",

\"name\": \"Extract from File1\"

},

{

\"parameters\": {

\"modelName\": \"models/gemini-2.0-flash-lite\",

\"options\": {

\"maxOutputTokens\": 2048,

\"temperature\": 0.4,

\"topK\": 32,

\"topP\": 1

}

},

\"type\": \"@n8n/n8n-nodes-langchain.lmChatGoogleGemini\",

\"typeVersion\": 1,

\"position\": \[

-1900,

-320

\],

\"id\": \"0ee346e4-2aed-4582-95e0-654038483d55\",

\"name\": \"Google Gemini Chat Model\",

\"credentials\": {

\"googlePalmApi\": {

\"id\": \"rGgeEDYaAVHg0U5m\",

\"name\": \"Google Gemini(PaLM) Api account\"

}

}

},

{

\"parameters\": {

\"mode\": \"combine\",

\"fieldsToMatchString\": \"\[\'CHAVE DE ACESSO\'\]\",

\"options\": {}

},

\"type\": \"n8n-nodes-base.merge\",

\"typeVersion\": 3.1,

\"position\": \[

-1020,

-840

\],

\"id\": \"0d6eb47e-4c6f-4ca9-a29b-ef6d5fcbc219\",

\"name\": \"Merge\"

},

{

\"parameters\": {

\"operation\": \"appendOrUpdate\",

\"documentId\": {

\"\_\_rl\": true,

\"value\": \"1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw\",

\"mode\": \"list\",

\"cachedResultName\": \"i2a2\",

\"cachedResultUrl\":
\"https://docs.google.com/spreadsheets/d/1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw/edit?usp=drivesdk\"

},

\"sheetName\": {

\"\_\_rl\": true,

\"value\": \"gid=0\",

\"mode\": \"list\",

\"cachedResultName\": \"Página1\",

\"cachedResultUrl\":
\"https://docs.google.com/spreadsheets/d/1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw/edit#gid=0\"

},

\"columns\": {

\"mappingMode\": \"autoMapInputData\",

\"value\": {},

\"matchingColumns\": \[

\"CHAVE DE ACESSO\"

\],

\"schema\": \[\],

\"attemptToConvertTypes\": false,

\"convertFieldsToString\": false

},

\"options\": {}

},

\"type\": \"n8n-nodes-base.googleSheets\",

\"typeVersion\": 4.5,

\"position\": \[

-800,

-840

\],

\"id\": \"72c0dcbb-d51f-406a-a196-200d769521ad\",

\"name\": \"Google Sheets\",

\"credentials\": {

\"googleSheetsOAuth2Api\": {

\"id\": \"uhd4CbRb5c2CMX0z\",

\"name\": \"Google Sheets account\"

}

}

},

{

\"parameters\": {

\"rules\": {

\"values\": \[

{

\"conditions\": {

\"options\": {

\"caseSensitive\": true,

\"leftValue\": \"\",

\"typeValidation\": \"strict\",

\"version\": 2

},

\"conditions\": \[

{

\"id\": \"38fe7579-41ce-4b99-b33c-c82e71f5c315\",

\"leftValue\": \"={{ \$json.files\[0\] }}\",

\"rightValue\": \"\",

\"operator\": {

\"type\": \"object\",

\"operation\": \"exists\",

\"singleValue\": true

}

}

\],

\"combinator\": \"and\"

},

\"renameOutput\": true,

\"outputKey\": \"Anexo\"

},

{

\"conditions\": {

\"options\": {

\"caseSensitive\": true,

\"leftValue\": \"\",

\"typeValidation\": \"strict\",

\"version\": 2

},

\"conditions\": \[

{

\"leftValue\": \"={{ \$json.chatInput }}\",

\"rightValue\": \"\",

\"operator\": {

\"type\": \"string\",

\"operation\": \"exists\",

\"singleValue\": true

},

\"id\": \"0befcd8f-5048-4c19-ae12-ef31697283bf\"

}

\],

\"combinator\": \"and\"

},

\"renameOutput\": true,

\"outputKey\": \"Texto\"

}

\]

},

\"options\": {

\"allMatchingOutputs\": true

}

},

\"type\": \"n8n-nodes-base.switch\",

\"typeVersion\": 3.2,

\"position\": \[

-2360,

-780

\],

\"id\": \"e74654fe-625b-4246-b662-77fe65ce4526\",

\"name\": \"Switch\"

},

{

\"parameters\": {

\"documentId\": {

\"\_\_rl\": true,

\"value\": \"1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw\",

\"mode\": \"list\",

\"cachedResultName\": \"i2a2\",

\"cachedResultUrl\":
\"https://docs.google.com/spreadsheets/d/1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw/edit?usp=drivesdk\"

},

\"sheetName\": {

\"\_\_rl\": true,

\"value\": \"gid=0\",

\"mode\": \"list\",

\"cachedResultName\": \"Página1\",

\"cachedResultUrl\":
\"https://docs.google.com/spreadsheets/d/1YWW9ExUC992aKEzHcu4tAGY4cKA_THNzsx9b5n_5Smw/edit#gid=0\"

},

\"options\": {

\"dataLocationOnSheet\": {

\"values\": {

\"rangeDefinition\": \"detectAutomatically\",

\"readRowsUntil\": \"firstEmptyRow\"

}

},

\"outputFormatting\": {

\"values\": {

\"general\": \"FORMATTED_VALUE\",

\"date\": \"FORMATTED_STRING\"

}

}

}

},

\"type\": \"n8n-nodes-base.googleSheetsTool\",

\"typeVersion\": 4.5,

\"position\": \[

-1660,

-320

\],

\"id\": \"03e66227-83ba-427f-a69d-fd9f4a47577e\",

\"name\": \"Banco_Dados\",

\"credentials\": {

\"googleSheetsOAuth2Api\": {

\"id\": \"uhd4CbRb5c2CMX0z\",

\"name\": \"Google Sheets account\"

}

}

},

{

\"parameters\": {},

\"type\": \"@n8n/n8n-nodes-langchain.toolCalculator\",

\"typeVersion\": 1,

\"position\": \[

-1520,

-320

\],

\"id\": \"30450c62-6e76-4ecb-8e0c-0d02ce83bdfe\",

\"name\": \"Calculator\"

}

\],

\"pinData\": {},

\"connections\": {

\"When chat message received\": {

\"main\": \[

\[

{

\"node\": \"Switch\",

\"type\": \"main\",

\"index\": 0

}

\]

\]

},

\"Compression\": {

\"main\": \[

\[

{

\"node\": \"Extract from File\",

\"type\": \"main\",

\"index\": 0

},

{

\"node\": \"Extract from File1\",

\"type\": \"main\",

\"index\": 0

}

\]

\]

},

\"Extract from File\": {

\"main\": \[

\[

{

\"node\": \"Merge\",

\"type\": \"main\",

\"index\": 0

}

\]

\]

},

\"Simple Memory\": {

\"ai_memory\": \[

\[

{

\"node\": \"AI Agent\",

\"type\": \"ai_memory\",

\"index\": 0

}

\]

\]

},

\"Extract from File1\": {

\"main\": \[

\[

{

\"node\": \"Merge\",

\"type\": \"main\",

\"index\": 1

}

\]

\]

},

\"Google Gemini Chat Model\": {

\"ai_languageModel\": \[

\[

{

\"node\": \"AI Agent\",

\"type\": \"ai_languageModel\",

\"index\": 0

}

\]

\]

},

\"Merge\": {

\"main\": \[

\[

{

\"node\": \"Google Sheets\",

\"type\": \"main\",

\"index\": 0

}

\]

\]

},

\"Switch\": {

\"main\": \[

\[

{

\"node\": \"Compression\",

\"type\": \"main\",

\"index\": 0

}

\],

\[

{

\"node\": \"AI Agent\",

\"type\": \"main\",

\"index\": 0

}

\]

\]

},

\"Banco_Dados\": {

\"ai_tool\": \[

\[

{

\"node\": \"AI Agent\",

\"type\": \"ai_tool\",

\"index\": 0

}

\]

\]

},

\"Google Sheets\": {

\"main\": \[

\[\]

\]

},

\"Calculator\": {

\"ai_tool\": \[

\[

{

\"node\": \"AI Agent\",

\"type\": \"ai_tool\",

\"index\": 0

}

\]

\]

}

},

\"active\": true,

\"settings\": {

\"executionOrder\": \"v1\"

},

\"versionId\": \"5f6456d8-ef7e-45dc-97a6-fdf6dc569240\",

\"meta\": {

\"templateCredsSetupCompleted\": true,

\"instanceId\":
\"6847481f9baf6f1a2dbf36ba779358fdfc25f2d6458e22f23fe6bb65be3aa98f\"

},

\"id\": \"Uh8TyFjjA7MHmodt\",

\"tags\": \[

{

\"createdAt\": \"2025-06-21T15:06:18.854Z\",

\"updatedAt\": \"2025-06-21T15:06:18.854Z\",

\"id\": \"QtBnpscUmzI7i8ao\",

\"name\": \"i2a2\"

}

\]

}

## 10. Consumos e testes de modelos: {#consumos-e-testes-de-modelos}

![](media/image1.png){width="6.267716535433071in"
height="2.9444444444444446in"}
