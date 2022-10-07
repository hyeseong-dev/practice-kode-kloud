1. how many services exist in default namespace?

2. 1번의 서비스의 타입은 무엇인가?
- 추가 참고 : 여러 타입에 대한 내용
- 링크 : https://kim-dragon.tistory.com/52

3. 쿠버네티스 서비스의 타겟 포트는?
- 야믈 파일로 출력을 파이프를 통해 받아서 그랩하여 처리 

4. How many labels are configured on the kubernetes service?

USE describe cli to specific service name to find lables
but what is Labels? and what are differences between yaml file label and this label?

```BASH
controlplane ~ ➜  k describe service/kubernetes 
Name:              kubernetes
Namespace:         default
Labels:            component=apiserver
                   provider=kubernetes
Annotations:       <none>
Selector:          <none>
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.43.0.1
IPs:               10.43.0.1
Port:              https  443/TCP
TargetPort:        6443/TCP
Endpoints:         10.2.100.9:6443
Session Affinity:  None
Events:            <none>
```

5. How many Endpoints are attached on the kubernetes service?
- HINT >> Run the command: kubectl describe service and look at the Endpoints.

6. How many Deployments exist on the system now?
In the current(default) namespace 

7. What is the image used to create the pods in the deployment?
- HINT >> Run the command: kubectl describe deployment and look under the containers section.
controlplane ~ ➜  k describe deployments.apps simple-webapp-deployment


8. 
9. 
10. Create a new service to access the web application using the service-definition-1.yaml file.


Name: webapp-service
Type: NodePort
targetPort: 8080
port: 8080
nodePort: 30080
selector:
name: simple-webapp

```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 8080
      port: 8080
      nodePort: 30080
  selector:
    name: simple-webapp
```

11. 