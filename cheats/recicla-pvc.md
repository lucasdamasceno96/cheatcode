# Reciclagem de PVC no Kubernetes

Este guia descreve como reciclar um PersistentVolumeClaim (PVC) no Kubernetes, garantindo que ele seja recriado automaticamente via GitOps. Além disso, ensina como realizar um rolling restart no Deployment ou StatefulSet e como remover o `finalizer` quando o PVC fica travado em "Finalizing".

## 1. Identificando o PVC
Antes de excluir um PVC, identifique o nome do recurso associado ao seu pod.

```sh
kubectl get pvc
```

Saída esperada:
```sh
NAME       STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
meu-pvc    Bound    pvc-12345678-90ab-cdef-1234-567890abcdef   10Gi       RWO            standard       5d
```

## 2. Excluir o PVC e o Volume Associado
Para reciclar o PVC, primeiro é necessário deletá-lo. Se o PVC estiver ligado a um Deployment ou StatefulSet, é necessário primeiro remover a referência ao PVC nos pods.

### 2.1. Removendo o PVC do Deployment ou StatefulSet
Se estiver usando um Deployment:
```sh
kubectl scale deployment meu-deployment --replicas=0
```
Se for um StatefulSet:
```sh
kubectl scale statefulset meu-statefulset --replicas=0
```
Isso garantirá que nenhum pod esteja utilizando o PVC antes da remoção.

### 2.2. Excluir o PVC
```sh
kubectl delete pvc meu-pvc
```
Se o PVC ficar travado no estado `Terminating`, vá para a seção **Removendo o Finalizer**.

### 2.3. Excluir o PV (se necessário)
Se o PVC não foi deletado corretamente e o PV ainda existir:
```sh
kubectl delete pv <nome-do-pv>
```

## 3. Garantindo a Recriação Automática do PVC
Como o ambiente utiliza GitOps, o PVC será recriado automaticamente conforme definido no repositório. Após deletá-lo, verifique se ele foi recriado corretamente com:

```sh
kubectl get pvc
```

Caso o PVC não seja recriado automaticamente, verifique o status do seu controlador GitOps (por exemplo, ArgoCD ou FluxCD) e sincronize as configurações.

## 4. Realizando Rolling Restart
Após a remoção e recriação do PVC, é necessário reiniciar os pods para que o novo PVC seja utilizado.

Se for um Deployment:
```sh
kubectl rollout restart deployment meu-deployment
```
Se for um StatefulSet:
```sh
kubectl rollout restart statefulset meu-statefulset
```

Se houver problemas na reimplantação, ajuste as configurações do PVC no `deployment.yaml` ou `statefulset.yaml` conforme necessário no repositório GitOps.

## 5. Removendo o Finalizer de um PVC Travado
Se o PVC ficar preso no estado `Terminating`, verifique seus metadados:

```sh
kubectl get pvc meu-pvc -o json
```
Se encontrar algo como:
```json
"finalizers": ["kubernetes.io/pvc-protection"]
```
Você precisa editar manualmente o PVC e remover esse finalizer.

### 5.1. Editando o PVC manualmente

```sh
kubectl edit pvc meu-pvc
```

No editor, localize a seção `finalizers` e remova a linha:
```yaml
finalizers:
  - kubernetes.io/pvc-protection
```
Salve e saia do editor, e então tente deletar o PVC novamente:
```sh
kubectl delete pvc meu-pvc
```

Agora o PVC deve ser removido corretamente, permitindo sua recriação automática pelo GitOps.

## Conclusão
Este guia ensinou como reciclar um PVC no Kubernetes dentro de um ambiente GitOps, remover o `finalizer` caso o PVC fique preso e garantir que os pods utilizem corretamente o novo PVC ao reiniciar o Deployment ou StatefulSet.
