# Vim Cheat Sheet

## Modos do Vim
- **Modo Normal**: Navegar e executar comandos (tecla `Esc` para entrar).
- **Modo Inserção**: Inserir texto (tecla `i`, `a`, etc., para entrar).
- **Modo Visual**: Selecionar texto (tecla `v` ou `V` para entrar).
- **Modo de Comando**: Executar comandos (tecla `:` para entrar).

---

## Navegação Básica
- `h` - Esquerda.
- `l` - Direita.
- `j` - Para baixo.
- `k` - Para cima.
- `gg` - Ir para o início do arquivo.
- `G` - Ir para o final do arquivo.
- `0` - Ir para o início da linha.
- `^` - Ir para o primeiro caractere não vazio da linha.
- `$` - Ir para o final da linha.

---

## Inserção de Texto
- `i` - Inserir antes do cursor.
- `I` - Inserir no início da linha.
- `a` - Inserir após o cursor.
- `A` - Inserir no final da linha.
- `o` - Criar uma nova linha abaixo.
- `O` - Criar uma nova linha acima.

---

## Edição de Texto
- `x` - Excluir o caractere sob o cursor.
- `dd` - Excluir a linha atual.
- `yy` - Copiar a linha atual (yank).
- `p` - Colar abaixo do cursor.
- `P` - Colar acima do cursor.
- `u` - Desfazer a última ação.
- `Ctrl-r` - Refazer a última ação desfeita.
- `>>` - Indentar a linha.
- `<<` - Remover indentação da linha.

---

## Pesquisar e Substituir
- `/texto` - Pesquisar por "texto".
- `?texto` - Pesquisar por "texto" para trás.
- `n` - Próxima ocorrência da pesquisa.
- `N` - Ocorrência anterior da pesquisa.
- `:%s/antigo/novo/g` - Substituir "antigo" por "novo" no arquivo inteiro.
- `:s/antigo/novo/g` - Substituir "antigo" por "novo" na linha atual.

---

## Comandos de Arquivo
- `:w` - Salvar.
- `:q` - Sair.
- `:wq` ou `:x` - Salvar e sair.
- `:q!` - Sair sem salvar.
- `:e nome_arquivo` - Abrir arquivo.
- `:w nome_arquivo` - Salvar como.
- `:bn` - Próximo buffer.
- `:bp` - Buffer anterior.

---

## Trabalhando com Janelas
- `:split` ou `:sp` - Dividir horizontalmente.
- `:vsplit` ou `:vsp` - Dividir verticalmente.
- `Ctrl-w w` - Alternar entre janelas.
- `Ctrl-w c` - Fechar a janela atual.
- `Ctrl-w =` - Ajustar o tamanho das janelas igualmente.

---

## Trabalhando com Guias (Tabs)
- `:tabnew nome_arquivo` - Abrir um arquivo em uma nova guia.
- `:tabn` - Próxima guia.
- `:tabp` - Guia anterior.
- `:tabclose` - Fechar guia atual.

---

## Atalhos Úteis
- `.` - Repetir o último comando.
- `%` - Ir para o par correspondente (como parênteses, colchetes).
- `:noh` - Limpar o destaque da pesquisa.
- `Ctrl-g` - Mostrar informações do arquivo (linha, coluna, etc.).

---

Este guia cobre os comandos mais usados no Vim. Pratique regularmente para se familiarizar e aumentar sua produtividade!
