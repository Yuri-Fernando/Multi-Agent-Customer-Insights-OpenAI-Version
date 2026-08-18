# Multi-Agent Customer Insights — OpenAI Version

### Multi-Agent AI · Customer Intelligence · LLM Orchestration · Research · Analysis · Strategy

## Status

🟢 **Concluído — Projeto de portfólio / Multi-Agent AI**

Pipeline multiagente para geração de **insights de clientes**, utilizando agentes especializados em **research, analysis e strategy**, coordenados por um orquestrador central.

O projeto foi estruturado para demonstrar **clareza arquitetural, separação de responsabilidades, extensibilidade e boas práticas de engenharia**, mantendo a lógica de negócio desacoplada do provedor de LLM.

---

## Sobre o projeto

O sistema recebe dados estruturados de um cliente e distribui essas informações entre agentes especializados, consolidando os resultados em um relatório final.

```text
Customer Data
      ↓
Orchestrator
      ↓
┌──────────────┬───────────────┬───────────────┐
│ Research     │ Analysis      │ Strategy      │
│ Agent        │ Agent         │ Agent         │
└──────────────┴───────────────┴───────────────┘
      ↓
Structured Insights
      ↓
Report Builder
      ↓
Final Customer Report
```

A arquitetura permite adicionar novos agentes, substituir modelos, ajustar prompts e expandir o pipeline sem alterar o código principal.

---

## Objetivo

Criar um pipeline de IA capaz de:

- Ler dados estruturados de um cliente;
- Distribuir informações para agentes especializados;
- Gerar análises independentes;
- Agregar insights estruturados;
- Gerar recomendações estratégicas;
- Produzir um relatório final pronto para análise.

O design permite evoluir o sistema para diferentes fontes de dados e cenários de negócio sem alterar o núcleo de orquestração.

---

## Como funciona o pipeline

### Entrada

O pipeline recebe um objeto JSON ou dicionário Python com os dados do cliente.

Exemplo:

```python
customer = {
    "name": "Maria Silva",
    "age": 34,
    "segment": "Alta Renda",
    "income": 18000,
    "behavior": "Compra frequente online",
    "history": "Atrasos ocasionais, bom relacionamento"
}
```

### Orquestrador

O `Orchestrator` distribui o payload entre os agentes:

```python
results = orchestrator.run(customer)
```

Retorno esperado:

```python
{
    "research": "...",
    "analysis": "...",
    "strategy": "..."
}
```

### Agentes especializados

| Agente | Função | Arquivo |
|---|---|---|
| **ResearchAgent** | Analisa padrões, comportamento e sinais de churn | `research_agent.py` |
| **AnalysisAgent** | Gera diagnóstico e interpreta riscos | `analysis_agent.py` |
| **StrategyAgent** | Cria recomendações práticas e planos de ação | `strategy_agent.py` |

Todos os agentes utilizam a abstração:

```text
core/base_agent.py
```

---

## Arquitetura

```text
                    Customer Data
                         │
                         ▼
                 ┌───────────────┐
                 │  Orchestrator │
                 └───────┬───────┘
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
   ┌────────────┐ ┌────────────┐ ┌────────────┐
   │  Research  │ │  Analysis  │ │  Strategy  │
   │    Agent   │ │    Agent   │ │    Agent   │
   └──────┬─────┘ └──────┬─────┘ └──────┬─────┘
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                 ┌───────────────┐
                 │ Report Builder│
                 └───────┬───────┘
                         ▼
                 Final Customer
                     Insights
```

---

## Extensibilidade

A arquitetura foi desenvolvida para permitir a inclusão de novos componentes sem modificar o código principal.

### Novos agentes

Exemplos:

- `FinanceAgent`
- `RiskAgent`
- `PersonaAgent`
- `RetentionAgent`
- `MarketingAgent`

### Novos formatos de relatório

O `Report Builder` pode ser adaptado para gerar diferentes estruturas e formatos de saída.

### Novos provedores de LLM

A camada de cliente LLM é separada da lógica de negócio, permitindo substituir o modelo ou provedor utilizado sem reestruturar o pipeline.

### Novas fontes de dados

O pipeline pode ser expandido para:

- CSV;
- CRM;
- APIs;
- Banco de dados;
- Eventos de comportamento.

### Evoluções arquiteturais

Também existe espaço para:

- Pipeline assíncrono;
- Persistência em banco;
- RAG;
- Memória de agentes;
- Observabilidade;
- Avaliação automatizada.

---

## Princípios de Engenharia

### Separação de responsabilidades

Cada agente possui uma responsabilidade bem definida dentro do pipeline.

### Baixo acoplamento

O orquestrador não depende da implementação interna de cada agente.

### Substituibilidade

Agentes podem ser substituídos ou adicionados sem alterar o núcleo da aplicação.

### Testabilidade

Os componentes principais são isolados e podem ser testados individualmente.

### LLM desacoplado

A comunicação com o modelo de linguagem fica separada da lógica de negócio e da orquestração.

### Arquitetura plugável

O registro de agentes permite incorporar novas implementações sem modificar o fluxo central.

---

## CI/CD com GitHub Actions

O projeto possui configuração de CI utilizando GitHub Actions.

O pipeline automatiza:

- Execução de testes com `pytest`;
- Validação de lint e estilo;
- Verificação de imports;
- Verificação de dependências;
- Detecção de regressões durante merges.

Fluxo:

```text
Git Push / Pull Request
          ↓
   GitHub Actions
          ↓
       Tests
          ↓
        Lint
          ↓
    Validation
          ↓
   Pipeline Status
```

Essa estrutura contribui para manter o projeto reproduzível e facilitar a validação das alterações.

---

## Estrutura do Projeto

```text
Multi-Agent-Customer-Insights-OpenAI-Version/
│
├── .github/
│   └── workflows/
│       └── ci.yml
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
│   │
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
```

---

## Componentes principais

### `core/base_agent.py`

Define a abstração comum para os agentes.

### `core/orchestrator.py`

Coordena o fluxo de execução do sistema multiagente.

### `core/report_builder.py`

Consolida as respostas produzidas pelos agentes em uma saída estruturada.

### `core/types.py`

Centraliza tipos e estruturas compartilhadas.

### `agents/registry.py`

Mantém o registro plugável dos agentes disponíveis.

### `tools/llm_client.py`

Camada responsável pela comunicação com o provedor de LLM.

### `tools/embeddings.py`

Responsável pela geração de embeddings.

### `tools/vector_store.py`

Abstração para armazenamento e recuperação vetorial.

### `utils/`

Conjunto de funções auxiliares para:

- Entrada e saída;
- Sanitização;
- Logging.

---

## Como executar

### Pré-requisitos

- Python;
- Ambiente virtual recomendado;
- Dependências do projeto;
- Credenciais necessárias para o provedor de LLM utilizado.

### Clonar

```bash
git clone <repo-url>
cd Multi-Agent-Customer-Insights-OpenAI-Version
```

### Criar ambiente virtual

Windows:

```powershell
python -m venv venv
venv\Scripts\activate
```

Linux/macOS:

```bash
python -m venv venv
source venv/bin/activate
```

### Instalar dependências

```bash
pip install -r src/requirements.txt
```

Configure as variáveis de ambiente necessárias conforme a configuração do projeto.

---

## Exemplo de execução

```python
from src.core.orchestrator import Orchestrator

customer = {
    "name": "Maria Silva",
    "age": 34,
    "segment": "Alta Renda",
    "income": 18000,
    "behavior": "Compra frequente online",
    "history": "Atrasos ocasionais, bom relacionamento"
}

orchestrator = Orchestrator()

results = orchestrator.run(customer)

print(results)
```

---

## Testes

Executar a suíte:

```bash
pytest tests/
```

Testes principais:

```text
tests/
├── test_agents.py
├── test_orchestrator.py
└── test_report_builder.py
```

O pipeline de CI também executa os testes automaticamente nas alterações submetidas ao repositório.

---

## Tecnologias

| Categoria | Tecnologias |
|---|---|
| Linguagem | Python |
| LLM | OpenAI |
| Embeddings | Embeddings |
| Vector Store | Vector Store |
| Testes | pytest |
| CI/CD | GitHub Actions |
| Arquitetura | Multi-Agent System |
| Engenharia | Modular / Plugável |

---

## Casos de uso

### Customer Intelligence

Análise estruturada de comportamento e características de clientes.

### Churn Analysis

Identificação de padrões e sinais relacionados à evasão.

### Risk Analysis

Possibilidade de adicionar agentes específicos para análise de risco.

### Marketing Intelligence

Geração de estratégias e recomendações personalizadas.

### CRM Intelligence

Transformação de dados de CRM em insights estruturados.

### Financial Intelligence

Inclusão de agentes especializados em análise financeira.

---

## O que este projeto demonstra

- Arquitetura Multi-Agent;
- Orquestração de agentes especializados;
- Agent Registry;
- Separação de responsabilidades;
- Design modular;
- Baixo acoplamento;
- Abstração de LLM;
- Embeddings;
- Vector Store;
- Geração estruturada de relatórios;
- Testes automatizados;
- CI/CD com GitHub Actions;
- Extensibilidade;
- Integração entre IA e Customer Intelligence;
- Boas práticas de engenharia de software.

---

## Limitações

- A qualidade das análises depende dos dados fornecidos;
- A qualidade das respostas depende do modelo LLM utilizado;
- A implementação atual utiliza dados estruturados conforme o schema esperado;
- Integrações externas podem exigir adaptações específicas;
- O pipeline atual é voltado à demonstração da arquitetura multiagente;
- O projeto não representa uma plataforma corporativa de produção.

---

## Melhorias Futuras

- Pipeline assíncrono;
- Integração com bancos de dados;
- Ingestão automática de CSV;
- Integração com CRM;
- Integração com APIs externas;
- Novos agentes especializados;
- Memória persistente;
- RAG;
- Agent evaluation;
- Observabilidade;
- Dashboard de resultados;
- API REST;
- Containerização;
- Integração com workflows de automação;
- Suporte a múltiplos provedores de LLM.

---

## Status Final

🟢 **Concluído**

O pipeline multiagente está implementado e estruturado com:

- ✅ ResearchAgent;
- ✅ AnalysisAgent;
- ✅ StrategyAgent;
- ✅ Orchestrator;
- ✅ Agent Registry;
- ✅ Report Builder;
- ✅ LLM desacoplado da lógica principal;
- ✅ Embeddings;
- ✅ Vector Store;
- ✅ Testes automatizados;
- ✅ GitHub Actions;
- ✅ Estrutura modular;
- ✅ Arquitetura extensível.

O projeto permanece como uma base de portfólio e referência técnica para experimentação e evolução de **Multi-Agent Systems, Customer Intelligence e Agentic AI**.

---

## Licença

Consulte a licença definida no repositório.

---

## Autor

**Yuri Fernando Dubbern**

AI/ML Engineer · Generative AI · Agentic AI · Multi-Agent Systems · Data Engineering

[LinkedIn](https://www.linkedin.com/in/yuridubbern) · [GitHub](https://github.com/Yuri-Fernando) · [Lattes](http://lattes.cnpq.br/7151392692642166) · [Linktree](https://linktr.ee/yuri.f.dubbern)
