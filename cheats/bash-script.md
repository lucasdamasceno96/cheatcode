# Guia Completo sobre o Uso do Bash e Programação em Shell

O Bash (Bourne Again Shell) é um dos interpretadores de linha de comando mais utilizados em sistemas Unix e Linux. Ele também permite a criação de scripts, que são sequências de comandos executados automaticamente. Este guia é um tutorial completo para você dominar o Bash e a programação em shell.

---

## 1. **Introdução ao Bash**

### O que é o Bash?
- Um interpretador de comandos que permite interação com o sistema operacional.
- Suporte para automação de tarefas com scripts.

### Por que usar o Bash?
- Disponível em praticamente todas as distribuições Linux.
- Excelente para automação, administração de sistemas e manipulação de arquivos.

### Como acessar o Bash?
Abra um terminal em sua distribuição Linux ou use ferramentas como o WSL no Windows.

---

## 2. **Criando Scripts Bash**

### Estrutura Básica de um Script
1. Crie um arquivo com extensão `.sh`.
2. Adicione a linha `#!/bin/bash` no início para indicar o interpretador.
3. Insira os comandos no script.

### Exemplo Básico:
```bash
#!/bin/bash
# Este é um comentário

echo "Olá, Mundo!"
```

### Como executar o script:
1. Dê permissão de execução ao arquivo:
   ```bash
   chmod +x script.sh
   ```
2. Execute o script:
   ```bash
   ./script.sh
   ```

---

## 3. **Variáveis no Bash**

### Declarando Variáveis:
```bash
nome="João"
echo "Meu nome é $nome"
```

### Variáveis de Ambiente:
```bash
echo "O usuário atual é: $USER"
echo "O diretório atual é: $PWD"
```

---

## 4. **Condicionais no Bash**

### Estrutura do `if`:
```bash
if [ condição ]; then
    comandos
fi
```

### Exemplo:
```bash
#!/bin/bash
numero=10
if [ $numero -gt 5 ]; then
    echo "O número é maior que 5."
fi
```

### Uso do `else` e `elif`:
```bash
if [ $numero -gt 10 ]; then
    echo "Maior que 10"
elif [ $numero -eq 10 ]; then
    echo "Igual a 10"
else
    echo "Menor que 10"
fi
```

---

## 5. **Loops no Bash**

### O Loop `for`:
```bash
for i in 1 2 3 4 5; do
    echo "Número: $i"
done
```

### Iterando sobre arquivos:
```bash
for arquivo in *.txt; do
    echo "Arquivo encontrado: $arquivo"
done
```

### O Loop `while`:
```bash
contador=1
while [ $contador -le 5 ]; do
    echo "Contagem: $contador"
    ((contador++))
done
```

---

## 6. **Funções no Bash**

### Criando e Chamando Funções:
```bash
minha_funcao() {
    echo "Esta é uma função."
}

minha_funcao
```

### Funções com Argumentos:
```bash
soma() {
    echo "Soma: $(($1 + $2))"
}

soma 5 3
```

---

## 7. **Comandos Úteis no Bash**

### Manipulação de Arquivos:
```bash
ls -l
mkdir novo_diretorio
rm arquivo.txt
```

### Redirecionamento de Saída:
```bash
ls > arquivos.txt  # Redireciona a saída para um arquivo
ls >> arquivos.txt # Adiciona à saída existente
```

### Pipe:
```bash
ls | grep "arquivo"
```

---

## 8. **Scripts Avançados**

### Trabalhando com argumentos do script:
```bash
#!/bin/bash
echo "Primeiro argumento: $1"
echo "Segundo argumento: $2"
```

Execute com:
```bash
./script.sh arg1 arg2
```

### Checando o status do comando:
```bash
ls /diretorio_inexistente
if [ $? -ne 0 ]; then
    echo "Erro ao listar o diretório."
fi
```

### Laços e Condicionais Combinados:
```bash
#!/bin/bash
for arquivo in *.txt; do
    if [ -s "$arquivo" ]; then
        echo "O arquivo $arquivo não está vazio."
    fi
done
```

---

## 9. **Integração com Docker e Kubernetes**

### Criando contêineres Docker com Bash:
```bash
#!/bin/bash
docker run -d --name meu_container nginx
```

### Automação com Kubernetes:
```bash
#!/bin/bash
kubectl get pods | grep Running
```

---

## 10. **Melhores Práticas**
- Sempre inclua comentários explicativos.
- Teste scripts em um ambiente seguro antes de utilizá-los em produção.
- Use nomes de variáveis descritivos.
- Verifique erros usando condicionais.

---

### Conclusão
Este guia fornece uma base sólida para você começar a criar scripts Bash. Pratique os exemplos fornecidos e, aos poucos, expanda seus conhecimentos para lidar com tarefas mais complexas. A programação em shell é uma habilidade poderosa para administradores de sistemas e desenvolvedores!
