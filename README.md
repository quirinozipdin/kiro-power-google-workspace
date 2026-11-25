# kiro-power-google-workspace

Power do Kiro que liga o Google Workspace (Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks,
Contacts e Meet) com leitura e escrita. Usa o servidor MCP
[`guinacio/mcp-google-workspace`](https://github.com/guinacio/mcp-google-workspace) (MIT).

## Estrutura
- `POWER.md`: metadados e instruções de onboarding.
- `mcp.json`: sobe o servidor via `uvx`, direto do GitHub.
- `steering/`: regras de uso e diagnóstico.

## Pré-requisitos
- [`uv`](https://docs.astral.sh/uv/getting-started/installation/)
- Conta Google Workspace corporativa
- Um `credentials.json` (client OAuth do Google Cloud), criado como abaixo

## 1. Criar o client OAuth
Quem tem permissão no Google Cloud da organização faz uma vez. Todos os usuários podem compartilhar o
mesmo client; cada um consente com a própria conta.

1. No [Google Cloud Console](https://console.cloud.google.com/), crie ou escolha um projeto da organização.
2. Em **APIs e serviços > Biblioteca**, ative: Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms,
   Tasks, People e **Google Meet REST API**.
3. Em **Google Auth Platform > Branding/Público**, defina o público como **Interno**. Isso limita o app
   à organização e dispensa a verificação do Google.
4. Em **Google Auth Platform > Clients**, crie um client do tipo **Desktop app** e marque
   **Use this client for an AI-powered agent**.
5. Baixe o JSON.

## 2. Instalar o credentials.json
```bash
mkdir -p ~/.kiro/google-workspace
mv ~/Downloads/client_secret_*.json ~/.kiro/google-workspace/credentials.json
```
Nunca commite esse arquivo. O `.gitignore` já o bloqueia.

## 3. Instalar o power
No Kiro: **Powers > Add power from GitHub** e informe a URL deste repositório. Reinicie o Kiro.

## 4. Conectar
Peça ao Kiro "conecte meu Google Workspace". Abra a URL de consentimento e entre com a conta
corporativa. O token fica criptografado, com a chave no Keychain do macOS.

## Configuração
Variáveis em `mcp.json`:

| Variável | Valor | Efeito |
|---|---|---|
| `MCP_TOOL_TIER` | `core` | ~82 tools. `extended` adiciona batch update raw e filtros do Gmail. |
| `ENABLE_MEET` | `true` | Liga as tools de Meet (exige a Meet API ativa). |
| `ENABLE_CHAT`, `ENABLE_KEEP`, `ENABLE_APPS_DASHBOARD` | `false` | Desligados. |
| `MCP_CREDENTIALS_DIR` | `${HOME}/.kiro/google-workspace` | Pasta do `credentials.json`. |

## Segurança
- Envio de e-mail, compartilhamento e exclusão permanente pedem confirmação.
- Não coloque `commit_workspace_action` em `autoApprove`.
- O servidor roda a partir da branch `main` do GitHub. Para travar uma versão, troque a URL em
  `mcp.json` por `git+https://github.com/guinacio/mcp-google-workspace@<tag-ou-commit>`.

## Mensagem para o admin de TI
> Preciso de um OAuth client no projeto Google Cloud da Zipdin para um power de Google Workspace no
> Kiro. Tipo Desktop app, marcado "Use this client for an AI-powered agent", com as APIs Gmail,
> Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, People e Meet ativas e consent screen Interna.
> Se o Admin Console restringir apps de terceiros, preciso que o client seja liberado em Controles de
> API. Pode me enviar o JSON do client?
