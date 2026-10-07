# setup

Setup pessoal de IA e VS Code, usado como template: copie os arquivos para qualquer projeto.

| Caminho | Para quê | Lido por |
|---|---|---|
| `.claude/skills/` | Skills (`<nome>/SKILL.md`) | Claude Code e GitHub Copilot (VS Code) |
| `AGENTS.md` | Instruções globais (PT-BR, Context7, Ponytail) | Copilot; Claude Code via `CLAUDE.md` |
| `CLAUDE.md` | Apenas `@AGENTS.md` | Claude Code |
| `.mcp.json` | Servidores MCP (chave `mcpServers`) | Claude Code |
| `.vscode/mcp.json` | Os mesmos MCPs (chave `servers`) | Copilot / VS Code |
| `.vscode/settings.json` | Configurações do workspace | VS Code |
| `.vscode/extensions.json` | Extensões recomendadas | VS Code |
| `skills-lock.json` | Só histórico: origem de cada skill | — |

## Usar em um projeto

```powershell
$dest = 'C:\caminho\do\projeto'
Copy-Item .claude, .vscode, AGENTS.md, CLAUDE.md, .mcp.json -Destination $dest -Recurse -Force
```

Copie só o que precisar (ex.: apenas as skills de `.claude/skills/<nome>`).

## Manutenção

- **Skills:** edite direto em `.claude/skills/`. Uma única cópia atende os dois agentes, sem symlinks.
- **MCPs:** os schemas do VS Code (`servers`) e do Claude Code (`mcpServers`) são incompatíveis; ao alterar um, altere o outro.
- **Segredos:** nunca commitar chaves. `.vscode/mcp.json` pede a `CONTEXT7_API_KEY` por prompt; `.mcp.json` lê `CONTEXT7_API_KEY`, `ADO_ORG` e `ADO_DOMAIN` de variáveis de ambiente.
