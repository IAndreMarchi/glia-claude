---
name: glia
description: Trabalhar nas tarefas da Glia (organizador de projetos da equipe) pelo servidor MCP glia — conectar a conta, listar pendentes de um projeto, entender cada tarefa, executar, marcar subtarefas, comentar e mover no Kanban; registrar ideias como sugestões de melhoria. Use quando o usuário citar a Glia, um projeto/tarefa dela (códigos como IC-25) ou pedir para "conectar na Glia" ou "pegar as tarefas do projeto X".
---

# Glia pelo MCP

As tools do servidor `glia` (os nomes terminam em `__listar_tarefas`, `__entrar`, etc.) operam a Glia **como o usuário logado nesta máquina**: tudo que você fizer aparece lá com o nome dele e notifica os colegas como se ele tivesse feito pela tela. Nada de abrir a Glia no navegador.

## Primeira vez nesta máquina (onboarding)

Quando o usuário pedir para "conectar na Glia", ou quando uma tool responder que não há sessão:

1. Chame **`entrar`**. Ela abre o navegador na página de login e devolve na hora. Diga ao usuário para clicar em **"Entrar com Google"** com a conta da Glia (você não digita credenciais) e avisar quando terminar. Se o navegador não abriu, mostre o endereço que a tool devolveu.
2. Quando ele confirmar, chame **`listar_workspaces`**. Se houver mais de uma e nenhuma marcada como padrão, mostre as opções, pergunte qual usar e fixe com **`usar_workspace`**. Fica salvo; não pergunte de novo.
3. Feche mostrando `listar_projetos` — é a prova de que está tudo ligado.

Sem as tools do servidor `glia` na sessão? O plugin não está instalado: peça ao usuário para rodar `/plugin marketplace add IAndreMarchi/glia-claude` e `/plugin install glia@glia-claude` no Claude Code e reabrir a sessão. Para trocar de conta: `entrar` com `trocar_conta: true`.

## Vocabulário

- **Workspace** = a equipe. **Projeto** tem sigla (`IC`), colunas do Kanban (ex. A Fazer → Em Andamento → Revisão → Concluído) e, às vezes, **fases** de roadmap.
- **Tarefa** tem código público `SIGLA-NÚMERO` (`IC-25`) — cite sempre assim. Tem coluna, prioridade (baixa/média/alta), prazo, responsáveis (vários), **subtarefas** (checklist) e **comentários** (chat da tarefa).
- **Sugestão** = ideia/melhoria no portal do projeto (aba Melhorias), triada pelo time depois. Não é tarefa.

## O roteiro (siga nesta ordem)

1. **Achar o projeto**: `listar_projetos` (nome, sigla, quantas tarefas abertas).
2. **Ver a fila**: `listar_tarefas` com `pendentes: true` (padrão). Mostre a lista com os códigos e confirme por onde começar, a menos que o usuário já tenha dito.
3. **Antes de mexer**: `ver_tarefa` — descrição, subtarefas (com ids), comentários, dependências abertas. É aí que está o que de fato precisa ser feito. Se faltar contexto, pergunte.
4. **Durante o trabalho**: a cada parte concluída, `marcar_subtarefa`. Descobriu trabalho novo? `adicionar_subtarefa` em vez de fazer em silêncio.
5. **Ao terminar**: `comentar_tarefa` com o que foi feito, onde (arquivos, PR, commit) e o que ficou de fora. **Nunca** mova para a coluna de conclusão sem esse comentário — é o registro que a equipe lê. Use `@Nome` para chamar alguém (a pessoa é notificada).
6. **Só então** `mover_tarefa` para a coluna certa (Revisão, Concluído…). Concluir fecha as subtarefas junto. Se a Glia recusar por dependência aberta ("Bloqueada por: …"), diga ao usuário — não force.
7. **Ideias fora do escopo** viram `criar_sugestao` no projeto, não tarefa nova. Trabalho concreto que precisa existir agora vira `criar_tarefa` (informe o código devolvido: "criei a IC-31").

## Referências rápidas

| Quero… | Tool |
|---|---|
| conectar / trocar de conta | `entrar` |
| saber em que workspace estou / quem está nela | `listar_workspaces`, `listar_membros` |
| fixar/trocar a workspace padrão | `usar_workspace` |
| as fases do roadmap | `listar_fases` |
| tarefas de uma coluna, só as minhas, de uma fase | `listar_tarefas` com `coluna`, `minhas`, `fase` |
| mudar título/descrição/prazo/prioridade/tags/fase/responsáveis | `atualizar_tarefa` (só os campos informados mudam) |
| ver o que já foi sugerido | `listar_sugestoes` |

Datas são `AAAA-MM-DD`. Pessoas podem ser referidas por nome, e-mail ou `"eu"`. Tarefas por código (`IC-25`) ou id (aí informe `projeto`).

## Exemplos de pedidos que este fluxo atende

- "Conecta na Glia."
- "Pega as tarefas pendentes do projeto Integração e vai fazendo uma por uma."
- "O que a IC-25 pede? Faz e me avisa quando terminar."
- "Registra na Glia que terminei a parte de testes da IC-12 e manda pra revisão."
- "Anota como sugestão no projeto Portal: validar CPF no front."
