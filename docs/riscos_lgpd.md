# Matriz de Riscos, Ética, Segurança e LGPD — engman-copilot

Recorte: B — Operação e Priorização de Campo
Personas: Operador do CCO (principal), Técnico em Campo (secundária)

| ID | Risco | Impacto | Probabilidade | Mitigação | Rastreabilidade |
|----|-------|---------|---------------|-----------|-----------------|
| R01 | **Alucinação** | O assistente inventa TAGs, números de série, históricos de falhas ou causas de alarme, levando a intervenções incorretas em ativos rodoviários. | Alta | Regras rígidas de recusa; citação obrigatória de fontes; distinção explícita entre FATO e HIPÓTESE; nível de confiança em toda resposta. | System Prompt (blocos REGRAS e FORMATO); Eval Set (categorias factual e dado_inexistente) |
| R02 | **Prompt Injection** | Usuário mal-intencionado tenta subverter as instruções do sistema para extrair o system prompt ou burlar regras de segurança. | Média | Guardrails de entrada; sanitização de inputs; testes rigorosos no Eval Set (categoria jailbreak). | System Prompt (bloco BORDA); Eval Set (categoria jailbreak) |
| R03 | **Risco Operacional** | Solicitação de intervenção em equipamentos energizados ou em vias sem POP pode causar acidentes elétricos ou atropelamento. | Alta | Recusa obrigatória para ações sem POP; alerta de EPIs; referência a NR-10 e NR-35; desligamento seguro prévio. | System Prompt (bloco REGRAS); tools (verificar_seguranca_epi) |
| R04 | **Viés na Priorização** | Priorização de alarmes influenciada por fatores subjetivos, prejudicando ativos críticos da rodovia. | Média | Critérios matemáticos e auditáveis de criticidade; matriz de criticidade documentada; revisão humana do coordenador. | Inventário (matriz de criticidade); tools (classificar_falha_ambiental) |
| R05 | **LGPD (Dados Pessoais)** | Placas de veículos (OCR), imagens de ocupantes ou dados de funcionários entram na base ou no prompt sem consentimento. | Alta | Bloqueio de dados pessoais na base de conhecimento; filtragem de entrada; não armazenar PII no histórico. | System Prompt (bloco REGRAS); .gitignore (*.key, .env) |
| R06 | **Confidencialidade Operacional** | Uso de dados reais da Motiva em modelos de nuvem pode expor informações sensíveis de infraestrutura crítica. | Média | Uso estrito de dados simulados; preferência por modelos locais quando aplicável; não expor estruturas reais de TAGs. | Decisões Técnicas (comparação de modelos); Inventário (dados simulados) |
| R07 | **Excesso de Confiança** | Operador confia cegamente na IA sem validar com procedimento oficial, confundindo hipótese com fato. | Média | Obrigatoriedade de distinguir FATO de HIPÓTESE; níveis de confiança explícitos; frase de recusa padronizada quando inseguro. | System Prompt (blocos FORMATO e REGRAS) |
| R08 | **Estouro de Contexto** | Histórico longo de conversa consome tokens e pode levar à perda de informações críticas de alarmes anteriores. | Baixa/Média | Truncagem inteligente do histórico; resumos periódicos; política de corte de contexto quantificada. | System Prompt (bloco BORDA); Decisões de chunk no Inventário |

## Decisões de Contexto (chunking)

- **Tamanho do chunk:** 512 tokens com sobreposição de 50 tokens, justificado pela janela de contexto do modelo selecionado e pelo tamanho médio de procedimentos de manutenção.
- **Metadados de filtragem por trecho:** TAG do ativo, tipo de alarme, localização (km da rodovia), data do ocorrido, nível de criticidade, fonte do documento.
