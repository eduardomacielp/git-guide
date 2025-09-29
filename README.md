# Guia de Git

Este repositório contém um guia abrangente e progressivo para estudar e consultar rapidamente comandos, conceitos e fluxos de trabalho de Git.

## Arquivos
- `GIT-GUIDE.md`: Guia completo (estudo + referência)
- `README.md`: Visão geral rápida e links úteis

## Objetivo
Ajudar no aprendizado contínuo de Git: começar pelo básico, reforçar mental models e dominar comandos intermediários e avançados (rebase, cherry-pick, bisect, hooks, etc.).

## Sumário do Guia Completo
Principais blocos presentes em `GIT-GUIDE.md`:
1. Conceitos Essenciais
2. Inicialização & Configuração
3. Ciclo Básico de Trabalho
4. Branches
5. Sincronização com Remotos
6. Commits e Padrões (Conventional Commits)
7. Histórico e Inspeção
8. Undo / Recuperação
9. Stash
10. Rebase / Cherry-pick / Squash
11. Tags & Versionamento Semântico
12. Assinatura de Commits
13. Submodules
14. Sparse Checkout
15. Git LFS
16. Bisect (Debug de histórico)
17. Hooks
18. Patches / Diffs Avançados
19. Workflows (pessoal, equipe, fork flow)
20. Limpeza & Otimização
21. Checklist de Pull Request
22. Resumo Ultrarrápido

## Uso Rápido
Clone ou adicione este repositório como favorito para consulta:
```bash
git clone https://github.com/eduardomacielp/git-guide.git
cd git-guide
open GIT-GUIDE.md # (ou abra no VSCode)
```

## Sugestão de Estudo
1. Leia seções 1–5 e pratique em um repositório de testes.
2. Introduza rebase e cherry-pick em outro ciclo.
3. Só depois avance para submodules, LFS e hooks.
4. Use o checklist antes de cada Pull Request real.

## Alias Recomendado
Adicione ao `~/.gitconfig`:
```ini
[alias]
  lg = log --oneline --graph --decorate --all
```
Depois use:
```bash
git lg
```

## Contribuições
Sugestões e melhorias são bem-vindas via Pull Request ou Issue.

## Licença
(Sem licença definida ainda. Se desejar, podemos adicionar MIT em um próximo commit.)

---
Aproveite! Abra o `GIT-GUIDE.md` para o conteúdo completo.