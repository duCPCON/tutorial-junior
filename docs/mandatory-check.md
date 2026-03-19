# 🛠️ Guia de Contribuição e Fluxo Git (tutorial-junior)

Este guia é **obrigatório** para todos os desenvolvedores. O objetivo é garantir que o código suba limpo, as versões sejam geradas automaticamente e a branch `dev` nunca fique defasada em relação à `main`.

## 1. Configuração Inicial (Uma única vez)
Para que as travas automáticas funcionem na sua máquina, você precisa rodar estes comandos:

```bash
# Instala as ferramentas de lint e controle
pip install pre-commit gitlint

# Ativa os ganchos de segurança no seu Git local
pre-commit install
pre-commit install --hook-type commit-msg
pre-commit install --hook-type pre-push
```

> Nota: Se você não rodar isso, o seu push será rejeitado pelo servidor ou você quebrará a CI.

## 2. Regras de Ouro
- Não enviar o Push Direto
- As branches `main` e `dev` são protegidas. Tentativas de `git push` direto para elas resultarão em erro no terminal. Use sempre **Pull Requests**.

### Commits Semânticos
Nossa automação de Changelog depende do padrão **Conventional Commits**. Use a extensão do VS Code ou siga o padrão:

- **feat**: para novas funcionalidades.
- **fix**: para correções de bugs.
- **docs**: para mudanças em documentação.
- **etc...**

### Lint e Testes
Antes de enviar qualquer código, rode os comandos de limpeza. Se o linter apontar erros, o Git não permitirá o envio.

```Bash
make lint-fix  # Tenta corrigir erros automaticamente
make lint      # Valida se está tudo nos conformes
```

## 3. Sincronização
Sempre que um Bug Fix (PR para a `main`) for finalizado, a branch `dev` fica "atrás" da `main`. Para evitar conflitos gigantescos no futuro, rode o comando de sincronização:

```Bash
make sync-dev
```

O que este comando faz por você?
1. Atualiza sua main local.
2. Vai para a dev e a atualiza.
3. Faz o merge da main na dev.
4. Sobe as atualizações para o GitHub.

### Problemas Comuns

**"O Git bloqueou meu commit!"**

Verifique a mensagem de erro. Provavelmente você esqueceu de rodar o `make lint` ou sua mensagem de **commit** não segue o padrão semântico.

**"O Git bloqueou meu push!"**

Você provavelmente está tentando dar `push` direto na `main` ou `dev`. Mude para uma branch de tarefa (feature/...) e abra um `PR (PULL REQUEST)`.
