# FieldOps

### Plataforma de Inspeção em Campo 
 
## by Kelvim Lucas, Ryan Augusto, Gustavo Senna, Carlos Eduardo, Gustavo Souza, Gustavo Silveira

<p align="center">
  <strong>Planeje. Execute. Registre. Revise.</strong><br>
  Inspeções técnicas padronizadas, rastreáveis e integradas em um único fluxo digital.
</p>

---

## 📋 Sobre o projeto

O **FieldOps** é uma plataforma digital desenvolvida para organizações que realizam **inspeções técnicas em campo**.

A solução substitui processos baseados em formulários impressos, planilhas, mensagens e registros informais por um fluxo digital integrado, conectando o trabalho realizado pelo técnico em campo à gestão administrativa.

Por meio do FieldOps, técnicos podem receber inspeções, identificar equipamentos, executar checklists, registrar evidências e trabalhar mesmo em locais sem conexão com a internet.

Ao mesmo tempo, administradores e supervisores podem configurar modelos de inspeção, agendar atividades, atribuir técnicos, acompanhar execuções, analisar não conformidades e revisar os resultados.

> **FieldOps conecta a operação em campo à gestão, preservando evidências, histórico, localização e regras de negócio em um único fluxo.**

---

## 🎯 Objetivo

O principal objetivo do FieldOps é **digitalizar e padronizar o processo de inspeções técnicas**, garantindo maior rastreabilidade das atividades realizadas em campo.

A plataforma busca proporcionar:

* ✅ Padronização dos processos de inspeção
* 📱 Execução através de aplicativo mobile
* 📴 Funcionamento offline
* 🔄 Sincronização automática dos dados
* 📸 Registro de evidências
* 📍 Captura de localização
* 🔎 Identificação de equipamentos por QR Code
* 📋 Checklists dinâmicos
* 📝 Registro de não conformidades
* 🔐 Autenticação e autorização
* 📊 Acompanhamento administrativo
* 🕐 Histórico e auditoria

---

# 🏗️ Arquitetura

O FieldOps é dividido em componentes especializados que trabalham de forma integrada:

```text
                    ┌─────────────────────────┐
                    │    Interface Web        │
                    │ Administradores /       │
                    │ Supervisores             │
                    └────────────┬────────────┘
                                 │
                                 │ REST API
                                 │
┌─────────────────────┐          ▼          ┌──────────────────────┐
│   Aplicativo        │◄────────────────────►│       API REST       │
│      Mobile         │                     │                      │
│                     │                     │ Regras de negócio    │
│ Técnicos de campo   │                     │ Autenticação         │
│ Checklists          │                     │ Autorização           │
│ QR Code             │                     │ Persistência          │
│ Evidências          │                     │ Auditoria             │
│ GPS                 │                     │ Sincronização         │
│ Offline             │                     └──────────┬───────────┘
└──────────┬──────────┘                                │
           │                                           │
           │ SQLite                                    │
           ▼                                           ▼
┌─────────────────────┐                    ┌──────────────────────┐
│ Persistência local  │                    │     PostgreSQL       │
│                     │                    │                      │
│ Outbox               │                    │ Dados centralizados │
│ Dados pendentes      │                    │ Histórico            │
│ Inspeções offline    │                    │ Usuários             │
└─────────────────────┘                    └──────────┬───────────┘
                                                       │
                                                       ▼
                                            ┌──────────────────────┐
                                            │ Armazenamento de      │
                                            │ evidências            │
                                            │                      │
                                            │ Fotos / Arquivos      │
                                            └──────────────────────┘
```

---

# 🧩 Componentes

## 📱 Aplicativo Mobile

Aplicação destinada principalmente aos **técnicos de campo**.

Principais responsabilidades:

* Autenticação e gerenciamento de sessão
* Consulta das inspeções atribuídas
* Identificação de equipamentos por QR Code
* Execução de checklists
* Captura de fotografias
* Registro de observações
* Registro de não conformidades
* Captura de localização
* Persistência local
* Funcionamento offline
* Sincronização com a API

O aplicativo deverá preservar operações ainda não sincronizadas mesmo quando for fechado.

---

## 🖥️ Interface Administrativa

Aplicação web destinada a **administradores e supervisores**.

Permite:

* Gerenciar usuários e perfis
* Cadastrar clientes
* Cadastrar locais
* Cadastrar equipamentos
* Criar modelos de inspeção
* Versionar modelos
* Agendar inspeções
* Atribuir técnicos
* Acompanhar inspeções
* Visualizar respostas
* Consultar evidências
* Analisar não conformidades
* Aprovar ou reprovar inspeções
* Consultar indicadores

---

## ⚙️ API REST

A API funciona como o núcleo da plataforma, centralizando as regras de negócio e a comunicação entre os diferentes componentes.

Responsabilidades:

* 🔐 Autenticação
* 🛡️ Autorização
* 📋 Validação das operações
* ⚙️ Regras de negócio
* 💾 Persistência
* 📸 Upload e consulta de evidências
* 🔄 Sincronização
* 🕐 Histórico
* 📝 Auditoria
* 🔗 Integração entre Mobile e Web
* 📚 Documentação da API

---

## 🗄️ Infraestrutura de dados

A solução utiliza diferentes mecanismos de armazenamento de acordo com a necessidade de cada componente.

| Tecnologia         | Responsabilidade                    |
| ------------------ | ----------------------------------- |
| **PostgreSQL**     | Dados centrais da aplicação         |
| **SQLite**         | Persistência local no aplicativo    |
| **Object Storage** | Armazenamento de fotos e evidências |
| **Logs**           | Monitoramento e diagnóstico         |
| **Auditoria**      | Rastreamento das operações          |

---

# 🔄 Fluxo principal

O fluxo de uma inspeção no FieldOps é baseado em um ciclo completo:

```text
Configuração administrativa
          ↓
Criação do modelo
          ↓
Agendamento da inspeção
          ↓
Atribuição do técnico
          ↓
Disponibilização no aplicativo
          ↓
Execução em campo
          ↓
Checklist + QR Code + Fotos + Localização
          ↓
Armazenamento local
          ↓
Sincronização
          ↓
Revisão do supervisor
          ↓
┌──────────────────────────────┐
│                              │
▼                              ▼
APROVADA                CORREÇÃO SOLICITADA
```

---

# 📴 Funcionamento Offline

Um dos principais diferenciais do FieldOps é a capacidade de executar inspeções **mesmo sem conexão com a internet**.

Durante uma inspeção, o técnico poderá continuar trabalhando normalmente.

Os dados serão armazenados localmente e posteriormente enviados para a API quando a conexão estiver disponível.

```text
          Técnico
             │
             ▼
      ┌──────────────┐
      │  Aplicativo  │
      └──────┬───────┘
             │
       Sem conexão
             │
             ▼
      ┌──────────────┐
      │    SQLite    │
      │              │
      │ Dados locais │
      │    Outbox    │
      └──────┬───────┘
             │
        Conexão volta
             │
             ▼
      ┌──────────────┐
      │ Sincronização│
      └──────┬───────┘
             │
             ▼
        ┌─────────┐
        │ API REST│
        └────┬────┘
             │
             ▼
        PostgreSQL
```

### Outbox

Operações realizadas offline serão armazenadas em uma **Outbox local**.

Cada operação aguardará até que possa ser enviada ao servidor.

Isso permite que o aplicativo preserve o trabalho realizado pelo técnico mesmo que:

* o aplicativo seja fechado;
* o dispositivo fique temporariamente sem internet;
* a conexão seja perdida durante uma inspeção.

---

# 📋 Escopo do MVP

O MVP será capaz de demonstrar o fluxo completo de uma inspeção:

### Administrador

* [ ] Cadastrar dados básicos
* [ ] Gerenciar usuários
* [ ] Cadastrar clientes
* [ ] Cadastrar locais
* [ ] Cadastrar equipamentos

### Supervisor

* [ ] Criar modelo de inspeção
* [ ] Versionar modelo
* [ ] Agendar inspeção
* [ ] Atribuir técnico
* [ ] Acompanhar execução
* [ ] Revisar resultado
* [ ] Aprovar inspeção
* [ ] Reprovar ou solicitar correção

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

---

# 🚫 Fora do MVP

Os seguintes recursos não fazem parte da primeira versão:

* Aplicativo exclusivo para clientes
* Portal público
* Multiempresa com isolamento completo
* Pagamentos e faturamento
* Roteirização automática
* Rastreamento contínuo de técnicos
* Chamadas de vídeo
* Armazenamento de vídeos longos
* Assinatura eletrônica com validade jurídica
* Relatórios regulatórios avançados
* Integrações com ERPs
* Diagnóstico automático por IA
* Integrações com sensores IoT
* Resolução colaborativa de conflitos complexos de sincronização

---

# 📦 Modelo conceitual

Os principais conceitos utilizados pelo sistema são:

| Conceito               | Descrição                                            |
| ---------------------- | ---------------------------------------------------- |
| **Cliente**            | Organização atendida pela empresa de inspeções       |
| **Local**              | Unidade, planta, prédio, setor ou área de um cliente |
| **Equipamento**        | Ativo físico que poderá ser inspecionado             |
| **Modelo de inspeção** | Estrutura reutilizável que define a inspeção         |
| **Inspeção**           | Instância agendada de um modelo                      |
| **Checklist**          | Conjunto de itens que devem ser respondidos          |
| **Evidência**          | Arquivo ou registro que comprova uma resposta        |
| **Não conformidade**   | Situação que não atende ao requisito esperado        |
| **Sincronização**      | Troca de alterações entre dispositivo e servidor     |
| **Snapshot**           | Cópia imutável do modelo usada por uma inspeção      |
| **Outbox**             | Fila local de operações aguardando sincronização     |
| **MVP**                | Menor versão capaz de demonstrar o fluxo principal   |

---

# 🔐 Segurança e rastreabilidade

A plataforma considera segurança e auditoria como partes fundamentais do processo.

O sistema deverá controlar:

* Autenticação dos usuários
* Perfis e permissões
* Autorização das operações
* Histórico das alterações
* Auditoria das operações
* Identificação do responsável pela inspeção
* Registro de localização
* Evidências associadas às respostas
* Versionamento dos modelos
* Rastreabilidade da sincronização

A **API REST será a fonte oficial dos dados após a sincronização**.

---

# 📱 Plataforma

A primeira versão terá como prioridade:

**Mobile**

* Android
* Expo

**Web**

* Navegadores modernos

**Backend**

* API REST

**Banco**

* PostgreSQL

**Persistência local**

* SQLite

---

# 🗂️ Estrutura do projeto

A estrutura definitiva dos repositórios poderá variar conforme a implementação, mas a solução está organizada conceitualmente da seguinte maneira:

```text
fieldops/
│
├── mobile/
│   ├── app/
│   ├── components/
│   ├── services/
│   ├── database/
│   ├── sync/
│   └── ...
│
├── web/
│   ├── pages/
│   ├── components/
│   ├── services/
│   └── ...
│
├── api/
│   ├── controllers/
│   ├── services/
│   ├── repositories/
│   ├── models/
│   ├── auth/
│   └── ...
│
├── docs/
│   ├── architecture/
│   ├── api/
│   └── ...
│
└── README.md
```

---

# 🚀 Roadmap

### Fase 1 — Fundação

* [ ] Definição da arquitetura
* [ ] Configuração dos projetos
* [ ] Banco de dados
* [ ] API REST
* [ ] Autenticação
* [ ] Estrutura inicial do aplicativo

### Fase 2 — Gestão

* [ ] Usuários
* [ ] Clientes
* [ ] Locais
* [ ] Equipamentos
* [ ] Modelos de inspeção
* [ ] Versionamento

### Fase 3 — Inspeção

* [ ] Agendamento
* [ ] Atribuição
* [ ] Checklist
* [ ] QR Code
* [ ] Fotografias
* [ ] Localização
* [ ] Não conformidades

### Fase 4 — Offline

* [ ] Banco local
* [ ] Outbox
* [ ] Sincronização
* [ ] Tratamento de operações pendentes

### Fase 5 — Revisão

* [ ] Painel de acompanhamento
* [ ] Revisão das inspeções
* [ ] Aprovação
* [ ] Reprovação
* [ ] Solicitação de correções
* [ ] Histórico

---

# 🎯 Visão futura

Após a consolidação do MVP, o FieldOps poderá evoluir para uma plataforma completa de gestão de operações de campo, incorporando recursos como:

* Integração com ERPs
* Dashboards avançados
* Relatórios regulatórios
* Roteirização de equipes
* Aplicativo para clientes
* Integrações IoT
* Inteligência artificial
* Automação de análises
* Recursos avançados de colaboração

---

# 💡 Por que FieldOps?

Inspeções técnicas geram informações importantes para a operação, mas processos manuais podem dificultar a padronização, rastreabilidade e análise desses dados.

O FieldOps transforma esse processo em um fluxo digital:

```text
              ANTES
               
 Papel ──┐
 Planilha├──► Dados dispersos
 Mensagens┘
                  │
                  ▼
             Dificuldade de
             rastreamento


              FIELDOPS

 Técnico ───────┐
                │
 Supervisor ────┼──► FieldOps ──► Dados centralizados
                │
 Administrador ─┘
                       │
              ┌────────┼────────┐
              ▼        ▼        ▼
           Evidências Histórico Auditoria
```

O resultado é uma operação mais **padronizada, rastreável e conectada**, desde o planejamento da inspeção até sua aprovação.

---

## 📄 Documentação

A documentação técnica do projeto está disponível no diretório:

```text
/docs
```

Documentações específicas sobre arquitetura, API, banco de dados, sincronização e regras de negócio serão adicionadas conforme a evolução do projeto.

---

## 👥 Equipe

**FieldOps**

Plataforma desenvolvida para digitalização e gerenciamento de inspeções técnicas em campo.

---

<p align="center">
  <strong>FieldOps</strong><br>
  <sub>Inspeções em campo. Dados que geram confiança.</sub>
</p>
