# lib.md — Registro de Dependências

Toda dependência do projeto é registrada aqui **antes** de entrar, com justificativa (regras em `roles.md` §6.9). Nenhuma dependência "de carona".

## Dependências de runtime

| Nome | Versão | Finalidade | Onde é usada | Justificativa | Alternativas consideradas | Riscos | CVEs conhecidas | Última validação | Docs |
|------|--------|-----------|--------------|---------------|---------------------------|--------|-----------------|------------------|------|
| — | | *nenhuma ainda — o scaffold não tem dependências* | | | | | | | |

## Ferramentas de desenvolvimento

| Nome | Versão | Finalidade | Onde é usada | Justificativa | Alternativas consideradas | Riscos | CVEs conhecidas | Última validação | Docs |
|------|--------|-----------|--------------|---------------|---------------------------|--------|-----------------|------------------|------|
| @upstash/context7-mcp | latest (via npx) | servidor MCP de documentação atualizada de bibliotecas | `.mcp.json` (sessões Claude Code) | reduz decisões baseadas em docs desatualizadas (roles.md §6.12) | consulta manual a docs (mais lenta, sujeita a versão errada) | execução via npx baixa pacote na 1ª execução (exige rede) | nenhuma conhecida | 2026-07-03 | https://github.com/upstash/context7 |

## Skills vendorizadas (não são dependências de código)

Vendorizadas de [affaan-m/ECC](https://github.com/affaan-m/ECC) (MIT) em 2026-07-03, em `.claude/skills/`: `tdd-workflow`, `e2e-testing`, `github-ops`, `git-workflow`, `architecture-decision-records`, `coding-standards`, `api-design`, `error-handling`, `deployment-patterns`, `security-scan`. Atualização: re-baixar do repositório de origem e reaplicar o rodapé de crédito.
