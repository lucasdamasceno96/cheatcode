Claro! Vou criar um arquivo `docker-commands.md` com os principais comandos Docker, incluindo como criar e executar um `docker-compose.yml`, usando o container PostgreSQL como exemplo.

---

````markdown
# Comandos Básicos Docker e Docker Compose

Este arquivo reúne os comandos essenciais para você trabalhar com Docker e Docker Compose, usando um container PostgreSQL como exemplo.

---

## 1. Comandos Docker Básicos

| Comando                            | Descrição                                       |
|----------------------------------|------------------------------------------------|
| `docker pull <imagem>`            | Baixa uma imagem do Docker Hub                   |
| `docker images`                   | Lista as imagens baixadas localmente             |
| `docker ps`                      | Lista containers em execução                      |
| `docker ps -a`                   | Lista todos os containers (ativos e parados)     |
| `docker run -d --name <nome> <imagem>` | Cria e executa um container em background    |
| `docker exec -it <container> bash` | Acessa o terminal interativo de um container    |
| `docker logs <container>`         | Exibe os logs do container                        |
| `docker stop <container>`         | Para um container em execução                      |
| `docker rm <container>`           | Remove um container parado                         |
| `docker rmi <imagem>`             | Remove uma imagem local                            |

---

## 2. Criando e Executando um Docker Compose

### Exemplo: `docker-compose.yml` para PostgreSQL

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16
    container_name: postgres-db
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: 123456
      POSTGRES_DB: firstspringdb
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
````

---

### Passos para usar o Docker Compose

1. Salve o arquivo `docker-compose.yml` na sua pasta de trabalho.

2. Para subir os containers definidos:

```bash
docker-compose up -d
```

3. Para listar os containers rodando:

```bash
docker-compose ps
```

4. Para parar os containers:

```bash
docker-compose down
```

5. Para ver os logs do container PostgreSQL:

```bash
docker-compose logs -f postgres
```

---

## 3. Acessando o container PostgreSQL

Após subir o container, você pode acessar o banco via terminal:

```bash
docker exec -it postgres-db psql -U admin -d firstspringdb
```

---

## 4. Comandos úteis no psql (cliente PostgreSQL)

* `\dt` — lista tabelas
* `\d <tabela>` — mostra estrutura da tabela
* `SELECT * FROM <tabela>;` — consulta dados da tabela
* `\q` — sai do cliente psql

---
