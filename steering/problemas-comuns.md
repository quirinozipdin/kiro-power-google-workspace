# Problemas comuns
- **Servidor não sobe / `uvx` não encontrado**: instale o `uv` e reinicie o Kiro.
- **`credentials.json not found`**: o arquivo precisa estar em `~/.kiro/google-workspace/credentials.json`.
  Se `${HOME}` não for expandido pelo seu cliente, troque `MCP_CREDENTIALS_DIR` no `mcp.json` por um
  caminho absoluto.
- **`access_denied` ou "app bloqueado" no consentimento**: o admin do Workspace precisa liberar o
  client no Admin Console (Segurança > Controle de acesso e de dados > Controles de API).
- **Erro de API desativada (`accessNotConfigured`)**: ative a API no projeto do Google Cloud
  (Gmail, Calendar, Drive, Docs, Sheets, Slides, Forms, Tasks, People, Meet).
- **Meet sem tools**: confirme `ENABLE_MEET=true` e a Meet API ativa no mesmo projeto.
- **Trocou de client OAuth**: substitua o `credentials.json`, chame `disconnect_google_workspace` e
  conecte de novo.
- **Mudou escopos / tier e deu erro de permissão**: reconecte a conta para renovar o consentimento.
