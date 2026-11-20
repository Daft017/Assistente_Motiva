# engman-copilot · M.I.R.A.I

Assistente de Inteligência Artificial Generativa para Engenharia de Manutenção — Motiva Rodovias (Programas PRIME e MIND)

**M.I.R.A.I** (Monitoramento Inteligente com Recuperação Autônoma de Imagem) é o ativo-piloto do engman-copilot: câmeras de CFTV equipadas com sensores embarcados (neblina, proximidade de aves/objetos) e um módulo de Computer Vision que monitora a própria qualidade de captura, prevê degradação e aciona manutenção — corretiva, preventiva ou autônoma (protótipos de troca de película e dupla lente com autolimpeza). O engman-copilot é a camada de IA que recebe os alertas gerados por essas câmeras (e pelos demais ativos ITS da via), confirma com a base de conhecimento, classifica, prioriza e organiza tudo para o Operador do CCO — funcionando como uma espécie de API de gestão de alarmes entre o hardware de campo e a decisão humana.

## Integrantes

- João Pedro Godoy — RM 575698 — Turma CCPB
- Pedro Almeida Pimenta — RM 575312 — Turma CCPB
- Gabriel de Paula Santa Izabel — RM 576143 — Turma CCPB
- Victor Hugo Astorino — RM 575927 — Turma CCPB
- Lucas Jorge Ferreira — RM 575223 — Turma CCPB

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

Um caso específico e recorrente motivou o recorte das câmeras M.I.R.A.I: hoje a manutenção de lente é manual — alguém precisa se deslocar até o ponto para limpar a câmera — e chuva, poeira e teias de aranha sujam a lente logo depois da limpeza. Imagem degradada compromete diretamente a leitura de placas (OCR/LPR) e a captura de evidências em caso de incidente. A proposta do grupo é que a própria câmera monitore a qualidade da sua captura (nível de visibilidade, probabilidade de erro de leitura, saúde da câmera) e emita o alerta de manutenção — o engman-copilot recebe esse alerta, confirma com sensores dedicados (neblina, proximidade) e decide a prioridade e ação, em vez de a IA precisar inferir tudo a partir da imagem.

## Recorte Escolhido: Recorte B — Operação e Priorização de Campo

**Justificativa técnica:** O Recorte B foca no suporte ao operador do CCO (Centro de Controle Operacional) e ao coordenador na triagem de alarmes em tempo real, diferenciando falhas reais de ativos de condições ambientais (chuva, cerração, glare), definindo prioridades e gerando ordens de serviço (OS). Essa escolha está diretamente alinhada com a operação rodoviária da Motiva, onde a rápida distinção entre falha de equipamento e interferência ambiental impacta a segurança dos usuários e a disponibilidade da via.

## Personas

- **Persona principal:** Operador do CCO — recebe alarmes em tempo real. Exige saídas estruturadas e classificadas (real vs. ambiental/indeterminado) com prioridade e ação recomendada.
- **Persona secundária:** Técnico em Campo — em campo, pelo celular, com o equipamento nas mãos. Precisa de instruções curtas, passo a passo, linguagem simples, com forte ênfase em EPI e desligamento seguro.

## Escopo

**Dentro do escopo:**
- Triagem de alarmes em tempo real no CCO
- Classificação de falha real vs. condição ambiental (chuva, cerração, glare)
- Leitura de alertas de câmeras M.I.R.A.I (saúde da câmera, probabilidade de erro de leitura, sensor de proximidade de aves/objetos) e decisão sobre ação recomendada
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

## Ativo-Piloto: Câmeras M.I.R.A.I

A arquitetura de hardware desenhada pelo grupo aposta em processar na borda (edge) o que for barato e repetitivo, e reservar o LLM para a parte que exige julgamento — alinhado ao critério de "Eficiência Computacional" do briefing da Motiva (Tema 2.1).

- **Sensor dedicado de neblina/umidade:** circuito embarcado na própria câmera confirma a condição ambiental antes de qualquer chamada à IA — o modelo não precisa "adivinhar" olhando a imagem, só decide classificação e prioridade com base num dado já confirmado.
- **Sensor de proximidade anti-aves:** detecta pássaros ou objetos próximos à lente e aciona um sistema sonoro de dispersão; o engman-copilot recebe esse evento como mais um tipo de alarme e decide se precisa notificar o operador (normalmente baixa prioridade, salvo recorrência).
- **Computer Vision de qualidade de imagem:** calcula nível de visibilidade, probabilidade de erro de leitura (ex.: placas veiculares) e causa provável (sujeira, gota d'água, embaçamento, obstrução, desfoque), alimentando os KPIs de saúde da câmera.
- **Manutenção preditiva:** combinação dos sinais acima estima o tempo até a próxima manutenção necessária, reduzindo corretivas não planejadas.
- **Protótipos mecânicos de autolimpeza (fora do escopo de IA desta sprint, documentados como contexto do ativo):** (1) troca automática de películas protetoras biodegradáveis via servo motor e gravidade; (2) sistema de dupla lente com câmara de limpeza, permitindo captura contínua enquanto uma das lentes é limpa. Ambos operam em modo assistido (aprovação do operador) ou automático, sempre a partir do alerta gerado pela IA — nunca por sujeira leve, só quando a degradação compromete a leitura de dado crítico.

Esse ativo é tratado pelo engman-copilot como qualquer outro alarme do Recorte B: a diferença é que a "condição ambiental" chega confirmada por sensor em vez de inferida, e a resposta inclui KPIs específicos de câmera (ver `tools/tools_spec.json`).

## Arquitetura da Solução

Fluxo completo com os 8 blocos essenciais (entrada → guardrail de entrada → montagem de contexto com RAG → chamada ao LLM → decisão de tool → execução de tool → guardrail de saída → resposta + histórico), com diagrama Mermaid e descrição bloco a bloco em [`/docs/arquitetura.md`](docs/arquitetura.md).

As três decisões mais importantes do fluxo: (1) o guardrail de entrada recusa pedidos fora de escopo, jailbreak ou com dado pessoal **antes** de chamar o modelo, reduzindo custo e superfície de ataque; (2) condições ambientais das câmeras M.I.R.A.I (neblina, proximidade) são confirmadas por sensor embarcado na borda, não inferidas pela IA a partir da imagem; (3) o guardrail de saída pode forçar uma nova geração se a resposta não citar fonte, não distinguir FATO de HIPÓTESE ou não trouxer nível de confiança — nenhuma alucinação sai sem passar por essa checagem.

## Stack e Justificativa Técnica

Comparação completa de modelos e vector stores em [`/docs/decisoes_tecnicas.md`](docs/decisoes_tecnicas.md).

**Resumo:** Groq (rodando Llama 3.3 70B) selecionado como o caminho **gratuito** do MVP — sem exigir chave paga, com latência muito baixa; Qwen 3 32B avaliado como concorrente direto, com a vantagem de rodar gratuitamente tanto via Groq quanto localmente via Ollama; Claude 3.5 Sonnet e GPT-4o avaliados como alternativas pagas para um cenário de produção; Llama local via Ollama como opção totalmente offline quando a confidencialidade for crítica. Para o vector store do RAG, Chroma foi selecionado para o protótipo (Sprints 3/4) por ser leve e não exigir infraestrutura de nuvem imediata; Pinecone e FAISS avaliados como alternativas para escala/produção local. Trade-off aceito: Groq elimina a barreira de custo, mas tende a perder um pouco de qualidade de raciocínio em casos ambíguos frente aos modelos proprietários — aceitável para o MVP acadêmico.

## Base de Conhecimento

Inventário completo (10 categorias de documento, todos simulados exceto glossário e normas) em [`/data/knowledge_base/inventario.md`](data/knowledge_base/inventario.md): catálogo de 32 ativos (incluindo 2 câmeras M.I.R.A.I), plano de manutenção preventiva, histórico de falhas do FSM (50+ registros), 4 POPs (incluindo resposta a alertas M.I.R.A.I), fichas técnicas, matriz de criticidade, glossário e normas NR-10/NR-35.

**Uso no RAG:** chunks de 512 tokens com sobreposição de 50, metadados por TAG/tipo de alarme/localização/data/criticidade, recuperação por busca híbrida (semântica + palavra-chave por TAG) — justificativa detalhada no próprio inventário.

## System Prompt

Resumo: estruturado em 7 blocos (`PAPEL`, `OBJETIVO`, `ESCOPO`, `REGRAS`, `FORMATO`, `TOM`, `BORDA`), com regras anti-alucinação numeradas, distinção obrigatória entre FATO e HIPÓTESE, frase padrão de recusa e comportamento definido para casos de borda (saudação, pergunta ambígua, dado inexistente, conversa longa, pedido hostil). Versão completa com comentários bloco a bloco em [`/prompts/system_prompt.md`](prompts/system_prompt.md).

## Eval Set

16 casos cobrindo as 8 categorias obrigatórias (factual, instrucional, ambíguo, dado_inexistente, out_of_scope, jailbreak, risco_operacional, memoria_contexto) — 2 deles específicos das câmeras M.I.R.A.I: saúde da câmera e recorrência de alerta de proximidade. Cada caso traz contexto esperado, resposta ideal e critérios de avaliação verificáveis. Arquivo completo em [`/evals/sprint1_eval_set.json`](evals/sprint1_eval_set.json).

## Riscos e Mitigações

9 riscos mapeados (alucinação, prompt injection, risco operacional, viés na priorização, LGPD, confidencialidade operacional, excesso de confiança, estouro de contexto, acionamento autônomo indevido dos protótipos M.I.R.A.I), cada um com impacto, mitigação concreta e rastreabilidade até o bloco do system prompt, a tool ou o caso de eval correspondente. Matriz completa em [`/docs/riscos_lgpd.md`](docs/riscos_lgpd.md).

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
| `classificar_falha_ambiental` | Classifica um alarme como falha real, ambiental/indeterminado ou sem informação; para câmeras M.I.R.A.I, recebe leitura dos sensores embarcados (neblina, proximidade) e métricas de Computer Vision, retornando também os KPIs de saúde da câmera | `tag`, `tipo_alarme`, `condicao_ambiental_informada`, `leitura_sensor_neblina`, `leitura_sensor_proximidade`, `metricas_visao_computacional` |
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
