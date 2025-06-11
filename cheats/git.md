Aqui está um exemplo de arquivo `melhores-praticas-git.md` com as principais boas práticas para uso profissional do Git, incluindo convenções de commit, uso de branches e pull requests:

---

# 🧠 Melhores Práticas com Git

## 📂 1. Organização de Branches

* **`main` ou `master`**: branch principal com código em produção.
* **`develop`** (opcional): branch de integração de funcionalidades (pré-produção).
* **Feature branches**: para novas funcionalidades (ex: `feature/login-page`).
* **Bugfix branches**: para correções de bugs (ex: `bugfix/fix-auth-token`).
* **Hotfix branches**: para correções urgentes em produção (ex: `hotfix/crash-on-load`).

---

## ✍️ 2. Commits Semânticos

Use o formato:

```
<tipo>(escopo): descrição sucinta no imperativo
```

### Tipos mais comuns:

* `feat`: nova funcionalidade
* `fix`: correção de bug
* `refactor`: refatoração de código
* `docs`: documentação
* `style`: formatação (sem alteração de lógica)
* `test`: adição ou modificação de testes
* `chore`: tarefas auxiliares (build, configs)

### Exemplos:

* `feat(auth): add JWT token validation`
* `fix(user): handle null pointer on profile fetch`
* `docs(readme): add installation instructions`

---

## 🌱 3. Criando uma Nova Branch

Sempre crie uma branch a partir da branch principal de trabalho:

```bash
git checkout main
git pull origin main
git checkout -b feature/nome-da-feature
```

---

## ✅ 4. Checklist antes de um Commit

* Código testado localmente
* Sem arquivos desnecessários (`.env`, `.log`, `node_modules`)
* Commit com mensagem clara e tipo adequado
* Evitar commits muito grandes (divida em partes lógicas)

---

## 🔁 5. Atualizando sua Branch

Antes de abrir um pull request:

```bash
git fetch origin
git rebase origin/main
# ou git merge origin/main (se sua equipe preferir merge)
```

---

## 🚀 6. Pull Requests

* Abra um PR apenas quando a feature estiver pronta.
* Faça *squash* de commits se necessário.
* Solicite revisão de um colega.
* Escreva uma descrição clara no PR (o que foi feito, como testar, etc).
* Nunca faça merge com erros de CI/CD.

---

## 🧽 7. Limpeza

Após merge:

```bash
git checkout main
git pull origin main
git branch -d feature/nome-da-feature
git push origin --delete feature/nome-da-feature
```

---

