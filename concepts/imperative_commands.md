1. controlplane ~ ➜  k run nginx-pod --image=nginx:alpine
pod/nginx-pod created

2.  Deploy a redis pod using the redis:alpine image with the labels set to tier=db.
Either use imperative commands to create the pod with the labels. Or else use imperative commands to generate the pod definition file, then add the labels before creating the pod using the file.

controlplane ~ ➜  k run redis --image=redis:alpine -l tier=db
pod/redis created

3. Create a service redis-service to expose the redis application within the cluster on port 6379.
Use imperative commands.

HINT >> Use the kubectl expose command.

controlplane ~ ✖ k expose pod redis --name=redis-service --port=6379 --type=ClusterIP
service/redis-service exposed

!!! EXPOSE 명령어가 서비스 생성 명령어이기도함 

4. Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.
Try to use imperative commands only. Do not create definition files.
CheckCompleteIncomplete

k create deploy webapp --image=kodekloud/webapp-color --replicas=3

5. Create a new pod called custom-nginx using the nginx image and expose it on container port 8080.
CheckCompleteIncomplete

서비스를 생성하라는 문제의 의도가 없으므로 


6. Create a new namespace called dev-ns.
Use imperative commands.

7. Create a new deployment called redis-deploy in the dev-ns namespace with the redis image. It should have 2 replicas.
Use imperative commands.

controlplane ~ ✖ k create deploy redis-deploy -n dev-ns --image=redis --replicas=2
deployment.apps/redis-deploy created

8. Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.
Try to do this with as few steps as possible.

controlplane ~ ✖ k run httpd --image=httpd:alpine -n default
pod/httpd created

controlplane ~ ✖ k create deploy redis-deploy -n dev-ns --image=redis --replicas=2
deployment.apps/redis-deploy created

9. 

10.

