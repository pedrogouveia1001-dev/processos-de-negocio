# Modelagem TO-BE — Processo Automatizado de CI/CD

## AS-IS — Processo antigo (manual)

```mermaid
flowchart TD
    A([Início]) --> B[Desenvolvedor altera o código]
    B --> C[Testes manuais]
    C --> D{Teste aprovado?}
    D -- Não --> E[Corrigir o código]
    E --> C
    D -- Sim --> F[Publicação manual]
    F --> G[Conferir site publicado]
    G --> H([Fim])
```

## TO-BE — Processo automatizado

```mermaid
flowchart TD
    A([Início]) --> B[Desenvolvedor altera o código]
    B --> C[Commit e Push no GitHub]
    C --> D[GitHub Actions inicia automaticamente]
    D --> E[CI - Verificar index.html]
    E --> F[Regra 1: index.html existe]
    F --> G[Regra 2: possui tag title]
    G --> H[Regra 3: arquivo termina com /html]
    H --> I{Todas as verificações passaram?}

    I -- Não --> J[Deploy bloqueado]
    J --> K[Site antigo continua no ar]
    K --> L[Desenvolvedor corrige o código]
    L --> C

    I -- Sim --> M[CD - Liberar publicação]
    M --> N[GitHub Actions realiza o deploy]
    N --> O[GitHub Pages publica a nova versão]
    O --> P([Fim])
```

## Melhoria do processo

No processo TO-BE, a conferência deixa de depender somente de testes manuais. A cada envio para a branch main, o GitHub Actions executa automaticamente as verificações do arquivo. Se alguma regra falhar, a publicação é bloqueada. Se todas as regras forem aprovadas, o processo segue para o deploy no GitHub Pages.

**Resultado:** menos risco de erro humano, bloqueio automático de versões incorretas, publicação mais rápida e maior rastreabilidade dos commits.
