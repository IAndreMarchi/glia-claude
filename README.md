# Glia para o Claude Code

Plugin que conecta o Claude Code à Glia: ele lista, executa, comenta e move suas tarefas em seu nome, sem abrir o navegador.

## Instalar

No Claude Code:

```
/plugin marketplace add IAndreMarchi/glia-claude
/plugin install glia@glia-claude
```

Depois, na conversa: **"conecta na Glia"**. O navegador abre uma vez para você entrar com o Google; o Claude pergunta qual workspace usar e pronto.

Pré-requisito: Node 20 ou mais novo (o plugin roda `node`).

## Atualizar

`/plugin marketplace update glia-claude` — ou espere: o Claude Code confere atualizações ao abrir.

Versão 0.3.0. Gerado a partir do repositório da Glia (`npm run mcp:plugin`); não edite aqui.
