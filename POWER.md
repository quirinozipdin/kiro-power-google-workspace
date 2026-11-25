---
name: "google-workspace-completo"
displayName: "Google Workspace (leitura e escrita)"
description: "Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, Contacts e Meet com a sua conta Google corporativa. Leitura e escrita, com confirmação antes de enviar e-mail, compartilhar ou excluir."
keywords: ["google", "gmail", "email", "calendar", "agenda", "drive", "docs", "sheets", "planilha", "slides", "meet", "forms", "tasks", "workspace"]
author: "Zipdin"
---
# Google Workspace (leitura e escrita)

## Overview
Servidor MCP [`guinacio/mcp-google-workspace`](https://github.com/guinacio/mcp-google-workspace)
(licença MIT) rodando local via `uvx`, direto do GitHub. Cobre Gmail, Calendar, Drive, Docs, Sheets,
Slides, Forms, Tasks, Contacts e Meet. Chat, Keep e o dashboard ficam desligados.

Cada pessoa autoriza com a própria conta. O token fica criptografado na máquina, com a chave no
Keychain do macOS (Credential Manager no Windows). O client OAuth (`credentials.json`) fica fora do
repositório, em `~/.kiro/google-workspace/`.

## Onboarding
1. Pré-requisito: [`uv`](https://docs.astral.sh/uv/getting-started/installation/) instalado.
2. Obtenha o `credentials.json` do client OAuth (Desktop app, marcado como "AI-powered agent").
   Passo a passo para criar ou pedir ao admin: `README.md` do repositório.
3. Salve em `~/.kiro/google-workspace/credentials.json`.
4. Instale o power no Kiro (Powers > Add power from GitHub) e reinicie o Kiro.
5. Primeira chamada: peça "conecte meu Google Workspace" ou "liste meus próximos eventos". O servidor
   devolve uma URL de consentimento. Abra e entre com a conta corporativa.

## Available Steering Files
- **regras-uso** - Regras de segurança para escrita; ler antes de enviar e-mail, editar ou excluir.
- **problemas-comuns** - Diagnóstico quando o servidor não sobe ou o Google recusa.

## Uso
- Tier `core`: cerca de 82 tools do dia a dia, mais as de Meet.
- Ações de consequência (enviar e-mail, compartilhar, excluir permanente) pedem confirmação. Em
  clientes sem esse suporte, o servidor usa `prepare_workspace_action` e `commit_workspace_action`.
  Nunca coloque `commit_workspace_action` em `autoApprove`: é o ponto onde a pessoa aprova.
- Para chamar tools raw de batch update ou configurar filtros do Gmail, mude `MCP_TOOL_TIER` para
  `extended` no `mcp.json`.
