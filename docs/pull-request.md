# Fluxo de Trabalho e Pull Requests (tutorial-junior.git)

Este guia define o padrão de contribuição para garantir a organização do código e a automação de releases.

---

## 1. Estrutura de Branches

* **`main`**: Apenas para criação de **fixups** (correções diretas).
* **`dev`**: Base para **qualquer branch de desenvolvimento** (features, melhorias, etc).

---

## 2. Passo a Passo: Do Código ao Pull Request

### Criando a Branch
Sempre inicie sua tarefa a partir da branch `dev`:

```bash
git checkout dev
git pull origin dev
git checkout -b nome-da-sua-branch
```

### Alterações e Commits
Realize suas modificações no código. Para os commits, utilize a extensão **Conventional Commits no VS Code**.

> Nota: Certifique-se de selecionar o tipo correto (feat, fix, etc.) na interface da extensão para manter o padrão semântico.

### Envio e Pull Request (PR)

1. Envie sua branch para o GitHub:

```Bash
git push origin nome-da-sua-branch
```

2. No GitHub, abra o **Pull Request** apontando para a branch de destino correta (`dev` para desenvolvimento ou `main` para fixups).

3. **Modelos de PR:** O repositório possui templates de descrição. O preenchimento detalhado não é obrigatório, mas ajuda na organização.

4. **Análise:** Você pode revisar todas as suas alterações na aba *Files Changed* antes de finalizar.

5. **Review:** O code review por outras pessoas **não é obrigatório** neste projeto.

## Automação de Changelog

Seguir este processo rigorosamente (especialmente os commits semânticos) é o que permite a **criação do changelog automático através de nossa CI**. Sem esse padrão, as versões do sistema não serão geradas corretamente.