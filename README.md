Comparação entre Azure Functions, Aplicativos Lógicos e WebJobs

Este projeto apresenta uma análise completa das diferenças entre Azure Functions, Azure Logic Apps e WebJobs, incluindo características funcionais, cenários de uso, planos de hospedagem e comportamento de escalabilidade.

Visão Geral

Os três serviços permitem execução de tarefas automatizadas no Azure, porém com abordagens diferentes:

Azure Functions → Serverless orientado a código
Azure Logic Apps → Integração visual declarativa
WebJobs → Processamento em background dentro do App Service
Comparação: Azure Functions vs Aplicativos Lógicos
Categoria	Azure Functions	Aplicativos Lógicos
Desenvolvimento	Primeiro o código (obrigatório)	Primeiro o designer (declarativo)
Conectividade	Tipos internos + código personalizado	Grande conjunto de conectores + B2B + conectores customizados
Ações	Cada atividade é uma função	Grande conjunto de ações pré-definidas
Monitoramento	Azure Application Insights	Azure Monitor + Portal Azure
Gerenciamento	API REST, Visual Studio	Portal Azure, REST, PowerShell, Visual Studio
Execução	Local ou nuvem	Run-anywhere
Comparação: Azure Functions vs WebJobs
Recurso	Azure Functions	WebJobs
Serverless com escala automática	Sim	Não
Desenvolver no navegador	Sim	Não
Pagamento por uso	Sim	Não
Integração com Logic Apps	Sim	Não
Execução por gatilho	Sim	Sim
Timer Trigger	Sim	Sim
Queue Storage	Sim	Sim
Blob Storage	Sim	Sim
Service Bus	Sim	Sim
Cosmos DB	Sim	Sim
Event Hub	Sim	Sim
HTTP/WebHook	Sim	Não
Quando usar Azure Functions

Utilize Azure Functions quando:

Precisar de execução sob demanda
Arquitetura serverless
Pagamento por execução
APIs leves
Processamento orientado a eventos
Microserviços
Webhooks
Jobs agendados

Exemplos:

Processar mensagens da fila
Executar timer
Webhook GitHub
API HTTP serverless
Processamento de arquivos
Quando usar Azure Logic Apps

Utilize Logic Apps quando:

Integração entre sistemas
Fluxos declarativos
Orquestração de processos
Integração com SaaS
Sem necessidade de código

Exemplos:

Enviar email ao criar registro
Integração SAP
Integração Dynamics
Fluxos approval workflow
Integração B2B
Quando usar WebJobs

Utilize WebJobs quando:

Aplicação já roda no App Service
Jobs em background contínuos
Worker permanente
Processamento batch
Não precisa serverless

Exemplos:

Worker queue
Job contínuo
Processamento batch
Limpeza de banco
Processamento noturno
Azure Functions - Tipos de Trigger

Principais triggers:

HTTP Trigger
Timer Trigger
Blob Trigger
Queue Trigger
Service Bus Trigger
Event Hub Trigger
Cosmos DB Trigger
Event Grid Trigger

Exemplo HTTP Trigger:

[FunctionName("HelloFunction")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", "post")]
HttpRequest req,
ILogger log)
{
    return new OkObjectResult("Hello Azure Functions");
}
Azure Functions - Bindings

Bindings permitem conectar a serviços sem escrever código manual.

Input Bindings:

Blob Storage
Queue Storage
Cosmos DB
Table Storage
Service Bus

Output Bindings:

Blob Storage
Queue
Service Bus
Cosmos DB
Event Hub

Exemplo binding:

[FunctionName("QueueOutput")]
[return: Queue("fila")]
public static string Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
    return "Mensagem fila";
}
Planos de Hospedagem Azure Functions

Azure Functions possui três planos principais.

Consumption Plan

Características:

Escala automática
Pagamento por execução
Sem servidor dedicado
Cold start possível
Ideal para cargas variáveis

Escala:

0 → milhares automaticamente

Premium Plan

Características:

Sem cold start
Instâncias pré-aquecidas
Escala automática
VNET support
Mais performance

Indicado para:

Alta performance
Baixa latência
Integração privada

App Service Plan

Características:

Instância dedicada
Sem cold start
Escala manual
Mesmo plano do App Service

Indicado para:

Controle total
Carga constante
Já possui App Service

Comparação Planos Azure Functions
Recurso	Consumption	Premium	App Service
Escala automática	Sim	Sim	Manual
Cold start	Sim	Não	Não
Pagamento por execução	Sim	Não	Não
VNET	Não	Sim	Sim
Instância dedicada	Não	Sim	Sim
Alta performance	Médio	Alto	Alto
Escalabilidade Azure Functions

Azure Functions escala automaticamente baseado em:

Número de eventos
Fila Azure Storage
Service Bus
HTTP requests
Event Hub
Cosmos DB

Exemplo:

Fila com 1000 mensagens
Azure Functions cria múltiplas instâncias
Cada instância processa mensagens
Escala automaticamente

Escala horizontal automática.

Modelo Serverless

Azure Functions utiliza modelo:

Sem gerenciamento de servidor
Escala automática
Pagamento por uso
Alta disponibilidade

Fluxo:

Evento ocorre
Function dispara
Executa código
Escala automaticamente
Encerramento

Azure Functions vs Logic Apps

Azure Functions:

Orientado a código
Mais flexível
Mais controle
Melhor performance

Logic Apps:

Visual
Integração SaaS
Orquestração
Sem código

Uso comum:

Logic App chama Azure Function.

Azure Functions vs WebJobs

Azure Functions:

Serverless
Escala automática
Triggers nativos
Bindings

WebJobs:

Executa no App Service
Sem escala automática
Worker contínuo
Controle manual

Cenários de Arquitetura

Arquitetura 1

Logic App → Azure Function → SQL

Arquitetura 2

Queue → Azure Function → Blob

Arquitetura 3

HTTP → Azure Function → Service Bus

Arquitetura 4

Timer → Azure Function → Database cleanup

Monitoramento

Azure Functions suporta:

Application Insights
Logs estruturados
Métricas
Tracing distribuído

Exemplo:

Requests
Failures
Execution time
Dependências

Segurança

Azure Functions suporta:

Function Key
Azure AD
Managed Identity
IP restriction
VNET Integration

Deploy Azure Functions

Criar function:

dotnet new func

Executar local:

func start

Deploy:

func azure functionapp publish app-name
Conclusão

Azure Functions

Serverless
Escala automática
Pagamento por uso
Código

Logic Apps

Fluxos visuais
Integração SaaS
Orquestração

WebJobs

Worker background
App Service
Execução contínua

Resumo:

Azure Functions → processamento serverless
Logic Apps → integração e workflow
WebJobs → jobs em background no App Service
