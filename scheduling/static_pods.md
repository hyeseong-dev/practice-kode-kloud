1. How many static pods exist in this cluster in all namespaces?

Run the command kubectl get pods --all-namespaces and look for those with -controlplane appended in the name
    
/etc/kubernetes/manifests 디렉토리를 확인하여 야믈파일의 개수를 파악함

그럼 안에 etcd, kube-apiserver, kube-controller-manager, kube-scheduler file 4개가 각각 있으므로 이에 기반하여 4개가 있다는 것을 유추할 수 있음. 

```bash

```


Create a static pod named static-busybox that uses the busybox image and the command sleep 1000
CheckCompleteIncompleteNext
Name: static-busybox
Image: busybox

아래 명령어는 yaml file을 생성시키도록 함. 
```bash
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: static-busybox
  name: static-busybox
spec:
  containers:
  - command:
    - sleep
    - "1000"
    image: busybox
    name: static-busybox
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```

2. Which of the below components is NOT deployed as a static pod?

- kube-apiserver
- etcd
- kube-controller-manager
- coredns

3. Which of the below components is NOT deployed as a static POD?

kube-controller-manager
kube-apiserver
kube-proxy
kube-scheduler

4. On which nodes are the static pods created currently?

- node01
- controlplane
- controlplane & node01
- All Nodes

힌트 >> Run the kubectl get pods --all-namespaces -o wide and identify the node in which static pods are deployed.

솔루션 >> By default, static pods are created for the controlplane components and hence, they are only created in the controlplane node.

5. What is the path of the directory holding the static pod definition files?

- /etc/kubernetes/manifests
- /var/kubelet/manifests
- /etc/kubernetes/pods
- /etc/kubelet/manifests

힌트 >> Run the command ps -aux | grep kubelet and identify the config file - --config=/var/lib/kubelet/config.yaml. Then check in the config file for staticPodPath.

솔루션 >> 

First idenity the kubelet config file:

```bash
root@controlplane:~# ps -aux | grep /usr/bin/kubelet
root      3668  0.0  1.5 1933476 63076 ?       Ssl  Mar13  16:18 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --network-plugin=cni --pod-infra-container-image=k8s.gcr.io/pause:3.2
root      4879  0.0  0.0  11468  1040 pts/0    S+   00:06   0:00 grep --color=auto /usr/bin/kubelet
root@controlplane:~# 
```

From the output we can see that the kubelet config file used is /var/lib/kubelet/config.yaml

Next, lookup the value assigned for staticPodPath:

```bash
root@controlplane:~# grep -i staticpod /var/lib/kubelet/config.yaml
staticPodPath: /etc/kubernetes/manifests
root@controlplane:~# 
```

As you can see, the path configured is the /etc/kubernetes/manifests directory.

6. 

7. What is the docker image used to deploy the kube-api server as a static pod?

- k8s.gcr.io/kube-apiserver-amd64:v1.10.3
- k8s.gcr.io/kube-apiserver:v1.24.0
- docker.io/kube-apiserver-amd64:v1.11.3

HINT >> Check the image defined in the /etc/kubernetes/manifests/kube-apiserver.yaml manifest file.

8. Create a static pod named static-busybox that uses the busybox image and the command sleep 1000

CheckCompleteIncomplete
Name: static-busybox

Image: busybox

HINT >> Create a pod definition file called static-busybox.yaml with the provided specs and place it under /etc/kubernetes/manifests directory.

SOLUTION >> Create a pod definition file in the manifests folder. To do this, run the command:
```bash
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

9. Edit the image on the static pod to use busybox:1.28.4

CheckCompleteIncomplete
Name: static-busybox

Image: busybox:1.28.4

HINT >> Update the new image in the pod definition file that we used in the last question.

SOLUTION >> Simply edit the static pod definition file and save it. If that does not re-create the pod, run: 

```bash
kubectl run --restart=Never --image=busybox:1.28.4 static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```


10. We just created a new static pod named static-greenbox. Find it and delete it.

This question is a bit tricky. But if you use the knowledge you gained in the previous questions in this lab, you should be able to find the answer to it.

CheckCompleteIncomplete
Static pod deleted

SOLUTION >> 

First, let's identify the node in which the pod called static-greenbox is created. To do this, run:
root@controlplane:~# kubectl get pods --all-namespaces -o wide  | grep static-greenbox
default       static-greenbox-node01                 1/1     Running   0          19s     10.244.1.2   node01       <none>           <none>
root@controlplane:~#
From the result of this command, we can see that the pod is running on node01.


Next, SSH to node01 and identify the path configured for static pods in this node.
Important: The path need not be /etc/kubernetes/manifests. Make sure to check the path configured in the kubelet configuration file.
root@controlplane:~# ssh node01 
root@node01:~# ps -ef |  grep /usr/bin/kubelet 
root       752   654  0 00:30 pts/0    00:00:00 grep --color=auto /usr/bin/kubelet
root     28567     1  0 00:22 ?        00:00:11 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --network-plugin=cni --pod-infra-container-image=k8s.gcr.io/pause:3.2
root@node01:~# grep -i staticpod /var/lib/kubelet/config.yaml
staticPodPath: /etc/just-to-mess-with-you
root@node01:~# 
Here the staticPodPath is /etc/just-to-mess-with-you


Navigate to this directory and delete the YAML file:
root@node01:/etc/just-to-mess-with-you# ls
greenbox.yaml
root@node01:/etc/just-to-mess-with-you# rm -rf greenbox.yaml 
root@node01:/etc/just-to-mess-with-you#
Exit out of node01 using CTRL + D or type exit. You should return to the controlplane node. Check if the static-greenbox pod has been deleted:
root@controlplane:~# kubectl get pods --all-namespaces -o wide  | grep static-greenbox
root@controlplane:~# 
