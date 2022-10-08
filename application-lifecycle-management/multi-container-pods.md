1.Identify the number of containers created in the red pod.

- 1 
- 2
- 3
- 4 

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

2.  Identify the name of the containers running in the blue pod.

- orange & yellow
- teal & navy
- grey & white
- Red & green

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

3. Create a multi-container pod with 2 containers.

Use the spec given below.
If the pod goes into the crashloopbackoff then add the command sleep 1000 in the lemon container.

CheckCompleteIncomplete
Name: yellow

- Container 1 Name: lemon
- Container 1 Image: busybox
- Container 2 Name: gold
- Container 2 Image: redis

HINT >> 
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

Solution manifest file to create a multi-container pod called yellow as follows:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: yellow
spec:
  containers:
  - name: lemon
    image: busybox
    command:
      - sleep
      - "1000"

  - name: gold
    image: redis
```

4. We have deployed an application logging stack in the elastic-stack namespace. Inspect it.
Before proceeding with the next set of questions, please wait for all the pods in the elastic-stack namespace to be ready. This can take a few minutes.

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
