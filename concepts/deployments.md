1. How many PODs exist on the system?
In the current(default) namespace.

controlplane ~ ➜  k get po -n default 
No resources found in default namespace.

2. How many ReplicaSets exist on the system?
In the current(default) namespace.

controlplane ~ ✖ k get rs -n default 
No resources found in default namespace.

3. How many Deployments exist on the system?
In the current(default) namespace.

controlplane ~ ✖ k get deploy -n default 
No resources found in default namespace.

4. How many ReplicaSets exist on the system now?

5. What is the image used to create the pods in the new deployment?
controlplane ~ ➜  k describe deploy

6. Why do you think the deployment is not ready?
controlplane ~ ➜  k logs deployments/frontend-deployment 
Found 4 pods, using pod/frontend-deployment-6d8c45b946-gmfm5
Error from server (BadRequest): container "busybox-container" in pod "frontend-deployment-6d8c45b946-gmfm5" is waiting to start: trying and failing to pull image

7. Create a new Deployment using the deployment-definition-1.yaml file located at /root/.
There is an issue with the file, so try to fix it.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-1
spec:
  replicas: 2
  selector:
    matchLabels:
      name: busybox-pod
  template:
    metadata:
      labels:
        name: busybox-pod
    spec:
      containers:
      - name: busybox-container
        image: busybox
        command:
        - sh
        - "-c"
        - echo Hello Kubernetes! && sleep 3600

```

```bash
 k apply -f /root/deployment-definition-1.yaml 
Error from server (BadRequest): error when creating "/root/deployment-definition-1.yaml": deployment in version "v1" cannot be handled as a Deployment: no kind "deployment" is registered for version "apps/v1" in scheme "k8s.io/apimachinery@v1.24.1-k3s1/pkg/runtime/scheme.go:100"
```

kind의 값은 대소문자 구분이 명확해야함.

8. Create a new Deployment with the below attributes using your own deployment definition file.

Name: httpd-frontend;
Replicas: 3;
Image: httpd:2.4-alpine

```bash
controlplane ~ ✖ k create deployment httpd-frontend --image=httpd:2.4-alpine
deployment.apps/httpd-frontend created

controlplane ~ ➜  k scale --replicas=3 deployment httpd-frontend 
deployment.apps/httpd-frontend scaled
```

9. 

