# Guia Completo sobre Storage no Linux

O armazenamento no Linux é gerenciado através de discos, partições e sistemas de arquivos. Este guia detalha como verificar discos, entender o funcionamento do filesystem e utilizar o LVM (Logical Volume Manager) para gerenciar e alterar diretórios específicos.

---

## 1. **Verificando Discos no Linux**

### Listando Dispositivos de Armazenamento
- **`lsblk`**: Lista dispositivos de blocos em formato hierárquico.
  ```bash
  lsblk
  ```
  Saída típica:
  ```
  NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
  sda      8:0    0  100G  0 disk 
  ├─sda1   8:1    0   50G  0 part /
  ├─sda2   8:2    0   25G  0 part /home
  └─sda3   8:3    0   25G  0 part [SWAP]
  ```

- **`fdisk`**: Exibe e manipula tabelas de partições.
  ```bash
  sudo fdisk -l
  ```

- **`df`**: Mostra o uso de espaço em disco para sistemas de arquivos montados.
  ```bash
  df -h
  ```
  Saída típica:
  ```
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/sda1        50G   20G   30G  40% /
  /dev/sda2        25G   15G   10G  60% /home
  ```

- **`du`**: Exibe o uso de espaço por arquivos e diretórios.
  ```bash
  du -sh /caminho/do/diretorio
  ```

---

## 2. **Como Funciona o Filesystem no Linux**

### Estrutura de Diretórios no Linux
- **`/` (Raiz)**: Ponto de montagem principal, onde todos os outros diretórios são montados.
- **`/home`**: Diretórios dos usuários.
- **`/var`**: Arquivos de logs e dados variáveis.
- **`/tmp`**: Arquivos temporários.
- **`/boot`**: Arquivos necessários para inicialização do sistema.

### Sistemas de Arquivos Comuns
- **ext4**: Padrão para a maioria das distribuições Linux, confiável e eficiente.
- **xfs**: Ótimo para alto desempenho e grandes arquivos.
- **btrfs**: Avançado, com suporte a snapshots e compressão.

### Comandos para Gerenciar Filesystems
- **Criar um sistema de arquivos**:
  ```bash
  mkfs.ext4 /dev/sda1
  ```
- **Verificar um sistema de arquivos**:
  ```bash
  fsck /dev/sda1
  ```
- **Montar um sistema de arquivos**:
  ```bash
  mount /dev/sda1 /mnt
  ```
- **Desmontar um sistema de arquivos**:
  ```bash
  umount /mnt
  ```
- **Mostrar sistemas de arquivos montados**:
  ```bash
  mount | column -t
  ```

---

## 3. **Gerenciamento de Volumes com LVM**

O LVM permite gerenciar volumes lógicos, oferecendo flexibilidade para redimensionar partições e mover dados sem interrupções.

### Estrutura do LVM
- **Physical Volume (PV)**: Corresponde aos discos físicos.
- **Volume Group (VG)**: Conjunto de PVs agrupados.
- **Logical Volume (LV)**: Partições lógicas criadas dentro de um VG.

### Configurando o LVM

1. **Criar um Physical Volume**:
   ```bash
   sudo pvcreate /dev/sdb
   ```

2. **Criar um Volume Group**:
   ```bash
   sudo vgcreate meu_vg /dev/sdb
   ```

3. **Criar um Logical Volume**:
   ```bash
   sudo lvcreate -L 20G -n meu_lv meu_vg
   ```

4. **Formatar e Montar o Logical Volume**:
   ```bash
   sudo mkfs.ext4 /dev/meu_vg/meu_lv
   sudo mount /dev/meu_vg/meu_lv /mnt
   ```

5. **Adicionar ao `fstab` para Montagem Automática**:
   ```bash
   echo '/dev/meu_vg/meu_lv /mnt ext4 defaults 0 0' | sudo tee -a /etc/fstab
   ```

### Alterando um Diretório Específico com LVM

1. **Mover Dados para Outro Local Temporário**:
   ```bash
   sudo mv /diretorio/atual /diretorio/temp
   ```

2. **Criar o Logical Volume para o Diretório**:
   ```bash
   sudo lvcreate -L 10G -n novo_lv meu_vg
   sudo mkfs.ext4 /dev/meu_vg/novo_lv
   sudo mount /dev/meu_vg/novo_lv /diretorio/atual
   ```

3. **Mover os Dados de Volta**:
   ```bash
   sudo mv /diretorio/temp/* /diretorio/atual/
   ```

4. **Atualizar o `fstab`**:
   ```bash
   echo '/dev/meu_vg/novo_lv /diretorio/atual ext4 defaults 0 0' | sudo tee -a /etc/fstab
   ```

---

## 4. **Comandos Úteis para LVM**
- **Exibir Physical Volumes**:
  ```bash
  sudo pvs
  ```
- **Exibir Volume Groups**:
  ```bash
  sudo vgs
  ```
- **Exibir Logical Volumes**:
  ```bash
  sudo lvs
  ```
- **Redimensionar um Logical Volume**:
  - Aumentar:
    ```bash
    sudo lvextend -L +5G /dev/meu_vg/meu_lv
    sudo resize2fs /dev/meu_vg/meu_lv
    ```
  - Reduzir:
    ```bash
    sudo umount /dev/meu_vg/meu_lv
    sudo lvreduce -L -5G /dev/meu_vg/meu_lv
    sudo mount /dev/meu_vg/meu_lv
    ```

---

## Conclusão
Com este guia, você pode gerenciar discos, sistemas de arquivos e volumes lógicos no Linux de forma eficiente. O conhecimento de LVM é essencial para administradores que precisam de flexibilidade e controle sobre o armazenamento. Pratique os comandos em um ambiente seguro antes de aplicá-los em produção!
