1. Let us explore the environment first. How many nodes do you see in the cluster?
Including the controlplane and worker nodes.

1
2
3

2. How many applications do you see hosted on the cluster?
Check the number of deployments in the default namespace.

5
1
2
3

4. We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.

- Node node01 Unschedulable
- Pods evicted from node01

HINT >> Run the command kubectl drain node01 --ignore-daemonsets


6. The maintenance tasks have been completed. Configure the node node01 to be schedulable again.

CheckCompleteIncomplete
Node01 is Schedulable

HINT >> Run the command kubectl uncordon node01

8. Why are there no pods on node01?
- node01 is cordoned
- node01 did not upgrade successfully
- Only when new pods are created they will be scheduled
- node01 is faulty 

HINT >> Running the uncordon command on a node will not automatically schedule pods on the node. When new pods are created, they will be placed on node01.

9. Why are the pods placed on the controlplane node?
Check the controlplane node details.

- controlplane node does not have any taints
- controlplane node is cordoned
- controlplane node is faulty
- you can never have pods on master nodes
- controlplane node has taints set on it



10. 
11. 
12. Why did the drain command fail on node01? It worked the first time!

- no pods on node01
- node01 was not upgraded correctly the last time
- there is a pod in node01 which is not part of a replicaset
- node01 tainted

HINT >> Run: kubectl get pods -o wide and you will see that there is a single pod scheduled on node01 which is not part of a replicaset.
The drain command will not work in this case. To forcefully drain the node we now have to use the --force flag.

13. 
14. What would happen to hr-app if node01 is drained forcefully?
Try it and see for yourself.

- hr-app will be re-created on master
- hr-app will continue to run as a Docker container
- hr-app will be lost forever
- hr-app will be recreated on other nodes

16. hr-app is a critical app and we do not want it to be removed and we do not want to schedule any more pods on node01.
Mark node01 as unschedulable so that no new pods are scheduled on this node.
Make sure that hr-app is not affected.

- Node01 Unschedulable
- hr-app still running on node01?

HINT >> Run the command kubectl cordon node01

SOLUTION >> Do not drain node01, instead use the kubectl cordon node01 command. This will ensure that no new pods are scheduled on this node and the existing pods will not be affected by this operation.

