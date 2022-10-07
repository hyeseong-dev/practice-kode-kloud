# 다중 스케쥴링

1. What is the name of the POD that deploys the default kubernetes scheduler in this environment?

- scheduler
- kube-scheduler
- kube-scheduler-controlplane
- etcd-master


힌트 >> Run the command 
```bash
kubectl get pods --namespace=kube-system
```

솔루션 >> 

2. What is the image used to deploy the kubernetes scheduler?

Inspect the kubernetes scheduler pod and identify the image


- k8s.gcr.io/kube-scheduler:v1.24.0
- scheduler:1.0
- kube-scheduler:1.13

힌트 >> Run the command 
```bash
kubectl describe pod kube-scheduler-controlplane --namespace=kube-system
```

솔루션 >> 

3. We have already created the ServiceAccount and ClusterRoleBinding that our custom scheduler will make use of.


Checkout the following Kubernetes objects:

ServiceAccount: my-scheduler (kube-system namespace)
ClusterRoleBinding: my-scheduler-as-kube-scheduler
ClusterRoleBinding: my-scheduler-as-volume-scheduler

Run the command: kubectl get serviceaccount -n kube-system & kubectl get clusterrolebinding

Note: - Don't worry if you are not familiar with these resources. We will cover it later on.

힌트 >> 

솔루션 >> 

4. Let's create a configmap that the new scheduler will employ using the concept of ConfigMap as a volume.
Create a configmap with name my-scheduler-config using the content of file /root/my-scheduler-config.yaml

CheckCompleteIncomplete
ConfigMap my-scheduler-config created ?

힌트 >> Use the imperative command to create the configmap with option --from-file

솔루션 >> Run the below command to create the configMap:

```bash
kubectl create -n kube-system configmap my-scheduler-config --from-file=/root/my-scheduler-config.yaml
```


5. Deploy an additional scheduler to the cluster following the given specification.

Use the manifest file provided at /root/my-scheduler.yaml. Use the same image as used by the default kubernetes scheduler.

CheckCompleteIncomplete
Name: my-scheduler

Status: Running

Correct image used?

힌트 >> Use the file at /root/my-scheduler.yaml to create your own scheduler with correct image.

솔루션 >> 

The final YAML file would look something like this:

```yaml
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: my-scheduler
  name: my-scheduler
  namespace: kube-system
spec:
  serviceAccountName: my-scheduler
  containers:
  - command:
    - /usr/local/bin/kube-scheduler
    - --config=/etc/kubernetes/my-scheduler/my-scheduler-config.yaml
    image: k8s.gcr.io/kube-scheduler:v1.24.0 # changed
    livenessProbe:
      httpGet:
        path: /healthz
        port: 10259
        scheme: HTTPS
      initialDelaySeconds: 15
    name: kube-second-scheduler
    readinessProbe:
      httpGet:
        path: /healthz
        port: 10259
        scheme: HTTPS
    resources:
      requests:
        cpu: '0.1'
    securityContext:
      privileged: false
    volumeMounts:
      - name: config-volume
        mountPath: /etc/kubernetes/my-scheduler
  hostNetwork: false
  hostPID: false
  volumes:
    - name: config-volume
      configMap:
        name: my-scheduler-config
```
Run kubectl create -f my-scheduler.yaml and wait sometime for the container to be in running state.

6. A POD definition file is given. Use it to create a POD with the new custom scheduler.

File is located at /root/nginx-pod.yaml


힌트 >> Set schedulerName property on pod specification to the name of the new scheduler

솔루션 >> 
Set schedulerName property on pod specification as my-scheduler.
```yaml
---
apiVersion: v1 
kind: Pod 
metadata:
  name: nginx 
spec:
  schedulerName: my-scheduler
  containers:
  - image: nginx
    name: nginx
```
Run kubectl create -f nginx-pod.yaml