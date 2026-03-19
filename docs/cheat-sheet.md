# Configuração Inicial (OBRIGATÓRIO)
Execute uma única vez para ativar as travas de segurança:


```Bash
# Instala as ferramentas de lint e controle
pip install pre-commit gitlint

# Ativa os ganchos de segurança no seu Git local
pre-commit install
pre-commit install --hook-type commit-msg
pre-commit install --hook-type pre-push
```

Ou

```Bash
pip install pre-commit gitlint && pre-commit install --hook-type commit-msg --hook-type pre-push && pre-commit install
```

## Fluxo Diário de Trabalho

<details>
  <summary>Fluxograma desenvolvimento</summary>

![alt text](<Development Task Workflow-2026-03-19-023018.png>)

</details>


1. **Iniciar Tarefa:**
    - *Feature*: `git checkout dev && git pull origin dev && git checkout -b feature/nome-da-task`

    - *Bug Fix*: `git checkout main && git pull origin main && git checkout -b fix/nome-do-bug`

2. **Antes de Commitar:**
```Bash
make lint-fix  # Limpa o código automaticamente
make lint      # Valida se está tudo OK
```

3. **Commits (Padrão Semântico):**
    - `feat: descrição` (Nova funcionalidade)
    - `fix: descrição` (Correção de bug)

4. **Enviar para o GitHub:**

```Bash
git push origin nome-da-sua-branch
# Crie o Pull Request no GitHub (Destino: dev para feats, main para fixes)
```

### Sincronização (Após Merge de Fix na Main)
Se um **Fix** entrou na `main`, a `dev` precisa ser atualizada imediatamente:

```Bash
make sync-dev
# (Esse comando faz o checkout, pull, merge e push por você).
```

### 🚫 Regras de Ouro (O Terminal vai te bloquear)
- **NÃO** dê push direto na `main` ou `dev`.
- **NÃO** ignore o Lint (o push falhará).
- **NÃO** use mensagens de commit genéricas (o commit falhará).


<details>
  <summary>Comandos Fluxograma</summary>

```
graph TD
    A[🚀 Início da Tarefa] --> B{É Bug Fix urgente?}
    
    B -- Sim --> C[Branch a partir da main]
    B -- Não --> D[Branch a partir da dev]
    
    C --> E[Desenvolvimento da Atividade]
    D --> E
    
    E --> F[Commits Semânticos]
    F --> G{Finalizou o Desenvolvimento?}
    
    G -- Não --> E
    G -- Sim --> TT{Destino do PR?}
    TT -- Fix --> UU[PR para 'main']
    TT -- Feature --> VV[PR para 'dev']

    UU -- Execute o comando -->  ZZ[make ready-to-main]
    VV -- Execute o comando -->  XXX[make ready-to-dev]

    ZZ --> I{Sucesso nos comandos?}
    XXX --> I
    I -- Não --> J[❌ Corrija os erros apontados!]
    J --> E
    
    I -- Sim --> S[Push para Origin]
    
    S --> T{Destino do PR?}
    T -- Fix --> U[PR para 'main']
    T -- Feature --> V[PR para 'dev']
    
    U --> X[PR Mergeado na 'main']
    V --> XX[PR Mergeado na 'dev']
    
    XX --> Z[✅ Tarefa Finalizada]
    
    %% Ciclo de Sincronização
    X --> SYNC[🔄 Manter ambiente atualizado]
    SYNC --> CMD[Rode: make sync-dev]
    CMD --> Z
```
</details>

