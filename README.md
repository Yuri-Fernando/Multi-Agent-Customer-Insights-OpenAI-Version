# Multi-Agent-Customer-Insights-OpenAI-Version

Pipeline multiagente para geração de insights de clientes, usando agentes especializados para **research**, **analysis** e **strategy**, coordenados por um orquestrador central.

Arquitetura extensível, plugável e organizada de forma profissional para demonstrar **domínio técnico**, **clareza arquitetural** e **boas práticas de engenharia**.

---

##  Objetivo do Projeto

Criar um pipeline de IA capaz de:

- Ler dados de um cliente  
- Distribuir informações para agentes especializados  
- Agregar insights estruturados  
- Gerar um relatório final pronto para análise  

O design permite adicionar novos agentes, trocar modelos, ajustar prompts e escalar o pipeline **sem alterar o código principal**.
                                           
---

## Extensibilidade
Fácil adicionar:
- Novos agentes (FinanceAgent, RiskAgent, PersonaAgent)
- Templates diferentes de relatório
- Outro cliente LLM
- Pipeline assíncrono
- Integração com banco de dados
- Ingestão automática de CSV, CRM ou APIs

---

## CI/CD com GitHub Actions
- O projeto já está configurado para:
- Rodar testes automáticos (pytest)
- Validar lint e estilo
- Verificar imports e dependências
- Prevenir regressões em cada merge
- Isso garante que o pipeline permaneça íntegro, confiável e reproduzível.

---

## Por que essa Arquitetura Demonstra Seriedade? 
- Separação clara de responsabilidades (SRP)
- Agentes isolados, substituíveis e testáveis
- Orquestração centralizada
- LLM desacoplado da lógica de negócio
- Estrutura realista de projeto (src, tests, utils)
- Registro plugável de agentes
- Report Builder transforma saída bruta em entrega utilizável
- Código fácil de manter e escalar

---

##  Estrutura do Projeto

```text
.
├── .git/
│   └── workflows/
│       └── ci.yml        # GitHub Actions (CI)
│
├── venv/
│
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
│   │   ├── registry.py   # Registro plugável de agentes
│   │   └── __init__.py
│   │
│   ├── tools/
│   │   ├── llm_client.py
│   │   ├── embeddings.py
│   │   └── vector_store.py
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

## Como Funciona o Pipeline:
 Entrada
Objeto JSON ou dicionário Python com dados do cliente:
{
  "name": "Maria Silva",
  "age": 34,
  "segment": "Alta Renda",
  "income": 18000,
  "behavior": "Compra frequente online",
  "history": "Atrasos ocasionais, bom relacionamento"
}

 Orquestrador
O Orchestrator distribui o payload entre os agentes:
results = orchestrator.run(customer)

Retorno esperado:
{
  "research": "...",
  "analysis": "...",
  "strategy": "..."
}
 Agentes Especializados
| Agente            | Função                                           | Arquivo             |
| ----------------- | ------------------------------------------------ | ------------------- |
| **ResearchAgent** | Analisa padrões, comportamento e sinais de churn | `research_agent.py` |
| **AnalysisAgent** | Gera diagnóstico e interpreta riscos             | `analysis_agent.py` |
| **StrategyAgent** | Cria recomendações práticas e planos de ação     | `strategy_agent.py` |

Todos herdam de:
core/base_agent.py
