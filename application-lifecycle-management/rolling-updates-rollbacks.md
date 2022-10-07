
1. We have deployed a simple web application. Inspect the PODs and the Services
Wait for the application to fully deploy and view the application using the link called Webapp Portal above your terminal.

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

2.  What is the current color of the web application?

Access the Webapp Portal.


- yellow
- red
- orange
- green
- blue

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

3. Run the script named curl-test.sh to send multiple requests to test the web application. Take a note of the output.
Execute the script at /root/curl-test.sh.

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

5. What container image is used to deploy the applications?

- kodekloud
- webapp
- kodekloud/webapp-color:v2
- kodekloud/webapp-color:v1
- simple-webapp

HINT >> k describe deployments frontend | grep -i image
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

6. Inspect the deployment and identify the current strategy


RollBack
ReCreate
RollOut
RollingUpdate

HINT >> Run the command kubectl describe deployment and look at StrategyType
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

7. If you were to upgrade the application now what would happen?
All PODs are taken down before upgrading any
PODs are upgraded few at a time

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

8. Let us try that. Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v2
Do not delete and re-create the deployment. Only set the new image name for the existing deployment.
CheckCompleteIncomplete

- Deployment Name: frontend
- Deployment Image: kodekloud/webapp-color:v2

HINT >> Run the command kubectl edit deployment frontend and modify the required feild
```bash
```

```yaml

```
SOLUTION >> 
```bash
```

```yaml

```

9. Run the script curl-test.sh again. Notice the requests now hit both the old and newer versions. However none of them fail.
Execute the script at /root/curl-test.sh.

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

11. Change the deployment strategy to Recreate
Delete and re-create the deployment if necessary. Only update the strategy type for the existing deployment.


- Deployment Name: frontend
- Deployment Image: kodekloud/webapp-color:v2
- Strategy: Recreate

HINT >> Run the command kubectl edit deployment frontend and modify the required field. Make sure to delete the properties of rollingUpdate as well, set at strategy.rollingUpdate.
```bash
```

```yaml

```
SOLUTION >> The stratergy section should be as shown below:


```bash
```

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  namespace: default
spec:
  replicas: 4
  selector:
    matchLabels:
      name: webapp
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        name: webapp
    spec:
      containers:
      - image: kodekloud/webapp-color:v2
        name: simple-webapp
        ports:
        - containerPort: 8080
          protocol: TCP
```

12. Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v3
Do not delete and re-create the deployment. Only set the new image name for the existing deployment.

CheckCompleteIncomplete
- Deployment Name: frontend
- Deployment Image: kodekloud/webapp-color:v3

HINT >> Run the command: kubectl edit deployment frontend and modify the required field
```bash
```

```yaml

```
SOLUTION >> Run the command: kubectl edit deployment frontend and modify the image to kodekloud/webapp-color:v3.
Next, save and exit. The pods should be recreated with the new image.

Note that all pods will be terminated and recreated simultaneously this time.


```bash
```

```yaml

```

13. Run the script curl-test.sh again. Notice the failures. Wait for the new application to be ready. Notice that the requests now do not hit both the versions
Execute the script at /root/curl-test.sh.

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

14. 

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

15. 

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

16. 

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