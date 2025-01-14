# Principais Ferramentas Linux para Teste de Conectividade

No contexto de troubleshooting em ambientes Linux, Docker e Kubernetes, dominar as ferramentas de conectividade é essencial. Essas ferramentas ajudam a diagnosticar problemas de rede, verificar conexões e monitorar a comunicação entre componentes do sistema. Abaixo estão as principais ferramentas, explicadas detalhadamente com exemplos de uso e cenários práticos.

---

## 1. **ping**
O `ping` é utilizado para verificar se um host está acessível e medir o tempo de resposta (latência) entre o seu sistema e o destino.

### Sintaxe:
```bash
ping <endereço_IP_ou_hostname>
```

### Exemplos:
```bash
ping 8.8.8.8    # Testa a conectividade com o DNS público do Google
ping www.example.com -c 4  # Envia apenas 4 pacotes ICMP para o domínio example.com
```

### Cenários de Uso:
- Verificar se um contêiner no Docker ou pod no Kubernetes responde a solicitações.
- Diagnosticar falhas de rede ao tentar se conectar a servidores externos.

No contexto de Kubernetes:
```bash
kubectl exec -it <nome_do_pod> -- ping 8.8.8.8
```
Este comando verifica se um pod tem conectividade externa com o Google DNS.

---

## 2. **traceroute**
O `traceroute` exibe o caminho que os pacotes percorrem até um destino, listando os roteadores intermediários.

### Sintaxe:
```bash
traceroute <endereço_IP_ou_hostname>
```

### Exemplos:
```bash
traceroute www.example.com
```

### Cenários de Uso:
- Identificar onde a comunicação está sendo interrompida em uma rota.
- Diagnosticar problemas de conectividade entre diferentes clusters Kubernetes.

Em um contêiner Docker:
```bash
docker exec -it <nome_do_container> traceroute www.example.com
```
---

## 3. **netstat** e **ss**
Essas ferramentas mostram informações sobre conexões de rede, portas abertas e estatísticas de rede.

### Sintaxe (netstat):
```bash
netstat -tuln
```

### Sintaxe (ss):
```bash
ss -tuln
```

### Exemplos:
- Listar conexões TCP ativas:
  ```bash
  ss -t
  ```
- Verificar portas de escuta:
  ```bash
  netstat -ln
  ```

### Cenários de Uso:
- Verificar quais portas estão abertas em um contêiner ou pod.
- Diagnosticar problemas de conectividade em serviços expostos por Kubernetes.

Em um pod Kubernetes:
```bash
kubectl exec -it <nome_do_pod> -- ss -tuln
```

---

## 4. **curl**
O `curl` é usado para testar solicitações HTTP/HTTPS e outros protocolos, como FTP.

### Sintaxe:
```bash
curl <URL>
```

### Exemplos:
```bash
curl -I https://www.example.com  # Mostra apenas os cabeçalhos da resposta HTTP
curl -X POST -d "key=value" https://api.example.com/endpoint
```

### Cenários de Uso:
- Verificar se uma API está respondendo no Kubernetes:
  ```bash
  kubectl exec -it <nome_do_pod> -- curl https://api.example.com/endpoint
  ```
- Testar endpoints de serviços em contêineres Docker ou entre pods.

---

## 5. **dig**
O `dig` é usado para consultas DNS, como resolução de nomes e obtenção de registros específicos.

### Sintaxe:
```bash
dig <domínio>
```

### Exemplos:
```bash
dig google.com
```

### Cenários de Uso:
- Diagnosticar problemas de DNS em Kubernetes:
  ```bash
  kubectl exec -it <nome_do_pod> -- dig google.com
  ```
- Verificar registros DNS personalizados em um serviço.

---

## 6. **telnet** e **nc (netcat)**
Essas ferramentas verificam a conectividade com uma porta específica de um host.

### Sintaxe (telnet):
```bash
telnet <host> <porta>
```

### Sintaxe (nc):
```bash
nc -zv <host> <porta>
```

### Exemplos:
```bash
nc -zv example.com 80  # Verifica se a porta 80 está aberta no host example.com
```

### Cenários de Uso:
- Testar conectividade entre contêineres:
  ```bash
  docker exec -it <nome_do_container> nc -zv 10.0.0.1 80
  ```
- Verificar se um serviço está acessível em um cluster Kubernetes.

---

## 7. **ip** e **ifconfig**
Essas ferramentas mostram informações sobre interfaces de rede e permitem configurá-las.

### Sintaxe (ip):
```bash
ip addr
ip route
```

### Exemplos:
- Verificar interfaces de rede:
  ```bash
  ip addr
  ```
- Exibir a tabela de roteamento:
  ```bash
  ip route
  ```

### Cenários de Uso:
- Verificar a configuração de rede de pods em Kubernetes:
  ```bash
  kubectl exec -it <nome_do_pod> -- ip addr
  ```
- Diagnosticar problemas de rota entre contêineres Docker.

---

### Conclusão
Essas ferramentas são fundamentais para resolver problemas de conectividade em Linux, Docker e Kubernetes. Pratique o uso delas em diferentes cenários e ambientes para ganhar confiança e eficácia no diagnóstico de problemas.
