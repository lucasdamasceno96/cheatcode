# Guia Completo: Interação com Linux via CLI

A CLI (Command Line Interface) do Linux é uma ferramenta poderosa para manipulação de texto, automação de tarefas e interação com sistemas, incluindo ferramentas como AWS CLI. Este guia abrange detalhadamente como usar a CLI para trabalhar eficientemente, incluindo manipulação de texto, redirecionamento de saída, uso de loops e integração de comandos.

---

## 1. **Entendendo Entrada e Saída no Linux**

### Conceitos Básicos
- **stdin** (entrada padrão): Entrada fornecida ao comando, geralmente pelo teclado.
- **stdout** (saída padrão): Saída gerada pelo comando, exibida na tela.
- **stderr** (saída de erro): Mensagens de erro geradas pelo comando.

### Redirecionamento de Saída
- Redirecionar `stdout` para um arquivo:
  ```bash
  comando > arquivo.txt
  ```
- Adicionar ao arquivo em vez de sobrescrever:
  ```bash
  comando >> arquivo.txt
  ```
- Redirecionar `stderr` para um arquivo:
  ```bash
  comando 2> erro.txt
  ```
- Redirecionar `stdout` e `stderr` juntos:
  ```bash
  comando > saida.txt 2>&1
  ```
- Descartar saída com `/dev/null`:
  ```bash
  comando > /dev/null 2>&1
  ```

---

## 2. **Manipulação de Texto**

### Comandos Comuns
- **cat**: Exibir o conteúdo de arquivos:
  ```bash
  cat arquivo.txt
  ```
- **head** e **tail**: Exibir linhas do início ou fim de um arquivo:
  ```bash
  head -n 10 arquivo.txt
  tail -n 10 arquivo.txt
  ```
- **less**: Navegar em arquivos grandes:
  ```bash
  less arquivo.txt
  ```
- **grep**: Filtrar linhas com base em padrões:
  ```bash
  grep "erro" arquivo.txt
  ```
- **awk**: Processar e extrair dados de forma avançada:
  ```bash
  awk '{print $2}' arquivo.txt  # Exibe a segunda coluna
  ```
- **sed**: Substituir texto:
  ```bash
  sed 's/antigo/novo/g' arquivo.txt
  ```

---

## 3. **Exibição de Dados na Tela**
- **Colunas e tabelas**: Muitos comandos geram saída tabular, como `ls`, `ps`, ou `df`. 
  - Para exibir uma tabela formatada:
    ```bash
    ls -lh
    ```
- **Seleção de colunas específicas**:
  ```bash
  df -h | awk '{print $1, $2}'
  ```
- **Ordenação e remoção de duplicados**:
  ```bash
  sort arquivo.txt | uniq
  ```

---

## 4. **Pipelines e Composição de Comandos**

### Usando o Pipe (`|`)
Um pipe conecta a saída de um comando como entrada de outro:
```bash
ls -lh | grep "txt"
```

### Combinando Comandos
- Encadear comandos com `&&` (executa o próximo somente se o anterior for bem-sucedido):
  ```bash
  mkdir novo_diretorio && cd novo_diretorio
  ```
- Executar comandos em paralelo com `&`:
  ```bash
  comando1 & comando2 &
  ```

---

## 5. **Usando Loops diretamente na CLI**

### Loop `for`
```bash
for arquivo in *.txt; do
    echo "Processando $arquivo"
done
```

### Exemplo: Renomear arquivos em lote
```bash
for i in *.txt; do
    mv "$i" "novo_$i"
done
```

---

## 6. **Comandos AWS na CLI**

### Configuração Inicial
```bash
aws configure
```
Forneça sua `Access Key`, `Secret Key` e região padrão.

### Exemplos de Uso
- Listar buckets S3:
  ```bash
  aws s3 ls
  ```
- Fazer upload de um arquivo para S3:
  ```bash
  aws s3 cp arquivo.txt s3://meu-bucket/
  ```
- Descrever instâncias EC2:
  ```bash
  aws ec2 describe-instances
  ```

---

## 7. **Outros Comandos Úteis**

### Monitoramento de Sistema
- **top**: Monitorar processos em tempo real.
  ```bash
  top
  ```
- **df**: Verificar uso de disco.
  ```bash
  df -h
  ```
- **du**: Exibir uso de espaço de arquivos e diretórios:
  ```bash
  du -sh *
  ```

### Gerenciamento de Processos
- **kill**: Finalizar processos.
  ```bash
  kill -9 <PID>
  ```
- **jobs** e **fg**: Gerenciar processos em segundo plano.
  ```bash
  jobs
  fg %1
  ```

---

## 8. **Melhores Práticas**
- Sempre use `man <comando>` para consultar a documentação de comandos.
- Combine ferramentas como `grep`, `awk`, e `sed` para manipular e processar dados de forma eficiente.
- Teste seus scripts ou comandos em um ambiente seguro antes de aplicá-los em produção.

---

Com estas ferramentas e técnicas, você pode realizar praticamente qualquer tarefa via CLI no Linux, de automação a administração avançada de sistemas!
