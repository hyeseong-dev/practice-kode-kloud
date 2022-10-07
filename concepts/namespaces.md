- How many Namespaces exist on the system?

```bash
controlplane ~ ✖ k get namespaces | wc -l
```

# CREATE , RUN, APPLY 차이점 
 https://kingofbackend.tistory.com/163

run과 create 비교
run은 파드 1개만 생성하고 관리해줍니다.

create는 그룹 내 파드 1개를 생성하고 관리해줍니다.

 

run으로 생성한 파드는 초코파이1개이고, create로 생성한 파드는 초코파이 박스 안에 있는 초코파이1개입니다.

 

create과 apply 비교
오브젝트가 디플로이먼트 일 경우 replicas 를 지정해주어서 파드의 갯수를 보장받을 수 있습니다.

 

만약 create를 이용하여 디플로이먼트 생성했을 경우 yaml 파일에서 replicas를 3개로 지정해주었다면 디플로이먼트의 갯수는 3개로 보장됩니다. 하지만 만약 더 추가하고 싶어서 yaml에서 replicas가 3개였던 걸을 6개로 늘려주었습니다. 

 

이후 create를 이용하여 다시 디플로이먼트로 생성해주먼 에러가 발생합니다. 이미 디플로이먼트가 존재하는 에러가 발생하죠.

 

이렇듯 create로 디플로이먼트를 생성하게 된다면 추후 수정이 불가능합니다. 

 

반면에, replicas를 6개로 바꿔준 후 apply 명령어를 통해 디플로이먼트를 생성해준다면 파드의 일관성 문제로 경고가 뜨긴 하지만 6개의 파드가 생성된걸 확인할 수 있습니다.

 

이렇듯 apply는 추후 오브젝트의 수정이 가능하고 create는 수정이 불가능합니다. 따라서 변경 가능성이 있는 복잡한 오브젝트는 yaml 파일로 스펙을 작성한 후 apply로 오브젝트를 생성하는 것이 좋습니다.

 

구분	Run	Create	Apply
명령 실행	제한적임	가능함	안됨
파일 실행	안됨	가능함	가능함
변경 가능	안됨	안됨	가능함
실행 편의성	매우 좋음	매우 좋음	좋음
기능 유지	제한적임	지원됨	다양하게 지원됨
- 

3. Create a POD in the finance namespace.
Use the spec given below.
### 틀린 이유 : 런 명령어로 생성하려했기 때문인듯?
그럼 정말 크리에잇으로는 팟 생성이 안되는 건가?

```BASH
controlplane ~ ➜  k create -n finance pod redis --image=redis
error: unknown flag: --image
See 'kubectl create --help' for usage.

controlplane ~ ✖ k create -n finance pod redis --image:redis
error: unknown flag: --image:redis
See 'kubectl create --help' for usage.

controlplane ~ ✖ k run -n finance pod redis --image=redis
```
- 정답
```bash
controlplane ~ ➜  k run -n finance redis --image=redis
pod/redis created
```

4. Which namespace has the blue pod in it?
Run the command kubectl get pods --all-namespaces

5. Access the Blue web application using the link above your terminal!!
From the UI you can ping other services.

6. What DNS name should the Blue application use to access the database db-service in its own namespace - marketing?
You can try it in the web application UI. Use port 6379.

```BASH
controlplane ~ ➜  k get all -n marketing
NAME           READY   STATUS    RESTARTS   AGE
pod/redis-db   1/1     Running   0          20m
pod/blue       1/1     Running   0          20m

NAME                   TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
service/blue-service   NodePort   10.43.81.35   <none>        8080:30082/TCP   20m
service/db-service     NodePort   10.43.81.7    <none>        6379:31750/TCP   20m
```

7. What DNS name should the Blue application use to access the database db-service in the dev namespace?

You can try it in the web application UI. Use port 6379.
