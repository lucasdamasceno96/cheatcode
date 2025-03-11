Claro! Vou criar novamente o script e incluir a explicação sobre como iniciar o contêiner após um reinício ou algo semelhante.

### Passo 1: Criar o Script Shell

Crie um arquivo chamado `start_siyuan.sh` com o seguinte conteúdo:

```bash
#!/bin/bash

# Definir o diretório onde os dados serão persistidos
WORKSPACE_DIR="$PWD/workspace_dir_host"

# Verificar se o diretório já existe, caso contrário, criar
if [ ! -d "$WORKSPACE_DIR" ]; then
  echo "Criando o diretório de trabalho..."
  mkdir -p "$WORKSPACE_DIR"
else
  echo "Diretório de trabalho já existe."
fi

# Executar o contêiner Siyuan com volume persistente
echo "Iniciando o contêiner Siyuan..."
docker run -d --name siyuan \
  --restart unless-stopped \
  -p 6806:6806 \
  -v "$WORKSPACE_DIR:/siyuan/workspace" \
  -e SIYUAN_ACCESS_AUTH_CODE=623362 \
  b3log/siyuan:latest

echo "Contêiner Siyuan iniciado com sucesso!"
```

### Passo 2: Dar Permissão de Execução ao Script

Depois de criar o arquivo, você precisa dar permissão de execução ao script. No terminal, execute:

```bash
chmod +x start_siyuan.sh
```

### Passo 3: Executar o Script

Agora, basta executar o script para iniciar o contêiner:

```bash
./start_siyuan.sh
```

Esse script vai:

1. Verificar se o diretório `workspace_dir_host` já existe. Se não, ele cria.
2. Iniciar o contêiner **Siyuan** com as opções especificadas, incluindo o volume persistente e a variável de ambiente `SIYUAN_ACCESS_AUTH_CODE`.

### Passo 4: Iniciar o Contêiner Após Reinício ou Parada

Quando você reiniciar a máquina ou o Docker, o contêiner **Siyuan** será automaticamente reiniciado devido à política de reinício configurada com `--restart unless-stopped`. No entanto, se por algum motivo ele não reiniciar, você pode iniciar manualmente com o seguinte comando:

```bash
docker start siyuan
```

Esse comando vai garantir que o contêiner seja iniciado, mesmo após um reinício ou parada do Docker.

### Passo 5: Acessar a Aplicação

Após iniciar o contêiner, você pode acessar a aplicação no seu navegador usando o endereço:

```
http://localhost:6806
```

Esse endereço acessa o contêiner mapeado para a porta `6806`, conforme especificado no comando `docker run`.

### Passo 6: Acessar o Terminal do Contêiner (Opcional)

Se você precisar acessar o terminal dentro do contêiner para verificar logs ou executar outros comandos, use:

```bash
docker exec -it siyuan /bin/bash
```

Isso abrirá um terminal interativo dentro do contêiner **Siyuan**.

### Conclusão

- **Após reiniciar o sistema**: O contêiner será reiniciado automaticamente devido à configuração `--restart unless-stopped`.
- **Para iniciar o contêiner manualmente após reinício ou parada**: Use `docker start siyuan`.
- **Acessar a aplicação**: Vá para `http://localhost:6806` no navegador.
- **Acessar o terminal do contêiner**: Use `docker exec -it siyuan /bin/bash`.

Esse fluxo garante que você tenha o contêiner sempre disponível, mesmo após reinícios ou paradas.