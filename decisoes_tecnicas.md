# Decisões Técnicas

Comparação de modelos e bibliotecas avaliadas para o engman-copilot.

## Modelos de linguagem avaliados

| Critério | Modelo A (ex: GPT-4) | Modelo B (ex: Claude 3) | Modelo C (ex: Llama-3 local) |
|----------|----------------------|-------------------------|------------------------------|
| Custo por token | Alto | Médio | Baixo (infra própria) |
| Latência | Média | Média | Baixa |
| Privacidade de dados | Nuvem terceirizada | Nuvem terceirizada | Local / próprio |
| Suporte a function calling | Sim | Sim | Limitado |
| Recomendação | Avaliado | Avaliado | Não recomendado para produção |

## Bibliotecas avaliadas

| Biblioteca | Uso pretendido | Prós | Contras | Decisão |
|------------|----------------|------|---------|---------|
| LangChain | Orquestração de chains e agents | Ecossistema maduro, integrações prontas | Curva de aprendizado, abstrações pesadas | Avaliado |
| LlamaIndex | RAG sobre knowledge base | Indexação e recuperação otimizadas | Foco maior em indexação que em agent | Avaliado |
| OpenAI Python SDK | Chamada direta à API | Simples, leve, controle total | Requer implementar orquestração manual | Selecionada |
| Pydantic | Validação de schemas e tools | Tipagem forte, validação automática | Dependência adicional | Selecionada |

## Decisão final

- **Modelo:** Modelo A (via API) para o MVP, com opção de auto-hospedagem futura.
- **Orquestração:** Implementação customizada com OpenAI SDK + Pydantic, sem depender de frameworks pesados de agent.
- **Validação de tools:** JSON Schema validado com Pydantic antes da execução.
