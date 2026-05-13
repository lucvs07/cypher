# Levantamento Detalhado de Requisitos — Projeto Cypher

Este documento consolida as personas, requisitos funcionais (RF), requisitos não funcionais (RNF) e as restrições do sistema para a **Sprint 1** do Challenge 2026, integrando as definições técnicas de IA com as necessidades de negócio da Metaindústria.

---

## 1. Personas Detalhadas

### Persona A: Marcos — O Operador de Chão de Fábrica
* **Perfil:** Profissional técnico que atua em ambientes de alto risco (metalurgia/manufatura). Focado na execução e no cumprimento de metas de produção.
* **Necessidades:** Um sistema de segurança que atue como um suporte inteligente, alertando-o apenas quando houver risco real, sem gerar interrupções desnecessárias.
* **Dores:** Fadiga ao final do turno que pode levar ao esquecimento involuntário de EPIs; ambientes barulhentos onde alertas puramente sonoros podem passar despercebidos.
* **Interação:** Recebe feedbacks imediatos (visuais e sonoros) no terminal da máquina, permitindo a correção do comportamento antes de acessar a zona de perigo.

### Persona B: Ana — A Gestora de Segurança Industrial
* **Perfil:** Engenheira de Segurança do Trabalho focada em conformidade normativa (NR-6, NR-12) e redução de sinistralidade.
* **Necessidades:** Dados centralizados para identificar gargalos de segurança e provas visuais para auditorias e treinamentos.
* **Dores:** Dificuldade em monitorar grandes áreas simultaneamente; falta de métricas claras sobre a eficácia dos treinamentos de EPI.
* **Interação:** Configura as regras da planta através do Onboarding e utiliza o Dashboard para analisar heatmaps de risco e gerenciar a equipe.

---

## 2. Requisitos Funcionais (RF)

### Módulo de Onboarding e Configuração
* **RF01 – Cadastro Empresarial:** O sistema deve permitir o registro da empresa, incluindo nome, CNPJ e setor de atuação.
* **RF02 – Customização de Interface:** O sistema deve oferecer opções de personalização de cores e temas para a plataforma.
* **RF03 – Gerenciamento de Login:** O sistema deve possuir um login fixo compartilhado para a empresa (acesso operacional) e logins individuais para gestores e funcionários (auditoria).
* **RF04 – Seleção Visual de EPIs:** O sistema deve permitir que o usuário selecione visualmente (via interface gráfica) quais EPIs serão monitorados em cada zona específica.
* **RF05 – Gestão de Certificado de Aprovação (CA):** O sistema deve permitir o cadastro do número do CA e a data de validade de cada EPI, emitindo alertas sobre vencimentos.

### Módulo da Máquina (Operador/Campo)
* **RF06 – Monitoramento em Tempo Real:** O sistema deve exibir o preview das câmeras IP (via stream RTSP) integradas ao ambiente fabril.
* **RF07 – Detecção Automática de Não Conformidade:** O motor de IA deve identificar em tempo real a ausência ou uso incorreto de EPIs obrigatórios.
* **RF08 – Registro de Incidentes (Foto/B.O.):** O sistema deve capturar uma foto e "congelar" o frame da câmera no momento exato em que uma infração for detectada para fins de prova.
* **RF09 – Alertas Locais Multi-sensoriais:** O sistema deve emitir alertas sonoros e visuais (avisos em tela) imediatos no terminal de operação ao detectar um risco.
* **RF10 – Notificação de Alerta Proativo:** O sistema deve disparar uma notificação automática para o dashboard do gestor assim que um risco for detectado no campo.

### Módulo do Gestor (Dashboard)
* **RF11 – Dashboard de Indicadores:** O sistema deve exibir o número total de incidentes, interrupções de linha e cálculos de impacto na produtividade.
* **RF12 – Mapa de Calor (Heatmap):** O sistema deve gerar mapas de calor indicando as zonas da fábrica com maior recorrência de infrações.
* **RF13 – Gestão de Equipe:** O gestor deve ser capaz de cadastrar funcionários e visualizar métricas individuais de conformidade de segurança.
* **RF14 – Galeria de Evidências:** O sistema deve disponibilizar uma galeria com as fotos de todos os incidentes registradas pelo motor de IA.
* **RF15 – Análise Preditiva:** O sistema deve analisar o histórico de ocorrências para identificar padrões de risco por turno, setor ou horário.

---

## 3. Requisitos Não Funcionais (RNF)

* **RNF01 – Latência Crítica:** O tempo de processamento da detecção (inferência) deve ser de até 100ms por frame para garantir a proatividade.
* **RNF02 – Taxa de Processamento:** O sistema deve processar o vídeo a uma taxa estável de 25 a 30 FPS.
* **RNF03 – Precisão da IA:** O modelo YOLOv8 deve manter uma precisão média (mAP) mínima de 80% em condições reais de iluminação.
* **RNF04 – Confiabilidade (Anti-Flicker):** O sistema deve validar a ausência de EPI por um número "N" de frames consecutivos antes de disparar o alerta, evitando falsos positivos.
* **RNF05 – Responsividade Industrial:** A interface do terminal de operação deve ser otimizada para alta legibilidade em ambientes de fábrica.
* **RNF06 – Escalabilidade:** A arquitetura deve suportar o monitoramento de múltiplas câmeras IP simultaneamente sem perda de performance.
* **RNF07 – Disponibilidade:** O sistema deve estar operacional 24/7, cobrindo todos os turnos da indústria.

---

## 4. Restrições do Sistema

* **Restrição 01:** A solução deve operar sobre a infraestrutura de câmeras IP já existente (protocolo RTSP), sem necessidade de novo hardware na Sprint 1.
* **Restrição 02:** Os ambientes monitorados devem possuir iluminação mínima controlada para garantir a acurácia da visão computacional.
* **Restrição 03:** O sistema é focado em ambientes internos (indoor).
* **Restrição 04:** Não contempla análise ergonômica ou integração com travas físicas de máquinas nesta etapa inicial.
