
8. Update the pod red to use an initContainer that uses the busybox image and sleeps for 20 seconds
Delete and re-create the pod if necessary. But make sure no other configurations change.


- Pod: red

initContainer Configured Correctly

SOLUTION >> 

Add initContainers section in the pod spec as below:
```yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: red
  namespace: default
spec:
  containers:
  - command:
    - sh
    - -c
    - echo The app is running! && sleep 3600
    image: busybox:1.28
    name: red-container
  initContainers:
  - image: busybox
    name: red-initcontainer
    command: 
      - "sleep"
      - "20"
```
Recreate the pod.

9. A new application orange is deployed. There is something wrong with it. Identify and fix the issue.
Once fixed, wait for the application to run before checking solution.

- Issue fixed

HINT >> Check the command used by the initContainer and correct it.

SOLUTION >> There is a typo in the command used by the initContainer. To fix this, first get the pod definition file by running kubectl get pod orange -o yaml > /root/orange.yaml.
Next, edit the command and fix the typo.
Then, delete the old pod by running kubectl delete pod orange
Finally, create the pod again by running kubectl create -f /root/orange.yaml


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
