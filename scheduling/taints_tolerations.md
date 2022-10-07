WHAT IS TAINTS AND TOLERATIONS?

- taint : "(평판 등을) 더럽히다, 오염시키다, 오점[오명]을 남기다"의 의미를 보았을 때, 부정적인 느낌을 주는 만큼. 
테인트 노드가 파드 셋을 제외시킬 수 있다.

톨러레이션은 파드에 적용된다. 톨러레이션을 통해 스케줄러는 그와 일치하는 테인트가 있는 파드를 스케줄할 수 있다. 톨러레이션은 스케줄을 허용하지만 보장하지는 않는다. 스케줄러는 그 기능의 일부로서 다른 매개변수를 고려한다.

- tolerations : 용인, 관용 (=tolerance)

1. Create a taint on node01 with key of spray, value of mortein and effect of NoSchedule

힌트 : Run the command: kubectl taint nodes node01 spray=mortein:NoSchedule

2. Create a new pod with the nginx image and pod name as mosquito.

```yaml

Solution manifest file to create a pod called bee as follows:

---
apiVersion: v1
kind: Pod
metadata:
  name: bee
spec:
  containers:
  - image: nginx
    name: bee
  tolerations:
  - key: spray
    value: mortein
    effect: NoSchedule
    operator: Equal
then run the kubectl create -f <FILE-NAME>.yaml to create a pod.
```

10. Remove the taint on controlplane, which currently has the taint effect of NoSchedule.

Run the command: kubectl taint nodes controlplane node-role.kubernetes.io/master:NoSchedule- to untaint the node.

Run the command: kubectl taint nodes controlplane node-role.kubernetes.io/master:NoSchedule
 마이너스 기호를 마지막에 반드시 붙여야함.`-` to untaint the node.