# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Governança

Este projeto segue governança multiagente. **`roles.md` é a fonte da verdade** de todas as regras — leia-o antes de qualquer trabalho. Agentes em `.claude/agents/`, skills do fluxo em `.claude/skills/`.

Fluxo padrão: `roadmap → task → PRD → implementação → auditoria → push → PR → CI/CD`.

## Invariantes (nunca violar, mesmo sem ler roles.md)

1. **Nenhuma implementação sem PRD** (`criar-prd`); nenhuma task sem branch própria e escopo ≤ 30 arquivos (`criar-task`).
2. **Nenhum push sem auditoria APROVADA** (skill `auditoria`).
3. **ADR só com autorização explícita do usuário** (`criar-adr`).
4. Toda dependência nova registrada em `lib.md` antes de usar; dúvida sobre lib/framework/versão → consultar **Context7**, nunca presumir.
5. Manter `plan.md` atualizado durante a task e `state.md` ao concluir; ao fim de cada task, registrar a sessão no vault Obsidian (`/obsidian-log` + `/obsidian-decide`, roles.md §6.13).

> Nota: `plan.md` na raiz é o plano da task corrente **do projeto** — não confundir com o plan mode do Claude Code.

## Scaffold atual (placeholder)

O template é **stack-agnóstico**; o código presente é um scaffold IntelliJ Maven **Java 25** descartável (`org.example.Main` usa JEP 512: `static void main()` sem args e `java.lang.IO.println` — exige JDK 25+).

- Executar: `java src/main/java/org/example/Main.java` (single-file source launch; funciona sem Maven).
- No WSL há JDK 25 (Corretto/SDKMAN), mas **não há `mvn` no PATH nem wrapper** — o build Maven é feito pelo IntelliJ no Windows. Com Maven disponível: `mvn compile`.
- `pom.xml` não tem dependências nem plugins; `src/test/java` está vazio — testes exigem adicionar framework ao `pom.xml` primeiro (registrar em `lib.md`).
- Quando a stack for definida (roadmap item 2), este scaffold pode ser substituído.
