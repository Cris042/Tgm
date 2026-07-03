# Roadmap

Visão geral das entregas do projeto. Cada item vira uma ou mais tasks pequenas via skill `criar-task` (fluxo completo em `roles.md` §2).

## Visão

Template base reutilizável de governança multiagente. Próximo marco: definir a stack e a primeira aplicação construída sobre o template.

## Itens

| # | Item | Prioridade | Status | Riscos/Dependências | Tasks |
|---|------|-----------|--------|---------------------|-------|
| 1 | Template de governança multiagente (agentes, skills, arquivos de controle, CI skeleton) | alta | ✅ concluído (2026-07-03) | — | bootstrap (pré-governança) |
| 2 | Definição da stack do projeto (linguagem, framework, banco) | alta | pendente | decisão do usuário; possíveis ADRs | — |
| 3 | Primeira funcionalidade sobre o template | média | pendente | depende do item 2 | — |

## Como usar

1. Escolha o item de maior prioridade com dependências resolvidas.
2. Rode `criar-task` para quebrá-lo em tasks pequenas.
3. Siga o fluxo: task → PRD → implementação → auditoria → push → PR → CI/CD.
