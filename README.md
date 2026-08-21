<h1 align="center" style="color: #17D1A6">Field<span style="color: #000000b2">Ops</span></h1>
<h2 align="center" style="color: #000000b2">Plataforma de Inspeção em Campo</h2>
<p align="center">
  <strong><span style="color: #000000b2">Planeje.</span> <span style="color: #17D1A6">Execute.</span> <span style="color: #000000b2">Registre.</span> <span style="color: #17D1A6">Revise<span>.</strong><br>
</p>



![Next JS](https://img.shields.io/badge/Next-black?style=for-the-badge&logo=next.js&logoColor=white) ![Expo](https://img.shields.io/badge/expo-1C1E24?style=for-the-badge&logo=expo&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi) ![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white) ![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white) 

<h2 style="color: #17D1A6">Visão <span style="color: #000000b2">Geral</span></h2>

O **FieldOps** é uma plataforma digital desenvolvida para organizações que realizam **inspeções técnicas em campo**, conectando a operação realizada pelos técnicos à gestão administrativa em um único fluxo.
A plataforma substitui processos fragmentados — como **formulários impressos, planilhas, mensagens e registros informais** — por uma solução digital integrada, padronizada e rastreável.

<h3 style="color: #17D1A6"><span style="color: #000000b2">Do</span> Campo <span style="color: #000000b2"> à <span style="color: #17D1A6">Gestão</span></h2>

|  Operação em campo 📱        |  Gestão administrativa 🖥️     |
| :--------------------------- | :----------------------------- |
| Receber inspeções atribuídas | Configurar modelos de inspeção |
| Identificar equipamentos     | Agendar atividades             |
| Executar checklists          | Atribuir técnicos              |
| Registrar evidências         | Acompanhar execuções           |
| Registrar não conformidades  | Analisar resultados            |
| Trabalhar offline            | Revisar e aprovar inspeções    |


<h3 style="color: #17D1A6"><span style="color: #000000b2">Um</span> único fluxo</h2>

O FieldOps permite que o técnico execute suas atividades mesmo em locais **sem conexão com a internet**, registrando checklists, evidências e informações da inspeção para posterior sincronização.
Ao mesmo tempo, administradores e supervisores acompanham o processo, desde a configuração e planejamento até a revisão dos resultados.

> **FieldOps conecta a operação em campo à gestão, preservando evidências, histórico, localização e regras de negócio em um único fluxo.**

<h3  align="center" style="color: #17D1A6">Resultado</h2>

**Uma operação de inspeção mais padronizada, rastreável e conectada**.


 
<h2 style="color: #17D1A6">Principais <span style="color: #000000b2">recursos</span></h2>

- [ ] Segurança
- [ ] Mobile
- [ ] Checklists 
- [ ] Evidências
- [ ] Offline
- [ ] Sincronização 




<h2  style="color: #17D1A6">Arquitetura</h2>

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: '#17d1a69a'
    primaryTextColor: '#096b54'
    primaryBorderColor: '#0000008a'
    lineColor: '#000000a9'
---
flowchart LR
    TECH[Técnico]
    WEB[Administração]

    MOBILE[Mobile App]
    API[REST API]
    DB[(PostgreSQL)]
    LOCAL[(SQLite)]
    STORAGE[(Object Storage)]

    TECH --> MOBILE
    MOBILE <--> LOCAL
    MOBILE <--> API
    WEB <--> API
    API --> DB
    API --> STORAGE
```


<h2 style="color: #17D1A6">Fluxo <span style="color: #000000b2">principal</span></h2>

O fluxo de uma inspeção no FieldOps é baseado em um ciclo completo:

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: '#17d1a69a'
    primaryTextColor: '#096b54'
    primaryBorderColor: '#0000008a'
    lineColor: '#000000a9'
---
flowchart TD
    A[Configuração] --> B[Modelo de Inspeção]
    B --> C[Agendamento]
    C --> D[Atribuição do Técnico]
    D --> E[Execução em Campo]
    E --> F{Conectividade}

    F -->|Online| G[API]
    F -->|Offline| H[SQLite + Outbox]

    H --> I[Sincronização]
    I --> G

    G --> J[Revisão do Supervisor]
    J --> K{Resultado}

    K -->|Aprovada| L[Finalizada]
    K -->|Correção| M[Retorno ao Técnico]
```




<h2  align="center" style="color: #17D1A6">Offline-first <span style="color: #000000b2">architecture</span></h2>

Um dos principais diferenciais do FieldOps é a capacidade de executar inspeções **mesmo sem conexão com a internet**.
Durante uma inspeção, o técnico poderá continuar trabalhando normalmente.
Os dados serão armazenados localmente e posteriormente enviados para a API quando a conexão estiver disponível.

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: '#17d1a69a'
    primaryTextColor: '#096b54'
    primaryBorderColor: '#0000008a'
    lineColor: '#000000a9'
---
flowchart TD
    TECH[Técnico]
    APP[Aplicativo]
    SQLITE[(SQLite<br/>Dados locais<br/>Outbox)]
    SYNC[SINCRONIZAÇÃO]
    API[API REST]
    DB[(PostgreSQL)]

    TECH --> APP
    APP -->|Sem conexão| SQLITE
    SQLITE -->|Conexão volta| SYNC
    SYNC --> API
    API --> DB
```




<h2 style="color: #17D1A6">Segurança <span style="color: #000000b2">/ rastreabilidade</span></h2>

No FieldOps, segurança e rastreabilidade fazem parte do processo de inspeção desde a execução em campo até a revisão dos resultados.
Cada operação deve estar associada ao usuário responsável, às permissões correspondentes, às evidências registradas e ao histórico da atividade, garantindo maior controle sobre os dados e sobre o ciclo de vida de uma inspeção.


<h3 style="color: #17D1A6">Camadas <span style="color: #000000b2">de controle</span></h3>

| Controle | Objetivo |
|---|---|
| **Autenticação** | Identificar e validar os usuários da plataforma |
| **Perfis e permissões** | Controlar o acesso conforme o papel do usuário |
| **Autorização** | Garantir que cada operação respeite as permissões definidas |
| **Versionamento** | Preservar a versão do modelo utilizada na inspeção |
| **Evidências** | Associar fotos e arquivos às informações registradas |
| **Localização** | Registrar a localização relacionada à execução |
| **Histórico** | Preservar alterações e eventos relevantes |
| **Auditoria** | Permitir o rastreamento das operações realizadas |
| **Sincronização** | Registrar e controlar a transferência dos dados entre dispositivo e servidor |




<h2 align="center"  style="color: #000000b2">Escopo do<span style="color: #17D1A6"> MVP</span></h2>

O MVP será capaz de demonstrar o fluxo completo de uma inspeção:

### Administrador

* [ ] Cadastrar dados básicos
* [ ] Gerenciar usuários
* [ ] Cadastrar clientes
* [ ] Cadastrar locais
* [ ] Cadastrar equipamentos

ADMIN
█░ 0%


### Supervisor

* [ ] Criar modelo de inspeção
* [ ] Versionar modelo
* [ ] Agendar inspeção
* [ ] Atribuir técnico
* [ ] Acompanhar execução
* [ ] Revisar resultado
* [ ] Aprovar inspeção
* [ ] Reprovar ou solicitar correção

SUPERVISOR
█░ 0%

### Técnico

* [ ] Autenticar no aplicativo
* [ ] Consultar inspeções atribuídas
* [ ] Identificar equipamento via QR Code
* [ ] Executar checklist
* [ ] Registrar respostas
* [ ] Registrar observações
* [ ] Registrar não conformidades
* [ ] Capturar fotografias
* [ ] Capturar localização
* [ ] Trabalhar offline
* [ ] Sincronizar dados

TÉCNICO
█░ 0%




<h2 align="center" style="color: #17D1A6">Road<span style="color: #000000b2">map</span></h2>

```mermaid
flowchart LR
    A["🏗️<br/>FASE 1<br/><b>Fundação</b><br/><br/>Arquitetura<br/>Projetos<br/>Banco de dados<br/>API REST<br/>Autenticação"]
    
    B["🗂️<br/>FASE 2<br/><b>Gestão</b><br/><br/>Usuários<br/>Clientes<br/>Locais<br/>Equipamentos<br/>Modelos"]
    
    C["📋<br/>FASE 3<br/><b>Inspeção</b><br/><br/>Agendamento<br/>Atribuição<br/>Checklist<br/>QR Code<br/>Evidências"]
    
    D["📴<br/>FASE 4<br/><b>Offline</b><br/><br/>Banco local<br/>Outbox<br/>Sincronização<br/>Operações pendentes"]
    
    E["🔎<br/>FASE 5<br/><b>Revisão</b><br/><br/>Acompanhamento<br/>Revisão<br/>Aprovação<br/>Correções<br/>Histórico"]

    A --> B --> C --> D --> E

    style A fill:#17D1A6,stroke:#000000b2,stroke-width:2px
    style C fill:#17D1A6,stroke:#000000b2,stroke-width:2px
    style D fill:#17D1A6,stroke:#000000b2,stroke-width:2px
    style B fill:#17D1A6,stroke:#000000b2,stroke-width:2px
    style E fill:#17D1A6,stroke:#000000b2,stroke-width:2px
```




## 📄 Documentação

A documentação técnica do projeto está disponível no diretório:

[/docs](link)

Documentações específicas sobre arquitetura, API, banco de dados, sincronização e regras de negócio serão adicionadas conforme a evolução do projeto.



<h2 style="color: #17D1A6">Equipe</h2>
 

<p align="center" style="color: #17D1A6">Kelvim<span style="color: #000000b2"> Lucas</span></p>
<p align="right" style="color: #17D1A6">Ryan<span style="color: #000000b2"> Augusto</span></p>
<p style="color: #17D1A6">Gustavo <span style="color: #000000b2"> Senna</span></p>
<p align="center" style="color: #17D1A6">Carlos<span style="color: #000000b2"> Eduardo</span></p>
<p align="right" style="color: #17D1A6">Gustavo<span style="color: #000000b2"> Silveira</span></p>


<footer align="center">
  <strong style="color: #17D1A6">Field<span style="color: #000000b2">Ops</span></strong><br>
  <sub>Inspeções em campo. Dados que geram confiança.</sub>
</footer>
