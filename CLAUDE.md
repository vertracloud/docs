# docs/ — orientador

**Documentação pública da Vertra Cloud** (`docs.vertracloud.app`) + a **base de conhecimento** interna. Este repo também hospeda `VERTRA_KNOWLEDGE_BASE.md`, a fonte da verdade de produto para todos os agentes.

> Contexto de plataforma e regras no **`../CLAUDE.md`** (mestre).

## Stack

**Mintlify** (`docs.json`, `"$schema": mintlify.com/docs.json`, theme `mint`). Sem `package.json` — build/preview é o CLI padrão (`mintlify dev`) e deploy hospedado pela Mintlify. Domínio `docs.vertracloud.app`.

## Estrutura de conteúdo

```
introduction.mdx / overview.mdx / how-to-host.mdx / deploy-github.mdx / common-errors.mdx
applications.mdx / databases.mdx / sites.mdx / credits.mdx / plan-downgrade.mdx / workspaces.mdx / vscode-extension.mdx
tutorials/       15+ guias por linguagem/runtime (nodejs, python, go, rust, java, php, ruby, bun, static, discord-bot, ...)
api-reference/   introduction.mdx, limitations.mdx, endpoint/*.mdx (apps, databases, workspaces, users, services)
changelog.mdx    índice + changelog/ (entradas datadas pela entrega da feature)
images/ logo/ favicon.svg
docs.json        navegação, tema, anchors
VERTRA_KNOWLEDGE_BASE.md   ← fonte da verdade de produto (planos, créditos, limites, linguagens, erros, troubleshooting)
```

## Regras

- **`VERTRA_KNOWLEDGE_BASE.md` é canônico** para números de produto. Mudou plano/preço/limite/linguagem/código de erro em qualquer repo? **Atualize a KB aqui** — os outros docs apontam para ela, não duplicam.
- **`api-reference/` deve casar com o contrato real** (`../api-types/` + rotas da `../api/`). Endpoint novo/alterado → atualize o `.mdx` correspondente. Os tipos em `api-types/rest/v1/*` já linkam a doc pública via `@see`.
- **Changelog:** toda feature/alteração visível ao usuário vira uma entrada em `changelog/`, **datada pela entrega da feature completa** (não por mês). Índice em `changelog.mdx`.
- Conteúdo público em pt-br; nada de segredo ou detalhe de infra interna (portas, tokens, nomes de container) na doc pública.

---

**Mudou estrutura/navegação/stack da doc? Atualize este `CLAUDE.md`.** E lembre: a KB e o `api-reference/` são atualizados por quem muda o produto/contrato — não deixe divergir (Regra zero do mestre).
