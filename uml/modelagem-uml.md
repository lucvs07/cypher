# Documentação Técnica - Modelagem UML (Projeto Cypher)

Esta seção detalha a arquitetura comportamental e estrutural do sistema **Cypher**, utilizando diagramas UML para alinhar os requisitos de segurança industrial proativa com a implementação técnica.

---

## 1. Diagrama de Casos de Uso
O diagrama de casos de uso descreve as funcionalidades do sistema e como os diferentes atores interagem com ele.

![Diagrama de Casos de Uso](/uml/casos-de-uso-cypher.png)

### **Atores**
* **Gestor de Segurança**: Ator principal responsável pelo gerenciamento administrativo e estratégico do sistema.
* **Sistema de IA (YOLOv8)**: Ator de sistema que realiza o processamento das imagens e detecções em tempo real.
* **Operador**: Usuário monitorado no chão de fábrica que recebe os feedbacks de segurança.

### **Casos de Uso Principais**
* **Realizar Onboarding**: Processo de configuração inicial obrigatória para o funcionamento do sistema.
    * **Cadastrar Empresa** (Include): Registro dos dados corporativos básicos.
    * **Configurar Zonas de Risco** (Include): Delimitação das áreas que serão monitoradas pelas câmeras.
* **Monitorar Área em Tempo Real**: Fluxo contínuo de análise de vídeo pelo motor de IA.
* **Detectar Ausência de EPI**: Funcionalidade crítica onde o sistema identifica falhas na proteção individual.
    * **Emitir Alerta Proativo** (Include): Disparo imediato de avisos visuais e sonoros.
* **Registrar Incidente (Foto/B.O.)**: Documentação automática da infração que estende o alerta proativo caso a ausência seja confirmada.
* **Visualizar Dashboard de KPIs**: Consultas segmentadas por perfil (Gestor e Operador) para análise de métricas de conformidade.

---

## 2. Diagrama de Atividades
O diagrama de atividades descreve o fluxo lógico do monitoramento, desde a captura da imagem até o registro do incidente.

![Diagrama de Atividades](/uml/diagrama-de-atividade-cypher.png)

### **Raias de Responsabilidade (Lanes)**
* **Pista 1: Hardware (Câmeras IP)**: Responsável pela ingestão do stream RTSP.
* **Pista 2: Terminal do Operador**: Local de exibição dos alertas de campo em tempo real.
* **Pista 3: Motor de IA (YOLOv8 & Lógica)**: Núcleo de processamento, filtragem e tomada de decisão.
* **Pista 4: Interface de Gestão & Banco de Dados**: Persistência de dados e atualização de métricas para o gestor.

### **Fluxo de Processamento**
1.  O sistema captura o frame via stream RTSP.
2.  O frame passa por pré-processamento (OpenCV) e inferência YOLOv8 para detecção de classes.
3.  O sistema identifica o status de EPI da pessoa.
    * **Pessoa com EPI**: O sistema atualiza as métricas de conformidade e retorna ao início.
    * **Pessoa sem EPI**: O sistema valida a ausência através de um filtro de N frames (anti-flickering).
4.  Após confirmação, o sistema dispara alertas locais, envia notificações push ao gestor e registra o incidente com foto e metadados no banco de dados.

---

## 3. Diagrama de Classes
O diagrama de classes define a estrutura estática das entidades do sistema e seus relacionamentos.

![Diagrama de Classes](/uml/diagrama-de-classe.png)

### **Entidades e Atributos**
* **Empresa**: Classe raiz que contém dados como `cnpj` e `setor`, gerenciando múltiplas zonas de risco.
* **Usuario**: Classe base que define `id`, `nome` e `status`.
    * **Operador**: Especialização que inclui `matricula` e `status_seguranca`.
    * **Gestor**: Especialização que inclui `cargo` e `nivel_acesso`.
* **ZonaDeRisco**: Define os `requisitos_EPI` de cada área monitorada.
* **Camera**: Gerencia o `ip_rtsp` e o `status_conexao` do hardware.
* **EPI**: Armazena informações de `numero_ca` e `data_validade_ca`.
* **Alerta / Incidente**: Registra o `timestamp`, a `confianca_IA` e a `foto_evidencia` (Blob).

### **Relacionamentos**
* **Herança**: `Operador` e `Gestor` herdam de `Usuario`.
* **Composição**: `Empresa` possui uma relação de composição com `ZonaDeRisco`.
* **Agregação**: `ZonaDeRisco` agrega `Cameras` e `EPIs`.
* **Associação**:
    * Uma `Camera` gera e localiza múltiplos `Alertas`.
    * Um `Operador` registra e está associado aos `Alertas` de infração.
    * O `Gestor` recebe notificações dos `Alertas` e supervisiona as métricas.
