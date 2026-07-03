# state.md — Estado Atual do Projeto

Atualizado ao final de cada task e antes de cada PR (regras em `roles.md` §6.11).

## Estado atual

Template de governança multiagente implantado. Projeto aguardando definição de stack (roadmap item 2). O scaffold Java 25 existente é placeholder e pode ser substituído quando a stack for decidida.

- **Última task concluída:** 0000 — bootstrap do template de governança (2026-07-03; anterior às próprias regras — sem PRD retroativo, por decisão consciente de evitar burocracia retroativa)
- **Task atual:** nenhuma
- **Branch atual:** `main`
- **PRD atual:** nenhum
- **ADRs ativos:** nenhum

## Últimas decisões relevantes

- 2026-07-03 — Template stack-agnóstico, artefatos em PT-BR (usuário).
- 2026-07-03 — Skills externas: 8 já instaladas em nível de usuário; 5 vendorizadas do ECC (MIT); 4 marcadas opcionais (roles.md §4.3).
- 2026-07-03 — Vault Obsidian (`Documents/SecondBrain`) adotado como segundo cérebro do ciclo de dev (roles.md §6.13).
- 2026-07-03 — Auditoria pré-push é convencional por ora; hook técnico registrado como evolução futura (roles.md §6.4.5).
- 2026-07-03 — Análise de lacunas de skills: +5 vendorizadas do ECC (`coding-standards`, `api-design`, `error-handling`, `deployment-patterns`, `security-scan`); observabilidade fica por plataforma, adiada até a stack (roles.md §4.3).
- 2026-07-03 — **Refinamento multiagente obrigatório** (usuário): toda task passa pelos 5 agentes, que debatem e convergem antes do PRD — skill `refinar-task` + regra §6.14; fluxo atualizado para 9 etapas.

## Pendências técnicas

- Definir stack (linguagem, framework, banco) — gerará os primeiros ADRs.
- Criar remote no GitHub e fazer o primeiro push (CI hoje só validado por lint local).
- Preencher os steps reais do `.github/workflows/ci.yml` quando a stack existir.

## Riscos conhecidos

- Regras de governança dependem de disciplina convencional (sem enforcement técnico por hooks ainda).
- Repo em `/mnt/c` (WSL): git mais lento; `core.filemode=false` configurado.

## Próximos passos

1. Definir a stack (roadmap item 2) com o agente `arquiteto` — possíveis ADRs 0001+.
2. Criar a primeira task real via `criar-task`.

## Histórico resumido

| Data | Evento |
|------|--------|
| 2026-07-03 | Bootstrap: git init, roles.md, 5 agentes, 6 skills de fluxo, 5 skills vendorizadas, docs/, arquivos de controle, CI skeleton, CLAUDE.md reescrito. Vault Obsidian integrado (nota [[Tllm]] criada). |
| 2026-07-03 | Análise de lacunas: +5 skills vendorizadas do ECC. Refinamento multiagente adicionado ao fluxo (skill `refinar-task`, regra §6.14). |
