# Cypher — Industrial Vision AI

## 1. Nome do Projeto e Integrantes
**Projeto:** Cypher — Plataforma de Segurança Industrial Proativa.
**Turma:** 3º Ano - Engenharia da Computação (Aclimação).

**Integrantes:**
* **Felipe Wapf Fettback** – RM 557217
* **Lucas Rodrigues Grecco** – RM 558261
* **Monique Ferreira Dos Anjos** – RM 558262
* **Rafael Augusto Oliveira Silva** – RM 555154
* **Ronaldo Veloso Filho** – RM 556445
* **Tiago Brito Nário** – RM 558248

---

## 2. Problema Abordado
O cenário atual da segurança industrial enfrenta um desafio crítico: o modelo de segurança punitivo e reativo está estruturalmente defasado. As inspeções manuais são periódicas e inconsistentes, criando uma falsa sensação de controle onde o risco só é percebido após o incidente. No Brasil, ocorrem cerca de 700 mil acidentes de trabalho por ano, gerando custos que superam R$ 100 bilhões anuais ao sistema previdenciário e às empresas. Estudos indicam que entre 40% e 60% das lesões graves poderiam ser evitadas apenas com o uso correto de Equipamentos de Proteção Individual (EPIs).

---

## 3. Proposta de Solução
O **Cypher** é uma plataforma modular de segurança industrial proativa que utiliza Visão Computacional para proteger trabalhadores antes que o acidente aconteça. 

A solução fundamenta-se em dois pilares:
1. **Motor de Visão Computacional:** Identifica em tempo real a presença ou ausência de EPIs obrigatórios (capacete, colete, luvas e óculos) e rastreia pessoas em zonas de risco monitoradas.
2. **Plataforma Web Cypher:** Dashboard inteligente para gestores com histórico de infrações, heatmaps de risco e KPIs de conformidade, além de um sistema de alertas imediatos (visuais e sonoros) para o operador no campo.

O diferencial do projeto é o foco no **onboarding modular**, permitindo que cada empresa configure suas próprias zonas, câmeras e regras de EPI obrigatório de forma flexível.

---

## 4. Tecnologias Selecionadas e Justificativa Técnica

Para atender às demandas de tempo real, confiabilidade e escalabilidade industrial, selecionamos o seguinte stack tecnológico:

| Tecnologia | Função | Justificativa Técnica |
| :--- | :--- | :--- |
| **Python 3.11** | Linguagem Principal | Base robusta para integração de bibliotecas de IA e processamento de dados. |
| **YOLOv8 (Ultralytics)** | Visão Computacional | Arquitetura de detecção de objetos de última geração que atinge mais de 50 FPS em hardware convencional, garantindo monitoramento em tempo real. |
| **OpenCV** | Processamento de Imagem | Essencial para a captura e decodificação de streams de vídeo RTSP vindos de câmeras IP industriais. |
| **Java (Spring Boot)** | Backend de Gestão | Utilizado para a estrutura empresarial do sistema, garantindo segurança, persistência de dados e escalabilidade para o dashboard. |
| **React + Next.js** | Frontend | Proporciona uma interface web segmentada e altamente responsiva para operadores e gestores. |
| **SQL (PostgreSQL/Oracle)** | Banco de Dados | Garante a integridade dos logs de eventos, metadados de incidentes e históricos de conformidade para auditoria industrial. |

---

## 5. Documentação UML e Requisitos
Os artefatos técnicos completos da **Sprint 1** (Diagramas de Caso de Uso, Atividades e Classes) e o levantamento detalhado de requisitos podem ser encontrados na pasta:
* [Requisitos Detalhados](/requisitos/doc-requisitos.md)
* [Modelagem UML](/uml/modelagem-uml.md)
* 
## 6. Protótipo Navegável (Sprint 2)
 
O protótipo de alta fidelidade do Cypher foi desenvolvido no Figma cobrindo **12 telas** e **65+ zonas de navegação interativas**, contemplando todos os fluxos exigidos pelo briefing da Sprint 2.
 
### 🔗 Links
 
* **Protótipo Figma (modo apresentação):** [Abrir protótipo navegável](https://www.figma.com/design/kyeXTO2Uw0lkm8DPK2a22v/Interface?node-id=0-1&p=f&t=y1y1U2H6eANluOBD-0)
* **Vídeo walkthrough (até 3 min):** [Assistir no YouTube](https://youtu.be/T8X5FBOi1XI)
* **Documentação de Design completa:** [`/pro/sprint-2-design.md`](./docs/sprint-2-design.md) — contém o mapa de telas, decisões de UX e mapeamento com casos de uso da Sprint 1.
### Instruções de Navegação
 
1. Acesse o link do protótipo Figma acima.
2. No canto superior direito, clique no botão **▶ Present** (ou pressione `Shift + Espaço`) para entrar no modo apresentação navegável.
3. Use o **mouse/trackpad** para clicar nas áreas interativas. Áreas clicáveis estão destacadas brevemente ao pressionar `R` no Figma.
4. Para retornar à tela inicial a qualquer momento, pressione `Home` ou use o item **Login** no menu lateral.
### Fluxos Cobertos pelo Protótipo
 
| Fluxo Exigido (Briefing) | Telas Envolvidas |
| :--- | :--- |
| **Cadastro e consulta de EPI por colaborador** | `05 Gestão EPIs` → `11 Cadastro EPI` → `06 Colaboradores` → `10 Perfil do Colaborador` |
| **Emissão e visualização de alerta de risco** | `03 Ao Vivo` → `09 Modal Crítico` → `04 Alertas` |
| **Geração de relatório de conformidade por setor** | `02 Dashboard` → `07 Relatórios` |
| **Onboarding e configuração inicial** | `08 Onboarding` → `01 Login` → `02 Dashboard` |
 
### Mapa de Telas (Resumo)
 
```
08 Onboarding ──► 01 Login ──► 02 Dashboard ──┬─► 03 Ao Vivo ──► 09 Modal Crítico
                                              ├─► 04 Alertas ──► 10 Perfil
                                              ├─► 05 Gestão EPIs ──► 11 Cadastro EPI
                                              ├─► 06 Colaboradores ──► 12 Cadastro Colab
                                              └─► 07 Relatórios
```
 
### Principais Decisões de UX
 
* **Dark mode como padrão** — reduz fadiga visual em ambientes de sala de controle 24/7 e segue padrão SCADA industrial.
* **Filosofia "Prever, não punir"** — linguagem educativa e contextualizada nos alertas, alinhada ao princípio norteador do produto.
* **Hierarquia visual de severidade em 5 níveis** — Crítico > Alto > Médio > Aviso > Resolvido, com redundância de cor + ícone para acessibilidade.
* **Modal bloqueante para alertas críticos** — garante tempo de resposta < 1s em situações de risco iminente.
* **Sidebar consistente com estado ativo** — padrão familiar de softwares industriais (Siemens TIA Portal, Rockwell FactoryTalk).
> Justificativas completas e detalhadas estão na [documentação de design](./docs/sprint-2-design.md).
 
---
