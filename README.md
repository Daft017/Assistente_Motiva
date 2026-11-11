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

## Estrutura do Repositório

```
engman-copilot/
|-- README.md
|-- .gitignore
|-- docs/
|   |-- arquitetura.png
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
