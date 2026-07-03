# plan.md — Plano da Task em Andamento

> Este arquivo é o plano vivo da task corrente **do projeto** — não confundir com o *plan mode* do Claude Code (que grava em `~/.claude/plans/`). Atualizado durante a implementação; reflete o estado real (regras em `roles.md` §6.11).

## Task atual

**0000 — Bootstrap do template de governança** · Status: **✅ Concluída (2026-07-03)**

*(Este preenchimento é o exemplo vivo do formato. A próxima task, criada via `criar-task`, substitui este conteúdo.)*

- **Objetivo:** transformar o scaffold vazio em template base de governança multiagente.
- **Escopo:** git init, roles.md, .mcp.json, 5 agentes, 6 skills de fluxo, 5 skills vendorizadas, docs/, lib.md, state.md, plan.md, CI skeleton, PR template, CLAUDE.md.
- **Fora de escopo:** definição de stack; hooks de enforcement; remote GitHub.
- **Branch:** `main` (exceção de bootstrap — tasks normais usam branch própria, roles.md §6.5)
- **PRD:** nenhum (task anterior às regras; decisão consciente)

## Arquivos

| Arquivo | Planejado | Concluído |
|---|---|---|
| `.gitattributes`, git init | ✅ | ✅ |
| `roles.md`, `.mcp.json` | ✅ | ✅ |
| `.claude/agents/` (5) | ✅ | ✅ |
| `.claude/skills/` fluxo (6) + templates | ✅ | ✅ |
| `.claude/skills/` vendorizadas (5) | ✅ | ✅ |
| `docs/` (3 READMEs + roadmap) | ✅ | ✅ |
| `lib.md`, `state.md`, `plan.md` | ✅ | ✅ |
| `.github/` (ci.yml + PR template), `.gitignore` | ✅ | ✅ |
| `CLAUDE.md` (reescrita) | ✅ | ✅ |

## Dependências envolvidas

`@upstash/context7-mcp` (dev, ver `lib.md`).

## Plano de testes

Não aplicável (sem código de aplicação). Verificação: JSON/YAML válidos, skills/agentes reconhecidos pelo Claude Code, git limpo em 2 commits.

## Pendências

Nenhuma nesta task. Próxima: definir stack (ver `state.md` → próximos passos).

## Riscos

Ver `state.md` (riscos conhecidos).
