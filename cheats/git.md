Claro! Aqui está o arquivo `melhores-praticas-git.md` **atualizado** com a seção explicando **como fazer push para a nova branch, abrir um merge (pull) request e deletar a branch antiga** após o merge:

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

* Faça push da branch para o GitHub:

  ```bash
  git push origin feature/nome-da-feature
  ```

* No GitHub, crie um **Pull Request**:

  * Compare `feature/nome-da-feature` com `main`
  * Escreva um título claro e uma descrição com:

    * O que foi feito
    * Como testar
    * Qual problema resolve

* Aguarde a revisão de outro membro da equipe.

* Após aprovação e sucesso do CI/CD, **faça o merge no GitHub** (preferencialmente com `Squash and merge`).

---

## 🧽 7. Limpeza após o Merge

Depois que o PR for aceito e a branch mergeada:

```bash
git checkout main
git pull origin main
git branch -d feature/nome-da-feature         # Deleta localmente
git push origin --delete feature/nome-da-feature  # Deleta no GitHub
```

---
Aqui está um **template de Pull Request** profissional e adaptável para equipes que seguem boas práticas de versionamento:

---

### 📄 `.github/pull_request_template.md`

```markdown
## 🚀 Descrição

<!-- Descreva de forma objetiva o que essa PR faz -->

## 📝 Checklist

- [ ] Código testado localmente
- [ ] Cobertura de testes adequada
- [ ] Documentação atualizada (se necessário)
- [ ] Sem arquivos desnecessários incluídos

## 🧪 Como testar

<!-- Explique como validar as alterações. Ex: comandos, rota da API, comportamento esperado -->

## 🧩 Tipo de mudança

Marque com `x` o que se aplica:

- [ ] Nova funcionalidade (`feat`)
- [ ] Correção de bug (`fix`)
- [ ] Refatoração (`refactor`)
- [ ] Atualização de documentação (`docs`)
- [ ] Outro: __________________________

## 📎 Tarefa relacionada (opcional)

<!-- Ex: Jira, Trello ou GitHub Issues -->
Closes #123

## 🗒️ Notas adicionais

<!-- Alguma dependência, contexto ou impacto a considerar? -->
```

---

📌 **Como usar:**

1. Crie a pasta `.github/` na raiz do seu projeto (se não existir).
2. Crie o arquivo `pull_request_template.md` dentro dela.
3. O GitHub aplicará automaticamente esse modelo sempre que alguém abrir um PR.

Se quiser um exemplo real preenchido ou um [template adaptado para projetos solo](f), posso montar também.

