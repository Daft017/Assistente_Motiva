# engman-copilot

Assistente de Inteligência Artificial Generativa para Engenharia de Manutenção — Motiva Rodovias (Programas PRIME e MIND)

## Contexto Acadêmico

- **Disciplina:** Prompt Engineering & Artificial Intelligence
- **Curso:** Ciência da Computação - 1º Ano (Semestre 2026.2)
- **Professor:** Jorge Luiz Gomes
- **Parceiro:** Motiva Rodovias (Engenharia de Manutenção - PRIME / MIND)
- **Formato:** Trabalho em grupo (3 a 5 alunos)

## Pergunta Norteadora

> Como um assistente de Inteligência Artificial, construído com Inteligência Artificial Generativa, pode apoiar a equipe de Engenharia de Manutenção da Motiva a diagnosticar, priorizar e documentar intervenções em ativos eletroeletrônicos rodoviários — usando apenas informação que esteja na base de conhecimento da empresa e nunca inventando dados?

## Problema Abordado

O CCO (Centro de Controle Operacional) da Motiva recebe dezenas de alarmes simultâneos de ativos ITS (CFTV, PMV, SAT, SCA, detectores de incidente) distribuídos por centenas de quilômetros de rodovia. Hoje, a triagem — decidir o que é falha real de equipamento e o que é interferência ambiental (chuva, cerração, glare) — depende inteiramente do julgamento do operador humano em tempo real, sem apoio sistemático.

Isso gera dois riscos opostos e caros: alarme falso tratado como real aciona deslocamento desnecessário de técnico em campo (custo operacional); alarme real descartado como ambiental atrasa o atendimento e aumenta o risco à segurança viária. Com a Motiva operando mais de 5 mil km de rodovias e cerca de 2 milhões de veículos pedagiados por dia, a escala do problema torna inviável a triagem manual sem apoio de IA.

## Recorte Escolhido: Recorte B — Operação e Priorização de Campo

**Justificativa técnica:** O Recorte B foca no suporte ao operador do CCO (Centro de Controle Operacional) e ao coordenador na triagem de alarmes em tempo real, diferenciando falhas reais de ativos de condições ambientais (chuva, cerração, glare), definindo prioridades e gerando ordens de serviço (OS). Essa escolha está diretamente alinhada com a operação rodoviária da Motiva, onde a rápida distinção entre falha de equipamento e interferência ambiental impacta a segurança dos usuários e a disponibilidade da via.

## Personas

- **Persona principal:** Operador do CCO — recebe alarmes em tempo real. Exige saídas estruturadas e classificadas (real vs. ambiental/indeterminado) com prioridade e ação recomendada.
- **Persona secundária:** Técnico em Campo — em campo, pelo celular, com o equipamento nas mãos. Precisa de instruções curtas, passo a passo, linguagem simples, com forte ênfase em EPI e desligamento seguro.

## Escopo

**Dentro do escopo:**
- Triagem de alarmes em tempo real no CCO
- Classificação de falha real vs. condição ambiental (chuva, cerração, glare)
- Definição de prioridade de atendimento
- Geração de texto de Ordem de Serviço (OS)
- Consulta a histórico de falhas por TAG (dentro da base de conhecimento)
- Recomendação de tipo de intervenção (corretiva, preventiva, inspeção, CBM)
- Instruções curtas de campo para técnicos (EPI, desligamento seguro)

**Fora do escopo (recusa educada obrigatória):**
- Emitir laudos técnicos com validade legal (ART)
- Liberar ou intervir fisicamente em equipamentos
- Substituir normas oficiais de segurança elétrica (NR-10 / NR-35)
- Responder sobre temas alheios à manutenção (esportes, política, receitas)
- Inventar números de série, TAGs, modelos, normas ou históricos
- Tratar dados pessoais em desacordo com a LGPD

## Arquitetura da Solução

Fluxo completo com os 8 blocos essenciais (entrada → guardrail de entrada → montagem de contexto com RAG → chamada ao LLM → decisão de tool → execução de tool → guardrail de saída → resposta + histórico), com diagrama Mermaid e descrição bloco a bloco em [`/docs/arquitetura.md`](docs/arquitetura.md).

As duas decisões mais importantes do fluxo: (1) o guardrail de entrada recusa pedidos fora de escopo, jailbreak ou com dado pessoal **antes** de chamar o modelo, reduzindo custo e superfície de ataque; (2) o guardrail de saída pode forçar uma nova geração se a resposta não citar fonte, não distinguir FATO de HIPÓTESE ou não trouxer nível de confiança — nenhuma alucinação sai sem passar por essa checagem.

## Stack e Justificativa Técnica

Comparação completa de modelos e vector stores em [`/docs/decisoes_tecnicas.md`](docs/decisoes_tecnicas.md).

**Resumo:** GPT-4o selecionado para o MVP pelo suporte maduro a function calling e saídas estruturadas em JSON (facilita validação das 4 tools); Claude 3.5 Sonnet como alternativa válida; Llama-3.1 70B avaliado para fases futuras com infraestrutura própria. Para o vector store do RAG, Chroma foi selecionado para o protótipo (Sprints 3/4) por ser leve e não exigir infraestrutura de nuvem imediata; Pinecone e FAISS avaliados como alternativas para escala/produção local. Trade-off aceito: modelo em nuvem ganha em capacidade de raciocínio, mas exige cuidado com dados confidenciais — mitigado nesta fase pelo uso exclusivo de dados simulados.

## Base de Conhecimento

Inventário completo (10 categorias de documento, todos simulados exceto glossário e normas) em [`/data/knowledge_base/inventario.md`](data/knowledge_base/inventario.md): catálogo de 30 ativos, plano de manutenção preventiva, histórico de falhas do FSM (50+ registros), 3 POPs, fichas técnicas, matriz de criticidade, glossário e normas NR-10/NR-35.

**Uso no RAG:** chunks de 512 tokens com sobreposição de 50, metadados por TAG/tipo de alarme/localização/data/criticidade, recuperação por busca híbrida (semântica + palavra-chave por TAG) — justificativa detalhada no próprio inventário.

## System Prompt

Resumo: estruturado em 7 blocos (`PAPEL`, `OBJETIVO`, `ESCOPO`, `REGRAS`, `FORMATO`, `TOM`, `BORDA`), com regras anti-alucinação numeradas, distinção obrigatória entre FATO e HIPÓTESE, frase padrão de recusa e comportamento definido para casos de borda (saudação, pergunta ambígua, dado inexistente, conversa longa, pedido hostil). Versão completa com comentários bloco a bloco em [`/prompts/system_prompt.md`](prompts/system_prompt.md).

## Eval Set

14 casos cobrindo as 8 categorias obrigatórias (factual, instrucional, ambíguo, dado_inexistente, out_of_scope, jailbreak, risco_operacional, memoria_contexto), cada um com contexto esperado, resposta ideal e critérios de avaliação verificáveis. Arquivo completo em [`/evals/sprint1_eval_set.json`](evals/sprint1_eval_set.json).

## Riscos e Mitigações

8 riscos mapeados (alucinação, prompt injection, risco operacional, viés na priorização, LGPD, confidencialidade operacional, excesso de confiança, estouro de contexto), cada um com impacto, mitigação concreta e rastreabilidade até o bloco do system prompt, a tool ou o caso de eval correspondente. Matriz completa em [`/docs/riscos_lgpd.md`](docs/riscos_lgpd.md).

## Limitações Conhecidas

- O assistente depende inteiramente da qualidade e atualização da base de conhecimento da Motiva; TAGs ou ativos não cadastrados resultam em "não sei", mesmo que o alarme seja real.
- A classificação de falha real vs. ambiental é probabilística, não determinística — decisões de alta criticidade ainda exigem validação humana do coordenador antes de dispensar o atendimento.
- O system prompt e o eval set nesta fase não foram executados contra um modelo real; a validação de viabilidade ocorre nas Sprints 03/04.
- Dados de condição ambiental (chuva, cerração, glare) dependem de integração com o SCA (Sistema Ambiental) da Motiva, que não está especificada nesta etapa — é uma tool/fonte adicional a ser definida.

## Referências

- Briefing "Inovação Aberta FIAP — EngMan Motiva" (16/09/2026)
- Documento do Challenge Integrador — Sprints 01 e 02 (FIAP × Motiva Rodovias, Prof. Jorge Luiz Gomes)
- Normas Regulamentadoras NR-10 (Segurança em Instalações e Serviços em Eletricidade) e NR-35 (Trabalho em Altura)
- Materiais da disciplina Prompt Engineering & Artificial Intelligence (Módulos 1 e 2: zero/one/few-shot, Chain-of-Thought, role prompting)

## Tools Especificadas

Contrato completo em [`/tools/tools_spec.json`](tools/tools_spec.json). Nenhuma tool é implementada nesta etapa — são especificações (JSON Schema) que serão executadas de forma mockada nas Sprints 03/04.

| Tool | O que faz | Parâmetros principais |
|------|-----------|------------------------|
| `consultar_historico_tag` | Busca o histórico de falhas/manutenções de um ativo na base de conhecimento, sem inventar dados | `tag`, `limite_registros` |
| `classificar_falha_ambiental` | Classifica um alarme como falha real, ambiental/indeterminado ou sem informação | `tag`, `tipo_alarme`, `condicao_ambiental_informada` |
| `verificar_seguranca_epi` | Verifica se há POP cadastrado e os EPIs obrigatórios antes de liberar orientação de campo | `tipo_intervencao`, `ativo_energizado` |
| `gerar_ordem_servico` | Monta o texto estruturado da OS com os campos obrigatórios do POP-03 | `tag`, `localizacao_km`, `tipo_intervencao`, `prioridade` |

## Estrutura do Repositório

```
engman-copilot/
|-- README.md
|-- .gitignore
|-- docs/
|   |-- arquitetura.md
|   |-- riscos_lgpd.md
|   |-- decisoes_tecnicas.md
|-- prompts/
|   |-- system_prompt.md
|-- evals/
|   |-- sprint1_eval_set.json
|-- data/
|   |-- knowledge_base/
|       |-- inventario.md
|-- tools/
|   |-- tools_spec.json
|-- sprint1_entrega.txt
```

## Entrega do Sprint 1

Este repositório contém exclusivamente projeto e documentação. Nenhum código, notebook, chave de API ou protótipo funcional deve ser entregue nesta etapa.

O arquivo `sprint1_entrega.txt` é a cópia fiel do `.txt` enviado na plataforma acadêmica da FIAP, contendo nomes, RMs, turmas, link do repositório e link do fluxograma.
