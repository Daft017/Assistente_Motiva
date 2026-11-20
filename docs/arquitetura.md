# Fluxograma da Arquitetura — engman-copilot (Recorte B)

Diagrama em Mermaid (renderizado nativamente pelo GitHub). Cobre os 8 blocos essenciais exigidos pelo Challenge, nomeados com os elementos reais do projeto (TAG, histórico de falhas, POP, criticidade, OS).

```mermaid
flowchart TD
    A["1. Entrada<br/>Operador do CCO / Técnico em Campo<br/>envia alarme ou pergunta (TAG + sintoma)"] --> B

    B{"2. Guardrail de Entrada<br/>Está no escopo (Recorte B)?<br/>É prompt injection / jailbreak?<br/>Contém dado pessoal (LGPD)?"}
    B -- "Fora de escopo / hostil / PII" --> B1["Recusa padronizada<br/>+ redireciona ao responsável"]
    B -- "OK" --> C

    C["3. Montagem do Contexto<br/>System Prompt + Histórico da conversa<br/>+ Trechos recuperados via RAG<br/>(inventário, POPs, histórico FSM)"] --> D

    D["4. Chamada ao LLM<br/>Modelo selecionado<br/>(temperature baixa, max_tokens definido)"] --> E

    E{"5. Decisão de Tool<br/>O modelo tem dado suficiente<br/>ou precisa consultar algo?"}
    E -- "Precisa consultar TAG" --> F1["consultar_historico_tag"]
    E -- "Precisa classificar alarme" --> F2["classificar_falha_ambiental"]
    E -- "Precisa checar segurança" --> F3["verificar_seguranca_epi"]
    E -- "Precisa documentar" --> F4["gerar_ordem_servico"]
    E -- "Tem dado suficiente" --> G

    F1 --> F["6. Execução da Tool<br/>Retorno mockado reinjetado no contexto"]
    F2 --> F
    F3 --> F
    F4 --> F
    F -- "Nova chamada ao LLM com resultado" --> D

    G["7. Guardrail de Saída<br/>Citou a fonte? Marcou FATO vs HIPÓTESE?<br/>Não inventou TAG/métrica/norma?<br/>Incluiu nível de confiança?"]
    G -- "Falhou alguma checagem" --> D
    G -- "Aprovado" --> H

    H["8. Resposta + Histórico<br/>Entrega formatada à persona<br/>(CCO: estruturado/classificado;<br/>Campo: passo a passo curto)<br/>+ grava turno com política de corte de contexto"]
```

## Descrição bloco a bloco

| # | Bloco | O que entra | O que é processado | O que sai |
|---|-------|--------------|---------------------|-----------|
| 1 | Entrada | Texto livre do Operador do CCO ou Técnico em Campo | Identificação de persona e intenção (triagem, consulta, geração de OS) | Mensagem normalizada para o guardrail |
| 2 | Guardrail de entrada | Mensagem normalizada | Checagem contra o escopo do Recorte B, detecção de jailbreak/prompt injection e de dados pessoais (placas, imagens, dados de funcionário) | Aprovação para seguir ou recusa padronizada imediata (sem chamar o LLM) |
| 3 | Montagem do contexto | Mensagem aprovada | Concatenação do `system_prompt.md`, histórico recente da conversa e trechos recuperados por RAG na base de conhecimento (busca híbrida semântica + TAG) | Prompt completo pronto para o modelo |
| 4 | Chamada ao LLM | Prompt completo | Inferência do modelo com parâmetros definidos (temperature baixa para reduzir alucinação) | Resposta preliminar ou decisão de usar tool |
| 5 | Decisão de tool | Resposta preliminar do modelo | Avaliação se há dado suficiente no contexto ou se é necessário acionar uma das 4 tools especificadas | Chamada de tool ou segue direto para o guardrail de saída |
| 6 | Execução da tool | Parâmetros da tool escolhida (ex: `tag`) | Execução mockada (retorno simulado conforme `tools_spec.json`) | Resultado reinjetado no contexto, nova chamada ao LLM |
| 7 | Guardrail de saída | Resposta gerada pelo modelo | Verificação final: cita fonte? distingue FATO de HIPÓTESE? não inventou dado? tem nível de confiança? está dentro do escopo? | Aprovação da resposta ou nova geração (volta ao bloco 4) |
| 8 | Resposta + histórico | Resposta aprovada | Formatação de acordo com a persona (estruturado para CCO, passo a passo para Campo) e gravação do turno | Resposta final ao usuário + histórico atualizado com política de corte de contexto |

## Decisões mais importantes do fluxo

1. **Guardrail de entrada antes do LLM:** recusas por escopo, jailbreak ou dado pessoal são resolvidas sem sequer chamar o modelo — reduz custo, latência e superfície de ataque de prompt injection.
2. **Guardrail de saída pode reenviar ao LLM:** se a resposta gerada falhar em qualquer checagem (ex: não citou fonte, não marcou FATO vs HIPÓTESE), o fluxo não entrega a resposta ao usuário — força nova geração até passar nas checagens, evitando que alucinação chegue ao operador.
