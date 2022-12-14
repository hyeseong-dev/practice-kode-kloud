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

3. How many nodes can host workloads in this cluster?

Inspect the applications and taints set on the nodes.


2
4
1
3

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

HINT >> In order to ensure minimum downtime, upgrade the cluster one node at a time, while moving the workloads to another node. In the upcoming tasks you will get to practice how to do that.


7. What is the latest stable version available for upgrade?
Use the kubeadm tool

- v1.22.1
- v1.21.0
- v1.20.0
- v1.23.12
HINT >> Run the `kubeadm upgrade plan` command

8. We will be upgrading the controlplane node first. Drain the controlplane node of workloads and mark it UnSchedulable

CheckCompleteIncomplete
Controlplane Node: SchedulingDisabled

HINT >> Run the `kubectl drain controlplane --ignore-daemonsets`
SOLUTION >> 
There are daemonsets created in this cluster, especially in the kube-system namespace. To ignore these objects and drain the node, we can make use of the --ignore-daemonsets flag.



9. 

10. Mark the controlplane node as "Schedulable" again
  
Check
- Controlplane Node: Ready & Schedulable

HINT >> Use the `kubectl uncordon command`
SOLUTION >> Run the command: `kubectl uncordon controlplane`

--- 
cordon에 대한 개념 학습 필요 

- drain에 대한 차이점과 비슷한점
- uncordon command는 무엇일까?



11. Next is the worker node. Drain the worker node of the workloads and mark it UnSchedulable

Check
- Worker node: Unschedulable

힌트 >> Use the `kubectl drain command`
SOLUTION >> Run the command: `kubectl drain node01 --ignore-daemonsets`


12. Upgrade the worker node to the exact version v1.24.0

Check

- Worker Node Upgraded to v1.24.0
- Worker Node Ready

HINT >> Make sure that the correct version of kubeadm is installed and then proceed to upgrade the node01 node. Once this is done, upgrade the kubelet on the node.

SOLUTION >> 

On the node01 node, run the following commands:

| If you are on the controlplane node, run ssh node01 to log in to the node01.

This will update the package lists from the software repository.
```bash
apt-get update
```

This will install the kubeadm version 1.24.0.
```bash
apt-get install kubeadm=1.24.0-00
```

This will upgrade the node01 configuration.
```bash
kubeadm upgrade node
```

This will update the kubelet with the version 1.24.0.
```bash
apt-get install kubelet=1.24.0-00 
```

You may need to reload the daemon and restart kubelet service after it has been upgraded.
```bash
systemctl daemon-reload
systemctl restart kubelet
```

Type exit or logout or enter CTRL + d to go back to the controlplane node.

13. Remove the restriction and mark the worker node as schedulable again.

Check
- Worker Node: Schedulable

HINT >>
Use the kubectl uncordon command

SOLUTION >> 

Run the command: `kubectl uncordon node01`

