# state.md — Estado Atual do Projeto

Atualizado ao final de cada task e antes de cada PR (regras em `roles.md` §6.11).

## Estado atual

Template de governança multiagente implantado. Projeto aguardando descoberta (`iniciar-projeto`, roadmap item 2), que definirá a stack. O scaffold Java foi removido em 2026-07-03 — resta o `pom.xml` placeholder e `src/` vazio.

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
- 2026-07-03 — **Descoberta de projeto obrigatória** (usuário): todo projeto abre com a skill `iniciar-projeto` — entrevista profunda (blocos A–H), análise dos 5 agentes, rodada de confronto de trade-offs; gera `doc.md` (mini-UML), `lib.md` e `docs/roadmap.md` iniciais — regra §6.15; fluxo agora tem etapa 0 (descoberta).
- 2026-07-03 — **Boas práticas de SQL obrigatórias em migrations** (usuário): FK nova sempre indexada, índices pelos padrões de acesso do PRD, `EXPLAIN` sem full scan não justificado, zero-downtime com tráfego — referência `boas-praticas-sql.md` na skill `criar-migration` + regra §6.10.4.

## Pendências técnicas

- Definir stack (linguagem, framework, banco) via descoberta — gerará os primeiros ADRs.
- Preencher os steps reais do `.github/workflows/ci.yml` quando a stack existir.

## Riscos conhecidos

- Regras de governança dependem de disciplina convencional (sem enforcement técnico por hooks ainda).
- Repo em `/mnt/c` (WSL): git mais lento; `core.filemode=false` configurado.

## Próximos passos

1. Rodar a descoberta do primeiro projeto real via `iniciar-projeto` (gera `doc.md`, `lib.md` e `roadmap.md` — cobre a definição de stack do roadmap item 2).
2. Criar a primeira task real via `criar-task`.

## Histórico resumido

| Data | Evento |
|------|--------|
| 2026-07-03 | Bootstrap: git init, roles.md, 5 agentes, 6 skills de fluxo, 5 skills vendorizadas, docs/, arquivos de controle, CI skeleton, CLAUDE.md reescrito. Vault Obsidian integrado (nota [[Tllm]] criada). |
| 2026-07-03 | Análise de lacunas: +5 skills vendorizadas do ECC. Refinamento multiagente adicionado ao fluxo (skill `refinar-task`, regra §6.14). |
| 2026-07-03 | Descoberta de projeto adicionada como etapa 0 do fluxo (skill `iniciar-projeto` + banco de perguntas + template do `doc.md`, regra §6.15). |
| 2026-07-03 | Skill `criar-migration` enriquecida com boas práticas de SQL (`boas-praticas-sql.md`: índices, anti-full-scan, zero-downtime) — regra §6.10.4. |
| 2026-07-03 | Scaffold Java removido pelo usuário (resta `pom.xml` placeholder). Ajustes manuais nos agentes qa (e2e, idempotência) e backend-dev (sem `jpa-patterns`). Remote GitHub criado (`mclovin137/Tllm`, privado) e primeiro push. |
