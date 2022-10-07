
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

2.  

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

3. Create a pod with the ubuntu image to run a container to sleep for 5000 seconds. Modify the file ubuntu-sleeper-2.yaml.
Note: Only make the necessary changes. Do not modify the name.

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 배열의 값을 문자열로 입력할것(아님 오류 발생)
```bash
```

```yaml
---
apiVersion: v1 
kind: Pod 
metadata:
  name: ubuntu-sleeper-2 
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command:
      - "sleep"
      - "5000"
```

4. Create a pod using the file named ubuntu-sleeper-3.yaml. There is something wrong with it. Try to fix it!
Note: Only make the necessary changes. Do not modify the name.
CheckCompleteIncomplete
Pod Name: ubuntu-sleeper-3
Command: sleep 1200

HINT >> 상기 3번과 동일한 유형 문제
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

5. Update pod ubuntu-sleeper-3 to sleep for 2000 seconds.
Note: Only make the necessary changes. Do not modify the name of the pod. `Delete and recreate the pod if necessary.`

- Pod Name: ubuntu-sleeper-3
- Command: sleep 2000

HINT >> 상기 4번과 동일한 유형의 문제이지만 팟을 메뉴얼하게 삭제하고 다시 생성해야함.
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

10. Create a pod with the given specifications. By default it displays a blue background. Set the given command line arguments to change it to green.

- Pod Name: webapp-green
- Image: kodekloud/webapp-color
- Command line arguments: --color=green

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml
---
apiVersion: v1 
kind: Pod 
metadata:
  name: webapp-green
  labels:
      name: webapp-green 
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    args: ["--color", "green"]
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
