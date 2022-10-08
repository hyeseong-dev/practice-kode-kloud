1. How many Secrets exist on the system?
In the current(default) namespace.


3
4
2
1
0

HINT >> Inspect the secrets in the default namespace using the kubectl get command.
```bash
```

```yaml

```
SOLUTION >> Run the command: kubectl get secrets and count the number of secrets.
```bash
```

```yaml

```

2.  How many secrets are defined in the dashboard-token secret?

5
2
0
4
3
1

HINT >> Use the kubectl describe command and inspect the secret.
```bash
```

```yaml

```
SOLUTION >> Run the command: kubectl describe secrets dashboard-token and look at the data field.
There are three secrets - ca.crt, namespace and token.


```bash
```

```yaml

```

3. What is the type of the dashboard-token secret?

- kubernetes.io/service-account-token
- Secret
- Opaque

HINT >> look into with describe cli 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

4. 

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

5. We are going to deploy an application with the below architecture

We have already deployed the required pods and services. Check out the pods and services created. Check out the web application using the Webapp MySQL link above your terminal, next to the Quiz Portal Link.

Ok

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

6. The reason the application is failed is because we have not created the secrets yet. Create a new secret named db-secret with the data given below.

You may follow any one of the methods discussed in lecture to create the secret.

- Secret Name: db-secret
- Secret 1: DB_Host=sql01
- Secret 2: DB_User=root
- Secret 3: DB_Password=password123



HINT >> Secrets can be easily created using imperative commands.
Use the kubectl create secret command with the --from-literal to pass in the secret data in the form of key value pairs.

You may also create the secret using a YAML file.
```bash
```

```yaml

```
SOLUTION >> Run the command: 
```bash
kubectl create secret generic db-secret \
  --from-literal=DB_Host=sql01 \
  --from-literal=DB_User=root \
  --from-literal=DB_Password=password123
```

```bash
```

```yaml

```

7. Configure webapp-pod to load environment variables from the newly created secret.
Delete and recreate the pod if required.

- Pod name: webapp-pod
- Image name: kodekloud/simple-webapp-mysql
- Env From: Secret=db-secret

HINT >> Expose the secret as an environment variable to be used the webapp-pod pod.

Refer the documentation by clicking the tab called Use Secrets in a Pod
```bash
```

```yaml

```
SOLUTION >> 
Add the secret in the pod spec as below:

```yaml
---
apiVersion: v1 
kind: Pod 
metadata:
  labels:
    name: webapp-pod
  name: webapp-pod
  namespace: default 
spec:
  containers:
  - image: kodekloud/simple-webapp-mysql
    imagePullPolicy: Always
    name: webapp
    envFrom:
    - secretRef:
        name: db-secret
```
      
Recreate the pod.

```bash
```

```yaml

```

8. 

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

9. 

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

10. 

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

11. 

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```
