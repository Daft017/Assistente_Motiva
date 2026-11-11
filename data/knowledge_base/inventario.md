# Inventário da Base de Conhecimento — engman-copilot

Recorte: B — Operação e Priorização de Campo  
Personas: Operador do CCO (principal), Técnico em Campo (secundária)

Todos os documentos abaixo são **simulados** para fins acadêmicos do Sprint 1. Não utilizar dados reais da Motiva Rodovias.

---

## 1. Catálogo de Ativos (30 linhas simuladas)

| ID | TAG | Tipo de Ativo | Localização (km) | Fabricante | Modelo | Data Instalação | Criticidade | Status |
|----|-----|---------------|------------------|------------|--------|-----------------|-------------|--------|
| 01 | CAM-001 | Câmera de monitoramento | 2,5 | Hikvision | DS-2CD2143G0-I | 2023-03-10 | Alta | Ativo |
| 02 | CAM-042 | Câmera de monitoramento | 12,5 | Hikvision | DS-2CD2143G0-I | 2023-03-15 | Alta | Ativo |
| 03 | CAM-078 | Câmera PTZ | 25,8 | Dahua | SD59230U-HNI | 2023-04-02 | Média | Ativo |
| 04 | SEN-015 | Sensor de tráfego | 5,2 | Siemens | SRS500 | 2023-02-20 | Alta | Ativo |
| 05 | SEN-110 | Sensor de tráfego | 15,2 | Siemens | SRS500 | 2023-02-22 | Alta | Ativo |
| 06 | SEN-203 | Sensor de tráfego | 30,1 | Siemens | SRS500 | 2023-04-10 | Média | Ativo |
| 07 | PMV-033 | Painel de Mensagem Variável | 8,4 | Luminator | V8100 | 2023-01-15 | Alta | Ativo |
| 08 | PMV-067 | Painel de Mensagem Variável | 18,9 | Luminator | V8100 | 2023-01-18 | Alta | Ativo |
| 09 | PMV-124 | Painel de Mensagem Variável | 33,5 | Luminator | V8100 | 2023-05-01 | Média | Ativo |
| 10 | GAB-008 | Gabinete de controle | 3,1 | Schneider | Prisma Plus | 2023-02-01 | Alta | Ativo |
| 11 | GAB-055 | Gabinete de controle | 14,7 | Schneider | Prisma Plus | 2023-02-05 | Alta | Ativo |
| 12 | GAB-099 | Gabinete de controle | 28,3 | Schneider | Prisma Plus | 2023-03-20 | Média | Ativo |
| 13 | ILU-012 | Luminária LED | 1,8 | Philips | RoadStar | 2023-03-05 | Baixa | Ativo |
| 14 | ILU-045 | Luminária LED | 6,3 | Philips | RoadStar | 2023-03-08 | Baixa | Ativo |
| 15 | ILU-089 | Luminária LED | 11,1 | Philips | RoadStar | 2023-03-12 | Baixa | Ativo |
| 16 | DET-021 | Detector de incidente | 7,6 | FLIR | TrafiCam | 2023-04-05 | Alta | Ativo |
| 17 | DET-058 | Detector de incidente | 19,2 | FLIR | TrafiCam | 2023-04-08 | Alta | Ativo |
| 18 | DET-101 | Detector de incidente | 35,0 | FLIR | TrafiCam | 2023-05-15 | Média | Ativo |
| 19 | FIB-004 | Cabo de fibra óptica | 0-5 | Corning | SMF-28e+ | 2023-01-10 | Alta | Ativo |
| 20 | FIB-027 | Cabo de fibra óptica | 5-15 | Corning | SMF-28e+ | 2023-01-15 | Alta | Ativo |
| 21 | FIB-053 | Cabo de fibra óptica | 15-30 | Corning | SMF-28e+ | 2023-01-20 | Média | Ativo |
| 22 | ENR-009 | Nobreak | 3,1 | APC | Smart-UPS 1500 | 2023-02-01 | Alta | Ativo |
| 23 | ENR-041 | Nobreak | 14,7 | APC | Smart-UPS 1500 | 2023-02-05 | Alta | Ativo |
| 24 | ENR-082 | Nobreak | 28,3 | APC | Smart-UPS 1500 | 2023-03-20 | Média | Ativo |
| 25 | CBM-002 | Sensor vibração/temperatura | 12,5 | Bosch | IoT Sensor | 2024-01-10 | Média | Ativo |
| 26 | CBM-017 | Sensor vibração/temperatura | 25,8 | Bosch | IoT Sensor | 2024-01-15 | Média | Ativo |
| 27 | CCTV-006 | Câmera CCTV analógica | 4,3 | Axis | M1065-LW | 2022-11-01 | Baixa | Inativo |
| 28 | CCTV-031 | Câmera CCTV analógica | 9,7 | Axis | M1065-LW | 2022-11-05 | Baixa | Inativo |
| 29 | SRL-001 | Sirene sonora | 15,2 | Federal Signal | VS4-12 | 2023-03-01 | Média | Ativo |
| 30 | SRL-008 | Sirene sonora | 22,4 | Federal Signal | VS4-12 | 2023-03-05 | Média | Ativo |

---

## 2. Plano de Manutenção Preventiva (1 plano)

**Plano PMP-2026 — Inspeção Preventiva de Ativos Eletroeletrônicos Rodoviários**

| Atividade | Frequência | Responsável | Ativos Cobertos |
|-----------|------------|-------------|-----------------|
| Limpeza de lentes e sensores | Mensal | Técnico em Campo | CAM-001, CAM-042, CAM-078 |
| Verificação de conexões de fibra | Semestral | Engenheiro de Manutenção | FIB-004, FIB-027, FIB-053 |
| Teste de nobreak (bateria) | Trimestral | Técnico em Campo | ENR-009, ENR-041, ENR-082 |
| Calibração de sensores de tráfego | Semestral | Engenheiro de Manutenção | SEN-015, SEN-110, SEN-203 |
| Inspeção visual de gabinetes | Mensal | Técnico em Campo | GAB-008, GAB-055, GAB-099 |
| Atualização de firmware PMV | Anual | Engenheiro de Manutenção | PMV-033, PMV-067, PMV-124 |

---

## 3. Histórico de Falhas do FSM (50+ registros simulados)

Resumo dos registros simulados (amostra de 10 dos 50+):

| Data | TAG | Tipo de Falha | Localização | Ação Tomada | Status |
|------|-----|---------------|-------------|-------------|--------|
| 2026-01-10 | CAM-042 | Perda de vídeo intermitente | km 12,5 | Limpeza de lente e verificação de cabo | Resolvido |
| 2026-01-15 | SEN-110 | Leitura inconsistente de velocidade | km 15,2 | Recalibração do sensor | Resolvido |
| 2026-01-20 | PMV-067 | Pixel apagado no display | km 18,9 | Substituição de módulo LED | Resolvido |
| 2026-02-05 | GAB-055 | Superaquecimento do gabinete | km 14,7 | Limpeza de filtros de ventilação | Resolvido |
| 2026-02-12 | FIB-027 | Perda de sinal na fibra | km 5-15 | Reemenda de fibra óptica | Resolvido |
| 2026-03-01 | ILU-045 | Lâmpada queimada | km 6,3 | Substituição de luminária | Resolvido |
| 2026-03-10 | DET-058 | Falha de detecção de incidente | km 19,2 | Ajuste de sensibilidade | Resolvido |
| 2026-03-18 | ENR-041 | Bateria do nobreak fraco | km 14,7 | Troca de bateria | Resolvido |
| 2026-04-02 | CAM-078 | Perda de controle PTZ | km 25,8 | Reconfiguração de IP | Resolvido |
| 2026-04-15 | SEN-203 | Contagem duplicada de veículos | km 30,1 | Atualização de firmware | Resolvido |

*Os 40+ registros restantes seguem o mesmo padrão e estão armazenados no arquivo simulado `fsm_historico_2026.json` (não entregue neste sprint).*

---

## 4. POPs - Procedimentos Operacionais (3)

### POP-01 — Triagem de Alarmes no CCO
Objetivo: Padronizar a recepção e classificação de alarmes recebidos pelo operador do CCO.
Passos:
1. Receber alarme no sistema de monitoramento.
2. Identificar TAG, localização (km) e tipo de alarme.
3. Verificar condições ambientais locais (chuva, cerração, glare).
4. Consultar base de conhecimento para histórico do TAG.
5. Classificar como: falha real, ambiental/indeterminado ou sem informação.
6. Definir prioridade (Alta/Média/Baixa) conforme matriz de criticidade.
7. Gerar OS se necessário e encaminhar ao técnico de campo.
8. Registrar turno no sistema.

### POP-02 — Desligamento Seguro de Equipamentos Energizados
Objetivo: Garantir segurança do técnico em campo durante intervenções elétricas.
Passos:
1. Isolar a área e sinalizar com cones/placas.
2. Desligar disjuntor principal do gabinete.
3. Verificar ausência de tensão com multímetro (apenas pessoa qualificada NR-10).
4. Bloquear/travar o disjuntor (Lockout/Tagout).
5. Usar EPI completo: capacete, luva isolante, bota, óculos de proteção.
6. Executar a manutenção.
7. Retirar bloqueios, religar e testar funcionamento.

### POP-03 — Geração de Ordem de Serviço (OS)
Objetivo: Documentar formalmente intervenções de manutenção.
Campos obrigatórios:
- Número da OS
- TAG do ativo
- Localização (km)
- Tipo de intervenção (corretiva/preventiva/inspeção/CBM)
- Descrição do problema
- Ações realizadas
- EPIs utilizados
- Responsável técnico
- Data e hora de abertura e fechamento
- Assinatura do responsável

---

## 5. Fichas Técnicas dos Equipamentos (seleção)

- **Câmera Hikvision DS-2CD2143G0-I:** Resolução 4MP, visão noturna, PoE, suscetível a acúmulo de umidade na lente.
- **Sensor Siemens SRS500:** Radar de tráfego, medição de velocidade e contagem, sensível a condições climáticas adversas.
- **Painel Luminator V8100:** LED matriz, comunicação via fibra óptica, pixels individuais substituíveis.
- **Gabinete Schneider Prisma Plus:** IP65, ventilação forçada, disjuntores termomagnéticos.
- **Nobreak APC Smart-UPS 1500:** Autonomia média 15 min, bateria selada, teste automático semanal.

---

## 6. Matriz de Criticidade

| Criticidade | Critério | Tempo Máximo de Resposta | Exemplo de Ativo |
|-------------|----------|--------------------------|------------------|
| Alta | Afeta segurança do usuário ou disponibilidade da via principal | 30 min | Câmeras, sensores de tráfego, PMV principais |
| Média | Afeta monitoramento secundário ou via alternativa | 2 horas | Sensores CBM, sirenes, luminárias secundárias |
| Baixa | Impacto operacional mínimo | 24 horas | Luminárias isoladas, CCTV analógica inativa |

---

## 7. Glossário de Siglas

| Sigla | Significado |
|-------|-------------|
| CCO | Centro de Controle Operacional |
| OS | Ordem de Serviço |
| POP | Procedimento Operacional Padrão |
| FSM | Sistema de Gestão de Serviços de Manutenção |
| TAG | Identificador único do ativo |
| PMV | Painel de Mensagem Variável |
| CBM | Condition-Based Maintenance |
| EPI | Equipamento de Proteção Individual |
| NR-10 | Norma Regulamentadora de Segurança em Instalações e Serviços em Eletricidade |
| NR-35 | Norma Regulamentadora de Trabalho em Altura |
| RAG | Retrieval-Augmented Generation |
| LLM | Large Language Model |

---

## 8. Normas de Segurança Resumidas (NR-10 e NR-35)

**NR-10 (Eletricidade):**
- Apenas profissionais qualificados podem trabalhar em instalações elétricas.
- Obrigatório uso de EPI adequado e procedimento de desligamento seguro (LOTO).
- Distâncias de segurança mínima devem ser respeitadas.

**NR-35 (Trabalho em Altura):**
- Obrigatório uso de cinto de segurança para trabalhos acima de 2 m.
- Treinamento específico necessário.
- Proteção contra quedas de objetos obrigatória.

---

## 9. Documentos do Briefing da Motiva

- Briefing PRIME — Programa de Inovação e Manutenção Eletroeletrônica (simulado)
- Briefing MIND — Monitoramento Inteligente de Rodovias (simulado)
- Plano de Comunicação de Incidentes (simulado)
- Matriz de Responsabilidades CCO x Campo (simulado)

---

## 10. Boletins de Ocorrência Simulados (10+ registros)

| ID BO | Data | TAG | Descrição | Condição Ambiental | Classificação |
|-------|------|-----|-----------|-------------------|---------------|
| BO-2026-088 | 2026-03-10 | CAM-042 | Perda de vídeo intermitente durante chuva forte | Chuva | Falha real + ambiental |
| BO-2026-089 | 2026-03-12 | SEN-110 | Leitura de velocidade zerada por 15 min | Cerração | Ambiental/indeterminado |
| BO-2026-090 | 2026-03-15 | PMV-067 | Mensagem não exibe corretamente | Sem chuva | Falha real |
| BO-2026-091 | 2026-03-18 | GAB-055 | Alarme de temperatura elevada no gabinete | Sem chuva | Falha real |
| BO-2026-092 | 2026-03-20 | FIB-027 | Perda de sinal intermitente | Chuva contínua | Ambiental/indeterminado |
| BO-2026-093 | 2026-03-25 | ILU-045 | Lâmpada piscando antes de queimar | Sem chuva | Falha real |
| BO-2026-094 | 2026-04-01 | DET-058 | Falso alarme de incidente | Chuva + glare | Ambiental/indeterminado |
| BO-2026-095 | 2026-04-05 | ENR-041 | Nobreak em modo bateria sem queda de energia | Sem chuva | Falha real |
| BO-2026-096 | 2026-04-10 | CAM-078 | Perda de controle PTZ remoto | Sem chuva | Falha real |
| BO-2026-097 | 2026-04-15 | SEN-203 | Contagem duplicada em horário de pico | Cerração | Ambiental/indeterminado |

---

## 11. Decisões de Chunking e Filtragem (RAG)

- **Tamanho do chunk:** 512 tokens com sobreposição de 50 tokens.
  - *Justificativa:* Equilibra o tamanho médio de POPs e boletins de ocorrência com a janela de contexto do modelo, evitando corte de sentenças críticas em procedimentos de segurança.
- **Metadados de filtragem por trecho:** TAG do ativo, tipo de alarme, localização (km), data do ocorrido, nível de criticidade, fonte do documento.
- **Estratégia de recuperação:** Busca híbrida (semântica + palavra-chave por TAG) para garantir que o operador do CCO encontre rapidamente o histórico do ativo mencionado.
