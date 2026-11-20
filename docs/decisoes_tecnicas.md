# Decisões Técnicas — engman-copilot

Recorte: B — Operação e Priorização de Campo

## 1. Modelos de Linguagem Avaliados

| Critério | Claude 3.5 Sonnet (Anthropic) | GPT-4o (OpenAI) | Groq (Llama 3.3 70B) | Qwen 3 32B (Groq ou Ollama) | Llama 3.1 70B local (Ollama) |
|----------|-------------------------------|------------------|------------------------|-------------------------------|-------------------------------|
| Custo por token | Médio (pago) | Alto (pago) | **Gratuito** (free tier generoso) | **Gratuito** via Groq / Gratuito via Ollama local | Gratuito (infra própria) |
| Latência | Média | Média | **Muito baixa** (inference acelerada em LPU) | Muito baixa via Groq; depende do hardware se local | Baixa, mas depende do hardware local |
| Privacidade de dados | Nuvem terceirizada | Nuvem terceirizada | Nuvem terceirizada | Nuvem terceirizada (Groq) ou local (Ollama) — flexível | Local / próprio |
| Suporte a function calling | Bom | Excelente | Bom (via API compatível com function calling) | Bom (via API Groq) | Limitado |
| Contexto | 200k | 128k | — | 131k | — |
| Segurança e guardrails | Robustos | Robustos | Robustos (herda do modelo open-weight) | Robustos (herda do modelo open-weight) | Dependem da implantação |
| Exige chave paga? | Sim | Sim | **Não** | **Não** (em nenhuma das duas formas de rodar) | Não |
| Recomendação | Alternativa válida | Avaliado | **Selecionado — caminho gratuito do MVP** | Concorrente direto avaliado — mesma dupla disponibilidade gratuita | Alternativa para produção local/offline |

**Decisão:** Groq (rodando Llama 3.3 70B) foi selecionado como o caminho gratuito documentado do MVP, atendendo à exigência do Challenge de que nenhum integrante seja obrigado a pagar por chave de API — e ainda com latência muito baixa, o que ajuda a reduzir o tempo de resposta percebido pelo Operador do CCO. **Qwen 3 32B** foi avaliado como concorrente direto: tem a particularidade de estar disponível gratuitamente tanto hospedado via Groq (mesma infraestrutura de baixa latência) quanto rodando localmente via Ollama — oferecendo flexibilidade entre nuvem e local sem trocar de modelo. Claude 3.5 Sonnet e GPT-4o seguem avaliados como alternativas pagas para um cenário de produção com orçamento, e Llama local via Ollama como opção totalmente offline quando a confidencialidade dos dados for crítica (ver R06 em `riscos_lgpd.md`).

## 2. Vector Stores Avaliados (para RAG futuro)

| Critério | Pinecone | Chroma | FAISS |
|----------|----------|--------|-------|
| Tipo | Nuvem gerenciada | Local / leve | Local (Meta) |
| Escalabilidade | Alta | Média | Alta (local) |
| Facilidade de uso | Alta | Muito alta | Média |
| Custo | Pagamento por uso | Gratuito (local) | Gratuito (local) |
| Persistência | Nuvem | Arquivo local | Arquivo local |
| Recomendação | Avaliado | Selecionado para protótipo | Alternativa para produção local |

**Decisão:** Chroma para o protótipo de RAG (Sprints 3 e 4), por ser leve, de fácil integração com Python e não exigir infraestrutura de nuvem imediata.

## 3. Trade-offs Finais

- **Modelo gratuito (Groq) vs. modelo pago (GPT-4o/Claude):** Groq elimina a barreira de custo e entrega latência muito baixa, mas o suporte a function calling e a qualidade de raciocínio em casos ambíguos tendem a ser ligeiramente inferiores aos modelos proprietários topo de linha — aceitável para o MVP acadêmico, a reavaliar se o projeto evoluir para produção real na Motiva.
- **Modelo nuvem vs. local:** Modelo em nuvem (Groq/GPT-4o/Claude) oferece melhor capacidade de raciocínio e manutenção simplificada, mas exige cuidado com dados confidenciais (mitigado pelo uso de dados simulados no Sprint 1); Llama local via Ollama é a opção quando a confidencialidade for inegociável.
- **Vector store gerenciado vs. local:** Pinecone oferece menos trabalho operacional, mas custo recorrente; Chroma/FAISS são gratuitos locais, mas exigem gerenciamento próprio.

## 4. Ferramentas (Tools) Obrigatórias

Conforme contrato em `tools/tools_spec.json`, o assistente poderá acionar:
1. `consultar_historico_tag`
2. `classificar_falha_ambiental`
3. `gerar_ordem_servico`
4. `verificar_seguranca_epi`

Todas com validação de JSON Schema antes da execução.
