
1. 

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

2.  What is the environment variable name set on the container in the pod?

- APP
- pink
- APP-COLOR
- APP_COLOR
- Sleep
- COLOR

HINT >>
- Run the command kubectl describe pod and look for ENV option
- or can access with exec command with -- 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

3. 

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

5. 

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

6. 

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

7. 

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

9. Create a new ConfigMap for the webapp-color POD. Use the spec given below.

- ConfigName Name: webapp-config-map
- Data: APP_COLOR=darkblue 

HINT >> You can use the kubectl create configmap command.
```bash
```

```yaml

```
SOLUTION >> Run the command kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue
```bash
```

```yaml

```

10. Update the environment variable on the POD to use the newly created ConfigMap

Note: Delete and recreate the POD. Only make the necessary changes. Do not modify the name of the Pod.

 Pod Name: webapp-color
 EnvFrom: webapp-config-map

HINT >> Set the environment option to envFrom and use configMapRef webapp-config-map.
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

Update the Pod spec to use the configMap as below:
```yaml
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-color
  name: webapp-color
  namespace: default
spec:
  containers:
  - envFrom:
    - configMapRef:
         name: webapp-config-map
    image: kodekloud/webapp-color
    name: webapp-color
```
Recreate the pod.

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
