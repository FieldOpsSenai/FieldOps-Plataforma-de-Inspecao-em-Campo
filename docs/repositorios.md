## Organização dos Repositórios

O FieldOps será organizado em três repositórios independentes:

- `fieldops-api`: backend e API REST da plataforma.
- `fieldops-mobile`: aplicativo móvel utilizado pelos técnicos.
- `fieldops-admin`: aplicação web utilizada por administradores e supervisores.

Os repositórios não compartilharão diretamente o banco de dados ou
implementações internas. A comunicação entre os clientes (`mobile` e
`admin`) e o backend ocorrerá exclusivamente através da API REST.

O `fieldops-api` será responsável por centralizar autenticação,
autorização, regras de negócio, persistência, auditoria e integrações.