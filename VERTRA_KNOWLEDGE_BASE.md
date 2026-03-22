# Vertra Cloud — Base de Conhecimento

> Este documento contém todas as informações da plataforma. Mantenha-o atualizado a cada mudança.

---

## 1. Visão Geral

A Vertra Cloud é uma plataforma brasileira de hospedagem em nuvem para deploy de aplicações e bancos de dados gerenciados. Suporta 10+ linguagens, 4 tipos de banco, monitoramento em tempo real, domínios personalizados, sistema de créditos, workspaces colaborativos e extensão VSCode.

- **Site**: https://vertracloud.app
- **Dashboard**: https://vertracloud.app/dashboard
- **API**: https://api.vertracloud.app
- **Documentação**: https://docs.vertracloud.app

---

## 2. Linguagens Suportadas

| Linguagem | Recomendada | Última | Outras |
|-----------|:-----------:|:------:|:------:|
| JavaScript | Node.js 22.18.0 | 24.5.0 | 20.18.0 |
| TypeScript | Node.js 22 | 22 | 18, 20 |
| Python | 3.13 | 3.13 | 3.12, 3.11 |
| Go | 1.23 | 1.23 | 1.22, 1.21 |
| Rust | 1.86 | 1.87 | 1.85 |
| Java | Temurin JRE 21 | 21 | 17 |
| Bun | 1.2.2 | 1.2.2 | 1.1.0 |
| PHP | 8.3 | 8.3 | 8.2 |
| Ruby | 3.3 | 3.4 | 3.2 |
| Static | — | — | HTML/CSS/JS |

---

## 3. Bancos de Dados

| Banco | Versão | Porta | TLS | Autenticação |
|-------|--------|:-----:|:---:|-------------|
| PostgreSQL | 17 | 5432 | Obrigatório | Certificado + Senha |
| MongoDB | 8.0.11 | 27017 | Obrigatório | CA assinado pela plataforma |
| Redis | 7 | 6379 | Obrigatório | Senha + TLS |
| MySQL | 8.0 | 3306 | Obrigatório | X509 obrigatório |

Todos os bancos geram certificados TLS automaticamente (CA, servidor, cliente). Os certificados podem ser baixados no dashboard ou via API.

**Host**: `vertra-cloud-<tipo>-<id>.db.vertraweb.app`

**Operações**: Iniciar, Parar, Reiniciar, Resetar (destrutivo), Resetar Senha, Resetar Certificados, Download/Restauração de Snapshot.

---

## 4. Planos e Preços

| Plano | Preço | RAM | vCPU | Max Projetos | Créditos AI/semana |
|-------|:-----:|:---:|:----:|:------------:|:------------------:|
| Free | R$0 | Créditos (até 1 GB) | 0.25 | 1 app + 1 db | 50 |
| Economy | R$1,99/mês | 256 MB | 0.3 | 2 | 100 |
| Pro | R$5,99/mês | 1.024 MB | 0.5 | 8 | 250 |
| Scale | R$10,99/mês | 2.048 MB | 1 | 16 | 500 |
| Intermediary | R$18,99/mês | 3.072 MB | 1.5 | 24 | 750 |
| Enterprise-4 | R$23,99+/mês | 4.096 MB | 2 | 32 | 1.000 |
| Enterprise-32 | Superior | 32.768 MB | 12 | 256 | 4.500 |

### IDs dos Planos (plan_id)

| ID | Plano |
|:--:|-------|
| 1 | FREE |
| 2 | ECONOMY |
| 3 | PRO |
| 4 | SCALE |
| 9 | INTERMEDIARY |
| 5 | ENTERPRISE_4 |
| 19 | ENTERPRISE_6 |
| 6 | ENTERPRISE_8 |
| 10 | ENTERPRISE_12 |
| 11 | ENTERPRISE_14 |
| 7 | ENTERPRISE_16 |
| 12 | ENTERPRISE_18 |
| 13 | ENTERPRISE_20 |
| 14 | ENTERPRISE_22 |
| 15 | ENTERPRISE_24 |
| 16 | ENTERPRISE_26 |
| 17 | ENTERPRISE_28 |
| 18 | ENTERPRISE_30 |
| 8 | ENTERPRISE_32 |

### Funcionalidades por Plano

| Funcionalidade | Free | Economy | Pro | Scale | Intermediary | Enterprise |
|----------------|:----:|:-------:|:---:|:-----:|:------------:|:----------:|
| Hospedagem de sites | — | — | Sim | Sim | Sim | Sim |
| Auto-restart | — | — | Sim | Sim | Sim | Sim |
| Gerenciador de arquivos | — | — | Sim | Sim | Sim | Sim |
| Métricas avançadas | — | — | Sim | Sim | Sim | Sim |
| Backups diários | — | — | — | Sim | Sim | Sim |
| Backups manuais | — | — | — | Sim | Sim | Sim |
| Subdomínio Vertraweb | — | — | — | Sim | Sim | Sim |
| Domínio personalizado | — | — | — | — | Sim | Sim |
| Auto-deploy (GitHub) | — | — | — | — | Sim | Sim |
| Workspaces | — | — | — | — | — | Sim (5-24 membros) |

### Limites do Plano Free
- Máximo 1 app + 1 banco de dados (somente créditos)
- 500 créditos compute/semana, 50 créditos AI/semana
- Projetos inativos por 30+ dias são deletados automaticamente
- Notificações por email nos dias 7, 23, 27 antes da exclusão
- Sem hospedagem de site, sem auto-restart, sem gerenciador de arquivos

---

## 5. Sistema de Créditos

### Como Funciona
- **Alocação gratuita semanal**: Reset toda segunda-feira às 00:00 UTC
- **Créditos não acumulam** entre ciclos
- **Créditos pagos**: Comprados via dashboard, expiram em 365 dias
- **Cobrança**: Por hora, automática. Fórmula: `ceil(RAM_MB / 100) × taxa` créditos/hora

### Taxas

| Plano | Taxa |
|-------|------|
| Free | 10 créditos por 100 MB por hora |
| Planos pagos | 7 créditos por 100 MB por hora |

### Exemplos de Custo (Planos Pagos)

| RAM | Créditos/hora | Créditos/dia | Créditos/mês |
|-----|:------------:|:-----------:|:-------------:|
| 100 MB | 7 | 168 | 5.040 |
| 256 MB | 18 | 432 | 12.960 |
| 512 MB | 36 | 864 | 25.920 |
| 1.024 MB | 72 | 1.728 | 51.840 |

### Limites de Memória no Modo Créditos

| Plano | Máximo por Recurso |
|-------|:------------------:|
| Free | 1.024 MB (1 GB) |
| Pagos | 16.384 MB (16 GB) |

### Quando os Créditos Acabam
Todos os recursos baseados em créditos são **parados automaticamente**. Opções:
- Comprar créditos adicionais via dashboard
- Aguardar o reset semanal (toda segunda-feira)
- Migrar o recurso para modo plano fixo (planos pagos)

---

## 6. Tipos de Aplicação

| Tipo | Código | Descrição |
|------|:------:|-----------|
| Bot | 1 | Processo em background, sem porta HTTP. Bots Discord, automação, workers. |
| Website | 2 | Acessível via HTTP/HTTPS, recebe subdomínio. APIs, web apps, SPAs. |

### Ciclo de Vida
```
Criando → Iniciando → Online → Parado (manual/créditos) ou Erro (crash)
Erro → Iniciando (auto-restart) ou Parado (crash loop: 5x em 10min)
```

### Arquivo de Configuração (vertracloud.config)
Arquivo INI opcional na raiz do projeto:
```
NAME=Meu App
MAIN=index.js
START=npm start
SUBDOMAIN=meu-app
VERSION=22
PORT=80
MEMORY=512
AUTORESTART=true
```

### Subdomínios
- Formato: `seu-app.vertraweb.app`
- Único por aplicação
- Configurável na criação ou nas configurações
- Disponível a partir do plano Scale

### Domínios Personalizados
- Disponível a partir do plano Intermediary
- Configurar registro CNAME no DNS apontando para o endereço fornecido
- SSL provisionado automaticamente após validação do DNS
- Limite: 1 domínio personalizado por aplicação

---

## 7. Auto-Restart e Detecção de Crash Loop

- Containers que crasham são reiniciados automaticamente (planos Pro+)
- Exit code 0 (terminação normal) NÃO dispara restart
- **Crash loop**: 5 crashes em 10 minutos → auto-restart desativado por 24 horas
- **Cooldown**: Mínimo 1 hora entre restarts consecutivos
- **Estabilidade**: Container precisa estar online 60+ segundos para contar como estável

---

## 8. Proteções da Plataforma (Vertra Shield)

- **Isolamento de containers**: Memória dedicada, CPU limitada, storage isolado, rede segregada
- **Monitoramento de tráfego**: Em tempo real por aplicação
- **Detecção de burst**: Análise de janela deslizante para picos anormais
- **Limitação de banda**: Proporcional à RAM alocada
- **Mitigação automática**: Violadores persistentes são pausados com cooldown

### Limites de Banda por Memória

| RAM | Banda | Requisições/seg (aprox.) |
|-----|:-----:|:------------------------:|
| 100 MB | 50 Mbit | ~300 |
| 256 MB | 100 Mbit | ~600 |
| 512 MB | 200 Mbit | ~900 |
| 1.024 MB | 400 Mbit | ~1.200 |
| 2.048 MB | 800 Mbit | ~2.400 |
| 4.096 MB | 1.600 Mbit | ~4.800 |

---

## 9. SSL/TLS

- Todos os sites recebem certificados SSL/TLS automáticos
- Renovação automática antes da expiração
- Redirecionamento HTTP → HTTPS ativado por padrão
- Domínios personalizados também recebem SSL automático
- Todas as conexões de banco de dados exigem TLS

---

## 10. Snapshots

- Criação manual de snapshots para apps e bancos
- Restaurar de qualquer snapshot anterior (cooldown de 30 segundos)
- Download do conteúdo do snapshot como ZIP
- Disponível a partir do plano Scale (backups manuais)

---

## 11. Workspaces

- Colaboração em equipe com controle de acesso por cargo
- Disponível apenas no plano Enterprise
- 5 a 24 membros dependendo do plano

### Cargos e Permissões

| Cargo | Gerenciar Membros | Deploy/Gerenciar | Iniciar/Parar | Ver Métricas | Deletar | Deletar Workspace |
|-------|:-:|:-:|:-:|:-:|:-:|:-:|
| Owner | Sim | Sim | Sim | Sim | Sim | Sim |
| Admin | Sim (não owner) | Sim | Sim | Sim | Sim | Não |
| Developer | Não | Sim | Sim | Sim | Não | Não |
| Operator | Não | Não | Sim | Sim | Não | Não |
| Viewer | Não | Não | Não | Sim | Não | Não |

---

## 12. Gerenciador de Arquivos

- Disponível a partir do plano Pro
- Navegar e editar arquivos diretamente no dashboard
- Syntax highlighting para todas as linguagens
- Upload via drag-and-drop (arquivos ou ZIP)
- Árvore de arquivos com até 6 níveis de profundidade
- Criar, editar, mover, deletar arquivos e pastas
- Diretórios ocultos: `node_modules`, `.git`, `__pycache__`, `vendor`, `.venv`, `.next`
- Upload bloqueado para: `vertracloud.config`

---

## 13. Deploy

### Métodos
1. **Upload de ZIP** via dashboard ou API
2. **Integração GitHub** — seleção de repositórios (incluindo privados)
3. **Webhooks GitHub** — deploy automático no push (planos Pro+)
4. **Extensão VSCode** — deploy direto do editor

### Processo
Upload do código → Instalação de dependências → Inicialização do container → Atribuição de subdomínio → Provisionamento SSL

### Limites de Upload
- Tamanho máximo do ZIP: 100 MB
- Tempo máximo de build: 5 minutos
- 1 porta exposta por aplicação

### Arquivos para Excluir do ZIP
- **JavaScript/TypeScript**: `node_modules`, `.npm`, `package-lock.json`, `.next`, `dist`
- **Python**: `venv`, `.venv`, `.cache`, `__pycache__`, `.env`
- **Go**: `vendor`
- **Rust**: `target`
- **Java**: `target`, `.gradle`, `build`
- **PHP/Ruby**: `vendor`

---

## 14. Downgrade de Plano

- Disponível via dashboard ou API: `POST /v1/users/me/downgrade`
- **Fórmula**: `novosDias = diasRestantes × (preçoAtual / preçoAlvo)`
- **Restrições**: FREE e ECONOMY não podem fazer downgrade
- **Verificações**: Uso de memória deve caber no plano alvo, rate limit (1x a cada 3 horas)
- **Impacto**: Limite de memória reduzido, funcionalidades de planos superiores desativadas, workspaces perdidos se sair do Enterprise, créditos não afetados

---

## 15. Extensão VSCode

- Disponível no VS Code Marketplace (pesquisar "Vertra Cloud")
- Funcionalidades: Deploy rápido, gerenciamento de apps, gerenciamento de arquivos, monitoramento em tempo real
- Requisitos: VS Code 1.80+, conta Vertra ativa, conexão com internet
- Deploy via command palette: `Ctrl+Shift+P` → "Vertra: Deploy"

---

## 16. Métodos de Autenticação

- **Discord OAuth** — Login e vinculação de conta
- **GitHub OAuth** — Login e vinculação de conta
- **Google OAuth** — Login e vinculação de conta
- **Magic Link** — Autenticação sem senha por email
- **Chave de API** — Para acesso programático (gerar nas configurações do dashboard)
- **Troca de conta** — Até 5 contas salvas no mesmo navegador

---

## 17. Referência da API

### Autenticação
Todas as requisições exigem Bearer token no header Authorization:
```
Authorization: Bearer SEU_TOKEN
```

### Formato de Resposta
- **Sucesso**: `{ "response": { ... } }`
- **Erro**: `{ "code": "CODIGO_ERRO", "message": "..." }`

### Códigos de Erro Comuns

| Código | Descrição |
|--------|-----------|
| UNAUTHORIZED | Não autenticado ou permissões insuficientes |
| FORBIDDEN | Sem permissão para acessar este recurso |
| APP_NOT_FOUND | Aplicação não encontrada |
| DATABASE_NOT_FOUND | Banco de dados não encontrado |
| PLAN_RESTRICTED_FEATURE | Funcionalidade não disponível no plano atual |
| INSUFFICIENT_CREDITS | Créditos insuficientes |
| INSUFFICIENT_MEMORY | Memória insuficiente no plano |
| MAX_APPS_REACHED | Limite de apps atingido para o plano |
| MAX_DATABASES_REACHED | Limite de bancos atingido para o plano |
| MEMORY_EXCEEDS_CREDITS_LIMIT | RAM excede o máximo do modo créditos |
| FILE_TOO_LARGE | Upload excede 100 MB |
| SUBDOMAIN_ALREADY_IN_USE | Subdomínio já em uso |
| RATE_LIMIT_EXCEEDED | Muitas requisições |
| INTERNAL_SERVER_ERROR | Erro interno do servidor |

### Endpoints Principais

#### Aplicações
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/v1/apps` | Criar aplicação (multipart: file, memory, name, etc.) |
| GET | `/v1/apps/{id}` | Detalhes da aplicação |
| DELETE | `/v1/apps/{id}` | Deletar aplicação |
| POST | `/v1/apps/{id}/start` | Iniciar aplicação |
| POST | `/v1/apps/{id}/stop` | Parar aplicação |
| POST | `/v1/apps/{id}/restart` | Reiniciar aplicação |
| GET | `/v1/apps/status` | Status de todas as apps (cpu, ram, running) |
| GET | `/v1/apps/{id}/status` | Status detalhado (cpu, ram, storage, network, uptime) |
| GET | `/v1/apps/{id}/logs` | Logs da aplicação (texto) |
| GET | `/v1/apps/{id}/realtime` | Logs em tempo real (SSE stream) |
| GET | `/v1/apps/{id}/metrics` | Métricas das últimas 24h |
| GET | `/v1/apps/{id}/download` | Download da app como ZIP |
| POST | `/v1/apps/{id}/commit` | Upload de novo snapshot |
| GET | `/v1/apps/{id}/commits` | Listar snapshots |
| POST | `/v1/apps/{id}/commit/{cid}/revert` | Reverter para snapshot |
| GET | `/v1/apps/{id}/envs` | Listar variáveis de ambiente |
| POST | `/v1/apps/{id}/envs` | Criar/editar variáveis |
| GET | `/v1/apps/{id}/files` | Gerenciador — listar arquivos |
| GET | `/v1/apps/{id}/files/content` | Conteúdo de um arquivo |
| PUT | `/v1/apps/{id}/files` | Criar/atualizar arquivo |
| DELETE | `/v1/apps/{id}/files` | Deletar arquivo/pasta |
| POST | `/v1/apps/{id}/network/custom` | Adicionar domínio personalizado |
| GET | `/v1/apps/{id}/network/dns` | Obter registros DNS |

#### Bancos de Dados
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/v1/databases` | Criar banco de dados |
| GET | `/v1/databases/{id}` | Detalhes do banco |
| POST | `/v1/databases/{id}/start` | Iniciar banco |
| POST | `/v1/databases/{id}/stop` | Parar banco |
| POST | `/v1/databases/{id}/restart` | Reiniciar banco |
| POST | `/v1/databases/{id}/reset` | Resetar banco (destrutivo) |
| GET | `/v1/databases/status` | Status de todos os bancos |
| GET | `/v1/databases/{id}/status` | Status detalhado |
| GET | `/v1/databases/{id}/metrics` | Métricas das últimas 24h |
| GET | `/v1/databases/{id}/credentials/certificate` | Obter certificados TLS |
| POST | `/v1/databases/{id}/credentials/reset` | Resetar senha |

#### Usuários
| Método | Rota | Descrição |
|--------|------|-----------|
| GET | `/v1/users/@me` | Dados do usuário (apps, dbs, plano, créditos, conexões) |
| PATCH | `/v1/users/me` | Atualizar perfil |
| POST | `/v1/users/me/downgrade` | Downgrade do plano |
| POST | `/v1/users/me/generate-api-key` | Gerar chave de API |

#### Workspaces
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/v1/workspaces` | Criar workspace |
| GET | `/v1/workspaces` | Listar workspaces |
| GET | `/v1/workspaces/{id}` | Detalhes do workspace |
| PUT | `/v1/workspaces/{id}` | Atualizar workspace |
| DELETE | `/v1/workspaces/{id}` | Deletar workspace |
| POST | `/v1/workspaces/{id}/members` | Adicionar membro |
| PUT | `/v1/workspaces/{id}/members/{uid}` | Alterar cargo |
| DELETE | `/v1/workspaces/{id}/members/{uid}` | Remover membro |
| POST | `/v1/workspaces/{id}/apps/{appId}` | Associar app |
| DELETE | `/v1/workspaces/{id}/apps/{appId}` | Desassociar app |

#### Créditos
| Método | Rota | Descrição |
|--------|------|-----------|
| GET | `/v1/credits/balance` | Saldo de créditos |
| GET | `/v1/credits/usage` | Histórico de uso (paginado) |
| GET | `/v1/credits/cost?ram={mb}` | Estimativa de custo |

#### Serviços
| Método | Rota | Descrição |
|--------|------|-----------|
| GET | `/v1/status` | Status da infraestrutura (sem autenticação) |

---

## 18. Variáveis de Ambiente

- Injetadas no container na inicialização
- Gerenciamento via dashboard ou API
- Limites: Máximo 25 variáveis, chave máx. 100 caracteres, valor máx. 1.000 caracteres
- Criptografadas em repouso
- Chaves proibidas: `PORT`, `HOST`, `PATH`, `HOME`, `USER`, `SHELL`

---

## 19. Limpeza Automática (Plano Free)

Projetos no plano Free inativos por mais de 30 dias são deletados automaticamente:

| Dia | Ação |
|:---:|------|
| 7 | Primeira notificação por email |
| 23 | Segundo aviso |
| 27 | Aviso final com link de reativação |
| 30 | Exclusão automática (irreversível) |

---

## 20. Problemas Comuns e Soluções

### Plataforma

- **App crashando / OOMKilled**: Memória insuficiente. Aumente a RAM alocada. Java/Puppeteer precisam de 512 MB+.
- **Crash loop (auto-restart desativado)**: 5 crashes em 10 min. Verifique logs, corrija o erro raiz, faça redeploy.
- **App para imediatamente (exit code 0)**: Processo não tem nada mantendo vivo. Garanta que bot está logado ou servidor está escutando.
- **ZIP muito grande**: Exclua `node_modules`, `venv`, `.git`, `vendor`, `target`, `__pycache__`.
- **Build excede 5 minutos**: Remova dependências desnecessárias.
- **Site retorna timeout**: Bind em `0.0.0.0` (não `localhost`). Use a porta do `PORT`.
- **Domínio personalizado não funciona**: Plano Intermediary+, CNAME correto, aguardar propagação DNS.
- **Conexão recusada no banco**: TLS obrigatório. Baixe certificados no dashboard.
- **Créditos acabando rápido**: `ceil(RAM_MB / 100) × taxa` por hora. Reduza RAM ou pare recursos ociosos.
- **Limite de projetos**: Free = 1 app + 1 db. Upgrade para mais.
- **Email não recebido**: Verifique spam. Tente outro método (Discord, GitHub, Google).

### Node.js / JavaScript

- **`Cannot find module 'xxx'`**: Pacote não está em `dependencies` do `package.json` (pode estar em `devDependencies`).
- **`missing script: start`**: Adicione `"start": "node index.js"` em `scripts` do `package.json`.
- **`Cannot use import statement outside a module`**: Adicione `"type": "module"` ao `package.json`, ou use `require()`.
- **`ERR_REQUIRE_ESM`**: Pacote só suporta ESM. Use ESM ou versão antiga (ex: `node-fetch@2`).
- **`ERESOLVE dependency tree`**: Crie `.npmrc` com `legacy-peer-deps=true`.
- **`EADDRINUSE`**: Porta já em uso. Apenas um `app.listen()` no código.
- **Módulos nativos falham** (better-sqlite3): Não envie `node_modules/`. A plataforma compila para Linux.

### TypeScript

- **`tsx / ts-node: command not found`**: Adicione `tsx` ao `dependencies`.
- **`TSError: Unable to compile`**: Inclua `tsconfig.json`. Corrija erros TS antes do deploy.

### Python

- **`ModuleNotFoundError`**: Módulo não está em `requirements.txt`. Gere com `pip freeze > requirements.txt`.
- **`requirements.txt` não encontrado**: Verifique nome exato e extensão (cuidado com `.txt.txt` no Windows).
- **`SyntaxError: invalid syntax`**: Versão do Python selecionada não suporta o recurso usado. Atualize a versão.
- **`UnicodeDecodeError`**: Salve arquivos como UTF-8. Use `encoding='utf-8'` ao abrir arquivos.
- **Flask/Django não acessível**: Use Gunicorn: `gunicorn app:app --bind 0.0.0.0:80`.

### Go

- **`go.mod not found`**: Execute `go mod init` e `go mod tidy`. Inclua `go.mod` e `go.sum`.
- **Binário incompatível**: Compile para Linux: `GOOS=linux GOARCH=amd64 go build`.

### Java

- **`no main manifest attribute`**: Configure o build tool para criar fat JAR com Main-Class.
- **`OutOfMemoryError`**: Java precisa de 512 MB+. Use flags: `-Xmx256m -Xms128m`.

### Bots Discord

- **`Invalid token` / `Improper token`**: Gere novo token no Developer Portal. Configure como variável de ambiente.
- **`DisallowedIntents`**: Habilite intents privilegiados no Developer Portal (Message Content, Server Members, Presence).
- **`ClientMissingIntents`**: Especifique intents no código: `new Client({ intents: [...] })`.
- **Bot offline aleatoriamente**: Memória insuficiente ou discord.js/discord.py desatualizado.
- **`on_message` não funciona (discord.py)**: Falta `intents.message_content = True` + habilitar no Developer Portal.

### Variáveis de Ambiente

- **Valores undefined/null**: Configure via dashboard, não dependa de arquivo `.env`.
- **`.env` não funciona**: A plataforma não lê `.env`. Use a interface de variáveis do dashboard.

---

## 21. Glossário

| Termo | Definição |
|-------|-----------|
| Aplicação | Um projeto deployado (bot ou website) rodando na Vertra Cloud |
| Banco de dados | Instância gerenciada (PostgreSQL, MongoDB, Redis, MySQL) |
| Workspace | Espaço de colaboração em equipe com controle de acesso (Enterprise) |
| Snapshot | Cópia salva do estado de uma aplicação ou banco de dados |
| Créditos | Moeda usada para cobrança por hora de recursos |
| Vertra Shield | Sistema de proteção de rede (monitoramento, mitigação DDoS) |
| Subdomínio | URL atribuída automaticamente: `nome-app.vertraweb.app` |
| Domínio personalizado | Domínio próprio do usuário conectado a uma aplicação |
| Auto-restart | Reinício automático do container em caso de crash (planos Pro+) |
| Crash loop | 5 crashes em 10 minutos — desativa auto-restart por 24 horas |
| vertracloud.config | Arquivo de configuração opcional na raiz do projeto |
| Deploy | Processo de envio e publicação do código na plataforma |
| Build | Processo de construção e instalação de dependências |
| Container | Ambiente isolado onde a aplicação ou banco de dados roda |
