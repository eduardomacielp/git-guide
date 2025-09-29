# 🧠 Guia Definitivo de Git (Estudo + Consulta Rápida)

> Use este arquivo como referência diária. Leia em blocos e pratique logo após cada seção.

---

## 🔌 0. Conceitos Essenciais

| Conceito | Explicação rápida |
|----------|-------------------|
| Repositório (repo) | Pasta versionada pelo Git |
| Commit | “Foto” do estado dos arquivos rastreados |
| Branch | Linha paralela de desenvolvimento |
| Merge | Junta o histórico de uma branch em outra |
| Rebase | Reaplica commits “por cima” de outro histórico |
| HEAD | Ponteiro para o commit atual |
| Origin | Nome padrão do remoto principal |
| Staging Area | Área intermediária entre modificações e commit |
| Fork | Cópia de um repo de outra conta pro seu usuário |

---

## 🚀 1. Inicialização & Configuração

```bash
git init
git clone URL.git
git config --global user.name "Seu Nome"
git config --global user.email "seu@email"
git config --global core.editor "code --wait"
git config --list
```

### Ignorando arquivos
```bash
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
```

---

## 📦 2. Ciclo Básico (Working Dir → Staging → Commit)

```bash
git status
git add arquivo.ext
git add .                     # cuidado
git restore arquivo.ext       # descarta alterações não commitadas
git restore --staged arquivo.ext
git commit -m "feat: adiciona X"
git commit -am "fix: ajusta Y"  # só altera rastreados
```

Ajustar último commit (mensagem ou incluir algo esquecido):
```bash
git commit --amend -m "feat: mensagem melhor"
```

---

## 🌿 3. Branches

```bash
git branch
git branch -M main
git checkout -b feature/login
git switch feature/login
git switch -c hotfix/alerta
git merge feature/login
git branch -d feature/login
git branch -D feature/login    # força
```

---

## 🔄 4. Sincronização com Remotos

```bash
git remote -v
git remote add origin URL.git
git remote set-url origin NOVO_URL.git
git fetch origin
git pull origin main
git pull origin main --rebase
git push -u origin main
git push
git push origin :nome-da-branch   # deleta branch remota
```

---

## 🧪 5. Commits: Padrão e Boas Práticas (Conventional Commits)

Formato:
```
<tipo>(escopo opcional): descrição curta

[corpo opcional]
[rodapé: refs, BREAKING CHANGE, etc.]
```

Tipos:
feat, fix, docs, style, refactor, test, chore, perf, build, ci, revert

Exemplo:
```
feat(auth): adiciona fluxo de login com JWT

Implementa middleware de validação e rota de refresh.

Refs #42
```

---

## 🧭 6. Explorando Histórico

```bash
git log --oneline --graph --decorate --all
git log -p arquivo.ext
git log --author="Seu Nome"
git log --since="2 weeks ago"
git show <hash>
git diff
git diff --staged
git blame arquivo.ext
```

Alias:
```
[alias]
  lg = log --oneline --graph --decorate --all
```

---

## 🕹️ 7. Undo / Recuperação

| Situação | Comando |
|----------|---------|
| Descartar alteração local | `git restore arquivo` |
| Tirar do staging | `git restore --staged arquivo` |
| Desfazer via novo commit | `git revert <hash>` |
| Mover HEAD mantendo staging/mudanças | `git reset --soft <hash>` |
| Reset staging mantendo working dir | `git reset --mixed <hash>` |
| Perder tudo até commit (perigoso) | `git reset --hard <hash>` |

Recuperar referências:
```bash
git reflog
```

---

## 📦 8. Stash

```bash
git stash push -m "ajustes parciais"
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}
git stash pop
git stash drop stash@{0}
git stash clear
```

---

## 🍒 9. Rebase, Squash e Cherry-pick

```bash
git rebase main
git rebase -i HEAD~5
git cherry-pick <hash>
git cherry-pick <h1> <h2>
```

Conflito:
```bash
# Resolve arquivos
git add resolvidos
git rebase --continue
# ou
git rebase --abort
```

---

## 🏷️ 10. Tags & Releases

```bash
git tag
git tag v1.0.0
git tag -a v1.0.0 -m "Primeira release"
git push origin v1.0.0
git push --tags
git tag -d v1.0.0
git push origin :refs/tags/v1.0.0
```

---

## 🔐 11. Assinando Commits

```bash
git config --global user.signingkey <GPG_KEY_ID>
git config --global commit.gpgsign true
```

---

## 🧩 12. Submodules

```bash
git submodule add URL.git caminho/
git submodule update --init --recursive
git submodule foreach git pull
```

---

## 📁 13. Sparse Checkout

```bash
git clone --filter=blob:none --no-checkout URL.git
cd repo
git sparse-checkout init --cone
git sparse-checkout set caminho/desejado
git checkout main
```

---

## 📦 14. Git LFS

```bash
git lfs install
git lfs track "*.psd"
git add .gitattributes
git add arquivo.psd
git commit -m "chore: adiciona LFS"
```

---

## 🩺 15. Bisect (Debug Histórico)

```bash
git bisect start
git bisect bad
git bisect good <hash_bom>
# testando...
git bisect good
git bisect bad
git bisect reset
```

---

## ⚙️ 16. Hooks

`.git/hooks/commit-msg`:
```bash
#!/bin/sh
if ! grep -E '^(feat|fix|chore|docs|style|refactor|test|perf)(\(.+\))?:' "$1"; then
  echo "Mensagem fora do padrão Conventional Commit"
  exit 1
fi
```
```bash
chmod +x .git/hooks/commit-msg
```

---

## 🧪 17. Patches & Diffs

```bash
git format-patch main --stdout > patch.diff
git apply patch.diff
```

---

## 🕸️ 18. Workflows

### A) Simples
main estável → branches curtas → merge fast-forward

### B) Equipe (variante git-flow)
main (release)  
develop (integração)  
feature/*  
hotfix/*  

### C) Fork Flow
1. Fork
2. clone fork
3. add upstream
4. fetch upstream
5. rebase upstream/main
6. PR

### D) Rebase antes de enviar
```bash
git fetch origin
git rebase origin/main
git push -f origin minha-branch
```

---

## 🧼 19. Limpeza

```bash
git gc --prune=now --aggressive
git prune
git clean -fd
```

---

## ✅ 20. Checklist PR

- [ ] Commits claros
- [ ] Sem logs desnecessários
- [ ] Testes/verificação feitos
- [ ] Sem secrets
- [ ] Branch atualizada
- [ ] Sem arquivos gigantes
- [ ] Issue referida (Closes #X)

---

## 🧭 21. Resumo Ultrarrápido

```bash
# Ciclo
git add . && git commit -m "feat: ..."
git pull --rebase
git push

# Branch
git switch -c feature/x
git merge feature/x
git branch -d feature/x

# Correção
git revert <hash>
git cherry-pick <hash>

# Recuperação
git reflog
git reset --hard <hash>

# Histórico
git log --oneline --graph --decorate --all
```

---

## 📘 Recursos

| Tema | Link |
|------|------|
| Git Book | https://git-scm.com/book/pt-br |
| Conventional Commits | https://www.conventionalcommits.org/pt-br/v1.0.0 |
| SemVer | https://semver.org/lang/pt-BR/ |

---

Feito para aprendizado incremental & produtividade.