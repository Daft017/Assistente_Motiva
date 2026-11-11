# Decisões Técnicas — engman-copilot

Recorte: B — Operação e Priorização de Campo

## 1. Modelos de Linguagem Avaliados

| Critério | GPT-4o (OpenAI) | Claude 3.5 Sonnet (Anthropic) | Llama-3.1 70B (local/hospedado) |
|----------|-----------------|-------------------------------|----------------------------------|
| Custo por token | Alto | Médio | Baixo (infra própria) |
| Latência | Média | Média | Baixa (local) |
| Privacidade de dados | Nuvem terceirizada | Nuvem terceirizada | Local / próprio |
| Suporte a function calling | Excelente | Bom | Limitado |
| Segurança e guardrails | Robustos | Robustos | Dependem da implantação |
| Recomendação | Selecionado para MVP | Alternativa válida | Avaliado para fases futuras |

**Decisão:** GPT-4o para o MVP (Sprint 1 como projeto), por conta do suporte maduro a function calling e estrutura de saídas JSON, facilitando a validação de tools e guardrails.

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

- **Modelo nuvem vs. local:** Modelo nuvem oferece melhor capacidade de raciocínio e function calling, mas exige cuidado com dados confidenciais (mitigado pelo uso de dados simulados no Sprint 1).
- **Vector store gerenciado vs. local:** Pinecone oferece menos trabalho operacional, mas custo recorrente; Chroma/FAISS são gratuitos locais, mas exigem gerenciamento próprio.

## 4. Ferramentas (Tools) Obrigatórias

Conforme contrato em `tools/tools_spec.json`, o assistente poderá acionar:
1. `consultar_alarme_tempo_real`
2. `classificar_falha_ambiental`
3. `gerar_ordem_servico`
4. `verificar_seguranca_epi`

Todas com validação de JSON Schema antes da execução.
