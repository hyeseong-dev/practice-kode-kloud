1. This lab tests your skills on upgrading a kubernetes cluster. We have a production cluster with applications running on it. Let us explore the setup first.

What is the current version of the cluster?

- v1.21.0
- v1.20.0
- v1.23.0
- v1.19.1

2. How many nodes are part of this cluster?
Including controlplane and worker nodes

- 2
- 4
- 1
- 0
- 3

HINT >> Check the taints on both controlplane and node01. If none exists, then both nodes can host workloads.

SOLUTION >> 

By running the kubectl describe node command, we can see that neither nodes have taints.

```bash
root@controlplane:~# kubectl describe nodes  controlplane | grep -i taint
Taints:             <none>
root@controlplane:~# 
root@controlplane:~# kubectl describe nodes  node01 | grep -i taint
Taints:             <none>
root@controlplane:~# 
```
This means that both nodes have the ability to schedule workloads on them.

3. 

4. How many applications are hosted on the cluster?
Count the number of deployments in the default namespace.

- 0
- 1
- 2
- 3

질문 : 여기서 말하는 앱이 무엇인가?
디플로이와 레플리카셋에서 .app 으로 도트 연결이 되는데 이를 말하는 것인지???? 그럼 디플로이만 앱의 영역이 되고 
레플리카셋은 해당 되지 않는 것은 레플리카셋은 컨트롤러의 영역이고 실질적인 서버 배포를 하는 부분은 아니기 때문에?

5. What nodes are the pods hosted on?

- node01
- controlplane,node01
- node01,node02
- controlplane
- node02

6. You are tasked to upgrade the cluster. Users accessing the applications must not be impacted, and you cannot provision new VMs. What strategy would you use to upgrade the cluster?

Users will be impacted since there is only one worker node
Add new nodes with newer versions while taking down existing nodes
Upgrade all nodes at once
Upgrade one node at a time while moving the workloads to the other

7. What is the latest stable version available for upgrade?
Use the kubeadm tool

- v1.22.1
- v1.21.0
- v1.20.0
- v1.23.12
HINT >> Run the kubeadm upgrade plan command

8. 

9. 

10. 

11. 

12. 

13. 

14. 

