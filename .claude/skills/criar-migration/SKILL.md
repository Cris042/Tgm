---
name: criar-migration
description: Cria uma migration versionada de banco de dados neste projeto, conforme roles.md §6.10. Obrigatória para TODA alteração estrutural de banco — nunca alterar schema manualmente.
---

# Criar Migration

Toda mudança estrutural de banco (tabela, coluna, índice, constraint, dado de referência) entra por migration versionada, vinculada à task e ao PRD.

## Pré-requisitos

1. A task e o PRD existem e preveem a mudança de banco.
2. A ferramenta de migration do projeto está definida (ver `lib.md` e ADRs). Se ainda não estiver, consulte o agente `arquiteto` e o usuário — a escolha da ferramenta é decisão relevante (possível ADR, roles.md §6.1).
3. **Consulte o Context7** para a sintaxe e convenções da ferramenta escolhida (Flyway, Liquibase, Prisma, Alembic, etc.) — não presuma (roles.md §6.12).

## Passo a passo

1. Nomeie no padrão da ferramenta; na ausência de convenção própria, use `VNNNN__descricao_curta` com numeração sequencial.
2. Escreva a migration com cabeçalho-comentário padrão:
   ```
   -- Task: NNNN — [nome]
   -- PRD: docs/prd/NNNN-titulo.md
   -- Descrição: [o que muda e por quê]
   -- Rollback: [como desfazer / arquivo de down / "não aplicável" com justificativa]
   ```
3. **Rollback**: defina a estratégia de reversão quando aplicável (script down, coluna mantida até task de limpeza, etc.).
4. **Idempotência**: use guardas quando a ferramenta permitir (`IF NOT EXISTS`, checagens) — migrations re-executáveis reduzem risco.
5. **Impacto em dados existentes**: avalie e documente (tabela grande? lock? backfill necessário?). Mudanças destrutivas (drop, rename) exigem confirmação do usuário.
6. **Valide localmente antes do push**: suba o banco do `docker-compose` (agente `sre-devops`) e aplique a migration do zero e sobre base já migrada.
7. Registre a migration no PRD (arquivos criados) e no `plan.md`.

## Checklist final

- [ ] Vinculada à task e ao PRD (cabeçalho)
- [ ] Rollback definido ou justificado
- [ ] Idempotente quando possível
- [ ] Impacto em dados existentes avaliado
- [ ] Validada localmente (aplicação limpa + incremental)
- [ ] Nenhuma alteração manual de schema fora dela
