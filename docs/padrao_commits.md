# Conventional Commits — FieldOps

## Formato

Todo commit deve seguir o formato:

```text
<type>(<scope>): <description>
```

Exemplo:

```text
feat(mobile): add offline inspection storage
```

---

## Tipos permitidos

| Type       | Uso                                          |
| ---------- | -------------------------------------------- |
| `feat`     | Nova funcionalidade                          |
| `fix`      | Correção de bug                              |
| `docs`     | Documentação                                 |
| `refactor` | Refatoração sem mudança de comportamento     |
| `test`     | Criação ou alteração de testes               |
---

## Scopes

Os scopes devem indicar a área afetada pela alteração.

| Scope        | Uso                           |
| ------------ | ----------------------------- |
| `mobile`     | Aplicativo mobile             |
| `web`        | Aplicação web                 |
| `api`        | API/backend                   |
| `db`         | Banco de dados                |
| `auth`       | Autenticação/autorização      |
| `docs`       | Documentação                  |

### Exemplos

```text
feat(mobile): add QR code equipment identification
```

```text
fix(api): prevent duplicate inspection submission
```
---

## Corpo do commit

Para alterações simples, apenas a primeira linha é suficiente:

```text
fix(mobile): prevent duplicate inspection submission
```

Para alterações mais complexas:

```text
feat(sync): implement offline inspection synchronization

Adds a local synchronization queue for inspection changes
created while the technician is offline.

Pending operations are automatically synchronized when
connectivity is restored.
```
---

## Regras

### 1. Usar inglês

Os commits devem ser escritos em inglês.

```text
feat(mobile): add offline inspection support
```

Evitar:

```text
feat(mobile): adiciona suporte offline
```

### 2. Usar verbo no imperativo

Preferir:

```text
feat(api): add inspection endpoint
```

Evitar:

```text
feat(api): added inspection endpoint
```

### 3. Não utilizar ponto final na descrição

Preferir:

```text
fix(api): validate inspection status
```

Evitar:

```text
fix(api): validate inspection status.
```

### 4. Manter a descrição curta

A primeira linha deve ser objetiva e preferencialmente ter até **72 caracteres**.

### 5. Um commit deve representar uma alteração lógica

Evitar:

```text
feat(mobile): add checklist, fix login, update dependencies and change API
```

Preferir commits separados:

```text
feat(mobile): add inspection checklist
fix(mobile): prevent login session expiration
build(mobile): update dependencies
```
---

# Branch Naming Convention

Padrão de nomenclatura das branches do FieldOps.

## Formato

**Áreas**
- mobile — Aplicativo Mobile
- web — Frontend Web
- api — Backend / API
- db — Banco de Dados
- infra — Infraestrutura
- docs — Documentação

