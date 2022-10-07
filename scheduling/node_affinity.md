1. How many Labels exist on node node01?

2. Apply a label color=blue to node node01
3. 
4. 
5. The elephant pod runs a process that consume 15Mi of memory. Increase the limit of the elephant pod to 20Mi.

Delete and recreate the pod if required. Do not modify anything other than the required fields.

CheckCompleteIncompleteNext
Pod Name: elephant

Image Name: polinux/stress

Memory Limit: 20Mi

Create the file elephant.yaml by running command kubectl get po elephant -o yaml > elephant.yaml and edit the file such as memory limit is set to 20Mi as follows:
```yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: elephant
  namespace: default
spec:
  containers:
  - args:
    - --vm
    - "1"
    - --vm-bytes
    - 15M
    - --vm-hang
    - "1"
    command:
    - stress
    image: polinux/stress
    name: mem-stress
    resources:
      limits:
        memory: 20Mi
      requests:
        memory: 5Mi
```
then run kubectl replace -f elephant.yaml --force. This command will delete the existing one first and recreate a new one from the YAML file.

6. 
7. 
8. 
9. 
10. 
11. 