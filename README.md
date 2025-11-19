# Multi-Agent-Customer-Insights-OpenAI-Version
Pipeline multiagente para geração de insights de clientes, usando agentes especializados para research, analysis e strategy, coordenados por um orquestrador central. Arquitetura extensível, plugável e organizada de forma profissional para demonstrar domínio técnico, clareza arquitetural e boas práticas de engenharia.

📌 Objetivo do Projeto
Criar um pipeline de IA capaz de:
- Ler dados de um cliente.
- Distribuir para agentes especializados.
- Agregar insights estruturados.
- Gerar um relatório final pronto para análise.

O design permite adicionar novos agentes, mudar modelos, ajustar prompts e escalar o pipeline sem alterar o código principal.

📂 Estrutura do Projeto:
.
├── .git/
       ├── Workflows/ci.yml
├── venv/ (Geral)
├── data/
│   ├── samples/
│   └── outputs/
│
├── src/
│   ├── main.py
│   ├── env.py
│   ├── pyproject.toml
│   ├── requirements.txt
│
│   ├── core/
│   │   ├── base_agent.py
│   │   ├── orchestrator.py
│   │   ├── report_builder.py
│   │   └── types.py
│   │
│   ├── implementations/
│   │   ├── research_agent.py
│   │   ├── analysis_agent.py
│   │   ├── strategy_agent.py
│   │   └── __init__.py
│   │
│   ├── agents/
│   │   ├── registry.py
│   │   └── __init__.py
│   │
│   ├── tools/
│   │   └── llm_client.py
│   │
│   └── utils/
│       ├── io.py
│       ├── sanitize.py
│       └── logger.py
│
├── tests/
│   ├── test_agents.py
│   ├── test_orchestrator.py
│   └── test_report_builder.py
│
└── README.md

⚙️ Como Funciona o Pipeline
1. Entrada
Um objeto JSON ou um dicionário Python com dados do cliente: (Pode vir de um dataset)
{
  "name": "Maria Silva",
  "age": 34,
  "segment": "Alta Renda",
  "income": 18000,
  "behavior": "Compra frequente online",
  "history": "Atrasos ocasionais, bom relacionamento"
}

2. Orquestrador
O Orchestrator distribui o pacote de informação entre os agentes:
results = orchestrator.run(customer)
Retorna:
{
  "research": "...",
  "analysis": "...",
  "strategy": "..."
}

3. Agentes
Cada agente faz uma parte do pipeline:
| Agente            | Função                                                    | Arquivo             |
| ----------------- | --------------------------------------------------------- | ------------------- |
| **ResearchAgent** | Analisa padrões, sinais de churn, comportamento           | `research_agent.py` |
| **AnalysisAgent** | Gera diagnóstico, interpreta padrões, encontra risco real | `analysis_agent.py` |
| **StrategyAgent** | Cria recomendações práticas, planos e ações               | `strategy_agent.py` |

Todos herdam de:
core/base_agent.py

4. Report Builder
Monta o relatório final estruturado.
core/report_builder.py

📐 Diagrama de Fluxo (ASCII)

                     +---------------------+
                     |  Customer Payload   |
                     +----------+----------+
                                |
                                v
                     +---------------------+
                     |     Orchestrator    |
                     +----------+----------+
                                |
        -------------------------------------------------
        |                       |                       |
        v                       v                       v
+---------------+      +----------------+      +------------------+
| ResearchAgent |      | AnalysisAgent |      | StrategyAgent     |
+-------+-------+      +-------+--------+      +---------+--------+
        |                      |                         |
        ------------------------                         |
                       |                                 |
                       v                                 v
                 +------------------+          +---------------------+
                 |  Aggregated Dict | -------> |   Report Builder    |
                 +------------------+          +-----------+---------+
                                                         |
                                                         v
                                              +----------------------+
                                              | Final Structured PDF |
                                              +----------------------+

🧩 Extensibilidade
Fácil adicionar:
-novos agentes (ex.: FinanceAgent, RiskAgent, PersonaAgent)
-templates diferentes de relatório
-outro cliente LLM
-pipeline async
-integração com banco de dados
-ingestão automática de CSV, CRM, API etc.

🎯 Por que essa arquitetura demonstra Seriedade
-Modulação clara (SRP).
-Agentes isolados, substituíveis e testáveis.
-Orquestração centralizada.
-LLM desacoplado.
-Estrutura de projeto realista (src, tests, utils, core).
-Agentes plugáveis via registry.
-Report Builder transforma resultado bruto em entrega utilizável.
-Estrutura fácil de manter e expandir.



