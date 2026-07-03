# roles.md — Governança Técnica do Projeto

> **Fonte da verdade** de todas as regras, agentes, skills e fluxos deste projeto.
> Cada regra está escrita uma única vez, aqui. Agentes, skills e o CLAUDE.md apenas referenciam este arquivo.
> Sempre que uma nova regra estrutural for definida, este arquivo DEVE ser atualizado.

---

## 1. Visão geral

Este projeto segue uma governança **multiagente**: agentes especializados colaboram para garantir padronização técnica, qualidade, segurança, observabilidade, manutenibilidade, baixo acoplamento e rastreabilidade completa do ciclo de desenvolvimento.

Toda decisão técnica relevante deve considerar **benefícios, riscos, trade-offs, impacto no negócio, custo operacional, manutenção futura e complexidade adicionada**. O objetivo é sempre **minimizar os trade-offs negativos** e evitar soluções desnecessariamente complexas (anti-overengineering).

**Importante — como os agentes atuam:** os subagentes do Claude Code são **consultivos**: analisam e retornam recomendações estruturadas. Quem executa o fluxo (edições, skills, git) é a sessão principal, seguindo as recomendações dos agentes. Não existe "agente que faz push".

---

## 2. Fluxo padrão de desenvolvimento

```
roadmap → task → PRD → implementação → auditoria → push → PR → CI/CD
```

| Etapa | Produz | Consome | Regra-chave |
|---|---|---|---|
| 1. Roadmap | `docs/roadmap.md` | objetivos do projeto | épicos, prioridades, riscos, ordem sugerida |
| 2. Task | `docs/tasks/NNNN-*.md` + branch | roadmap | escopo pequeno, máx. 30 arquivos (§6.3) |
| 3. PRD | `docs/prd/NNNN-*.md` | task | nenhuma implementação sem PRD (§6.2) |
| 4. Implementação | código + testes | PRD, ADRs | seguir padrões; atualizar `plan.md` (§6.11) |
| 5. Auditoria | veredito APROVADO/REPROVADO | diff da branch, PRD, ADRs | obrigatória antes do push (§6.4) |
| 6. Push | branch remota | auditoria aprovada | **nenhum push sem auditoria** |
| 7. PR | Pull Request | template de PR | rastreável até task e PRD (§6.5) |
| 8. CI/CD | pipeline verde | `.github/workflows/ci.yml` | executa todos os testes definidos |

---

## 3. Agentes

Definidos em `.claude/agents/`. Invocação: pedir explicitamente ("consulte o agente arquiteto sobre X") ou deixar o Claude delegar quando a description casar.

| Agente | Arquivo | Responsabilidade central | Quando acionar |
|---|---|---|---|
| **Arquiteto de Software** | `arquiteto.md` | ADRs, padrões, trade-offs, volumetria, tecnologias, anti-overengineering | decisões estruturais, escolha de tecnologia, antes de qualquer ADR |
| **SRE / DevOps** | `sre-devops.md` | docker-compose, ambiente reproduzível, observabilidade, gargalos | infra local, métricas/logs/traces, performance, CI |
| **Security Engineer** | `security.md` | segurança da concepção à implementação, CVEs, secrets, authn/authz | novas dependências, endpoints, dados sensíveis, **sempre na auditoria** |
| **QA Engineer** | `qa.md` | estratégia de testes, cobertura mínima, idempotência | plano de testes do PRD, revisão de suíte, **sempre na auditoria** |
| **Backend Developer** | `backend-dev.md` | implementação seguindo ADRs, PRD e diretrizes dos demais agentes | executar a implementação da task |

---

## 4. Skills

### 4.1 Skills do fluxo (deste projeto, em `.claude/skills/`)

| Skill | Propósito | Obrigatória quando |
|---|---|---|
| `criar-task` | quebrar roadmap em tasks pequenas e rastreáveis | iniciar qualquer trabalho novo |
| `criar-prd` | detalhar a task antes de implementar | antes de toda implementação |
| `criar-adr` | registrar decisão arquitetural relevante | decisão estrutural **com autorização do usuário** |
| `criar-migration` | mudança estrutural de banco versionada | toda alteração de schema |
| `auditoria` | gate de qualidade pré-push (13 itens) | **antes de todo push** |
| `fluxo-git` | branches, commits, PR padronizados | todo trabalho com git |

### 4.2 Skills de apoio por agente (externas, já instaladas ou vendorizadas)

| Agente | Skills de apoio |
|---|---|
| Arquiteto | `backend-patterns`, `design-system`, `architecture-decision-records`ᵛ |
| SRE/DevOps | `docker-patterns`, `benchmark`, `postgres-patterns`, `github-ops`ᵛ (CI/releases) |
| Security | `security-review` |
| QA | `tdd-workflow`ᵛ, `e2e-testing`ᵛ, `browser-qa`, `benchmark` |
| Backend Dev | `backend-patterns`, `postgres-patterns`, `jpa-patterns` (se Java), `tdd-workflow`ᵛ, `database-migrations`, `ui-ux-pro-max` (tarefas de UI) |
| fluxo-git (skill) | `git-workflow`ᵛ, `github-ops`ᵛ |

ᵛ = vendorizada neste repositório em `.claude/skills/` a partir de [affaan-m/ECC](https://github.com/affaan-m/ECC) (MIT). As demais estão instaladas em nível de usuário (`~/.claude/skills/`) ou como plugin.

### 4.3 Skills opcionais (instalação manual, se necessário)

Avaliadas e consideradas cobertas ou redundantes hoje; instalar via [mcpmarket.com](https://mcpmarket.com) apenas se surgir necessidade real:

- `gh-issues-auto-fixer` — ciclo automático de issues→fix→PR; o essencial é coberto por `github-ops`.
- `spec-driven-development` — este template já implementa SDD (task→PRD→gates).
- `mp-pdf-data-extractor` — o Claude lê PDFs nativamente (tool Read).
- `mp-sql-copilot` — parcialmente coberta por `postgres-patterns`.

---

## 5. Arquivos de controle

| Arquivo | Conteúdo | Quem atualiza | Quando |
|---|---|---|---|
| `roles.md` | política completa (este arquivo) | sessão principal, com aval do usuário | a cada regra estrutural nova |
| `lib.md` | registro de dependências e versões | quem adiciona dependência | **toda** nova dependência (§6.9) |
| `state.md` | estado atual + histórico recente | sessão principal | fim de cada task e antes do PR |
| `plan.md` | plano vivo da task em andamento | sessão principal durante implementação | continuamente durante a task |
| `docs/roadmap.md` | visão geral das entregas | sessão principal, com aval do usuário | quando prioridades mudarem |

---

## 6. Regras

### 6.1 ADR (Architecture Decision Records)
1. Toda decisão arquitetural **relevante** deve ser registrada em ADR (`docs/adr/`).
2. ADR só é criado com **necessidade real E autorização explícita do usuário**. Agentes recomendam; nunca criam por conta própria.
3. Não criar ADR para decisões triviais.
4. Todo ADR deve deixar claro: motivo, o que foi considerado e descartado, trade-offs e estratégias para minimizá-los.
5. ADRs devem ter escopo claro e listar ADRs relacionados.
6. Critérios de relevância: afeta estrutura, tecnologia, modelo de dados ou contratos entre módulos/sistemas.

### 6.2 PRD (Product Requirements Document)
1. **Toda task deve ter um PRD antes da implementação** (`docs/prd/`).
2. O PRD orienta a implementação e delimita o escopo — nada fora dele sem atualizá-lo primeiro.
3. O PRD indica claramente os arquivos previstos para criação/alteração.
4. Se a implementação divergir do plano, o PRD deve ser atualizado.

### 6.3 Task
1. Escopo pequeno, revisável com clareza.
2. **Máximo de 30 arquivos alterados**; acima disso, quebrar em tasks menores.
3. Cada task tem: branch própria, PRD próprio, critérios de aceite claros.
4. Rastreável em `state.md` e `plan.md`.

### 6.4 Auditoria (gate obrigatório)
1. **Nenhum push antes da auditoria aprovada.** Sem exceções.
2. Executada pela skill `auditoria`, que valida os 13 itens (PRD, ADRs, overengineering, escopo, testes, secrets, logs, lib.md, CVEs, migrations, state.md, plan.md, qualidade).
3. Agentes `security` e `qa` são acionados para os itens dos seus domínios.
4. Veredito REPROVADO bloqueia o push até correção.
5. Hoje o gate é convencional (não há hook técnico). Evolução futura possível: hook PreToolUse bloqueando `git push` sem auditoria.

### 6.5 Git e Pull Request
1. Branches: `feature/NNNN-nome` · `fix/NNNN-nome` · `chore/NNNN-nome` · `refactor/NNNN-nome` (NNNN = id da task).
2. Nunca misturar múltiplas tasks na mesma branch.
3. Sem push sem auditoria; sem PR sem PRD e testes mínimos.
4. PR segue `.github/pull_request_template.md`: resumo, task, PRD, ADRs, arquivos principais, testes executados, riscos, evidências.
5. O CI/CD executa todos os testes após a abertura do PR.

### 6.6 Segurança
1. Secrets nunca em código, commit ou log — usar variáveis de ambiente/secret manager.
2. Logs não podem conter dados sensíveis (PII, tokens, credenciais).
3. Toda dependência nova passa por verificação de CVEs antes de entrar (registrar em `lib.md`).
4. Autenticação, autorização e controle de acesso validados pelo agente `security`.
5. Riscos de segurança avaliados **antes** do push e da abertura do PR.

### 6.7 Testes
1. QA define a cobertura mínima; prioridade para o MVC da aplicação e rotinas críticas.
2. Testes devem ser **idempotentes**, confiáveis e sem dependência de estado compartilhado indevido.
3. Cobrir cenários de erro, borda e fluxos principais — validar comportamento de negócio, não implementação.
4. Suíte simples de executar localmente e no pipeline.

### 6.8 Observabilidade
1. O sistema nasce preparado para observabilidade: logs estruturados, métricas e traces conforme padrões do agente `sre-devops`.
2. Cada dependência da aplicação deve ser monitorável.
3. Rotinas críticas (queries, jobs, integrações, processamento assíncrono) devem expor sinais que permitam identificar gargalos.

### 6.9 Dependências
1. **Toda nova dependência deve ser registrada no `lib.md`** com justificativa — nenhuma entra "de carona".
2. Avaliar: necessidade real, estabilidade, manutenção ativa, CVEs, alternativas.
3. Preferir a biblioteca padrão / recursos nativos quando resolverem o problema.

### 6.10 Migrations
1. Toda alteração estrutural de banco tem migration versionada — nunca alterar schema manualmente.
2. Migration vinculada à task e ao PRD; rollback definido quando aplicável; idempotente quando possível.
3. Validada localmente (docker-compose) ou nos testes antes do push.

### 6.11 Arquivos de controle
1. `plan.md` atualizado **durante** a implementação — reflete o estado real da task.
2. `state.md` atualizado ao **final** de cada task e antes do PR.
3. `roles.md` atualizado a cada regra estrutural nova.

### 6.12 MCP Context7
1. Sempre que houver dúvida sobre biblioteca, framework ou versão, **consultar o Context7** (configurado em `.mcp.json`).
2. Não assumir comportamento de dependência sem validação.
3. Usar para apoiar ADRs, PRDs, planos de implementação e análise de dependências.

### 6.13 Segundo cérebro (vault Obsidian)
1. O vault Obsidian (caminho em `OBSIDIAN_VAULT_PATH` no `~/.claude/settings.json`) é o **segundo cérebro** do ciclo de desenvolvimento: conhecimento destilado das sessões (decisões, aprendizados, contexto de projeto) vive lá, seguindo as regras AI-first do `_CLAUDE.md` do vault.
2. **Ao final de cada task** (junto com a atualização do `state.md`): registrar a sessão no vault (`/obsidian-log`) e as decisões relevantes (`/obsidian-decide`).
3. Conversas que produzirem insight além da task: salvar com `/obsidian-save`.
4. A nota do projeto no vault (`Projects/<nome>.md`) deve refletir o estado real — atualizar `Recent Activity` e `Key Decisions` quando houver mudança relevante.
5. O hook PostCompact já propaga automaticamente resumos de contexto para o vault; os comandos acima cobrem o registro deliberado.

---

## 7. Estrutura de documentação

```
docs/
├── roadmap.md            visão geral das entregas
├── adr/NNNN-titulo-kebab.md
├── prd/NNNN-titulo-kebab.md
└── tasks/NNNN-titulo-kebab.md
```

Numeração sequencial de 4 dígitos por diretório, começando em `0001`. Cada diretório tem um `README.md` com índice. Templates ficam nas pastas das skills correspondentes (`.claude/skills/criar-*/`).

---

## 8. Manutenção deste arquivo

- Este arquivo é a **única** fonte de regras. Não duplicar regras em agentes, skills ou CLAUDE.md — referenciar por seção (ex.: "ver roles.md §6.4").
- Alterações estruturais na governança exigem atualização imediata deste arquivo e aval do usuário.
