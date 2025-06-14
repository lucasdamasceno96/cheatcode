Claro! Vou criar um arquivo `postgresql-commands.md` completo e organizado com os principais comandos para você usar via CLI (`psql`). Assim fica fácil consultar para verificar o estado do seu banco PostgreSQL.

---

````markdown
# Comandos Básicos PostgreSQL via CLI (`psql`)

Este arquivo reúne os comandos essenciais para você gerenciar bancos, tabelas e dados no PostgreSQL usando o terminal.

---

## 1. Conectar ao banco via Docker

```bash
docker exec -it <container_name> psql -U <usuario> -d <banco>
# Exemplo:
docker exec -it postgres-db psql -U admin -d firstspringdb
````

---

## 2. Comandos Gerais no `psql`

| Comando           | Descrição                                  |
| ----------------- | ------------------------------------------ |
| `\l` ou `\list`   | Lista todos os bancos de dados             |
| `\c <db_name>`    | Conecta a um banco de dados diferente      |
| `\dt`             | Lista as tabelas do banco conectado        |
| `\d <table_name>` | Mostra o esquema (estrutura) de uma tabela |
| `\du`             | Lista os usuários e seus privilégios       |
| `\q`              | Sai do cliente `psql`                      |

---

## 3. Comandos para Tabelas e Dados

| Comando / SQL                                          | Descrição                         |
| ------------------------------------------------------ | --------------------------------- |
| `CREATE TABLE nome (coluna1 tipo, coluna2 tipo, ...);` | Cria uma nova tabela              |
| `DROP TABLE nome;`                                     | Apaga uma tabela                  |
| `INSERT INTO nome (col1, col2) VALUES (val1, val2);`   | Insere uma linha na tabela        |
| `SELECT * FROM nome;`                                  | Consulta todos os dados da tabela |
| `SELECT col1, col2 FROM nome WHERE condição;`          | Consulta com filtro               |
| `UPDATE nome SET coluna = valor WHERE condição;`       | Atualiza dados na tabela          |
| `DELETE FROM nome WHERE condição;`                     | Apaga dados da tabela             |

---

## 4. Comandos para Esquema e Index

| Comando / SQL                                   | Descrição                           |
| ----------------------------------------------- | ----------------------------------- |
| `ALTER TABLE nome ADD COLUMN nova_coluna tipo;` | Adiciona uma coluna                 |
| `ALTER TABLE nome DROP COLUMN coluna;`          | Remove uma coluna                   |
| `CREATE INDEX nome_idx ON nome (coluna);`       | Cria índice para acelerar consultas |
| `DROP INDEX nome_idx;`                          | Remove índice                       |

---

## 5. Informações do Servidor e Status

| Comando                      | Descrição                          |
| ---------------------------- | ---------------------------------- |
| `SELECT version();`          | Mostra versão do PostgreSQL        |
| `SHOW config_file;`          | Caminho do arquivo de configuração |
| `SELECT current_database();` | Mostra o banco atual conectado     |
| `SELECT current_user;`       | Usuário atual                      |

---

## 6. Exemplo Prático

```sql
-- Ver todas as tabelas no banco atual
\dt

-- Ver estrutura de uma tabela chamada "clientes"
\d clientes

-- Ver dados da tabela "clientes"
SELECT * FROM clientes;

-- Criar tabela de exemplo
CREATE TABLE produtos (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100),
  preco NUMERIC(10,2)
);

-- Inserir dados
INSERT INTO produtos (nome, preco) VALUES ('Teclado', 120.50);

-- Atualizar dados
UPDATE produtos SET preco = 115.00 WHERE nome = 'Teclado';

-- Apagar dados
DELETE FROM produtos WHERE id = 1;
```

---

## 7. Sair do psql

```sql
\q
```

---

