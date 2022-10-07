
1. We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment (env)?
Use selectors to filter the output

힌트 -> --selector flag를 통해서 키와값을 매칭시킬수 있음

k get pods --selector env=dev | wc -l

2.  How many PODs are in the finance business unit (bu)?

controlplane ~ ➜  k get pods --selector bu=finance | wc -l

3. How many objects are in the prod environment including PODs, ReplicaSets and any other objects?

힌트 : kubectl get all --selector env=prod
정답 : kubectl get all --selector env=prod --no-headers | wc -l

4. Identify the POD which is part of the prod environment, the finance BU and of frontend tier?

힌트 : Run the command kubectl get all --selector env=prod,bu=finance,tier=frontend
절대 셀렉터 키의 값의 콤마들을 스페이스바로 띄우지 않음!!!

5. A ReplicaSet definition file is given replicaset-definition-1.yaml. Try to create the replicaset. There is an issue with the file. Try to fix it.

CheckCompleteIncomplete

Update the /root/replicaset-definition-1.yaml file as follows:

```yaml


---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
   name: replicaset-1
spec:
   replicas: 2
   selector:
      matchLabels:
        tier: front-end
   template:
     metadata:
       labels:
        tier: front-end
     spec:
       containers:
       - name: nginx
         image: nginx 
```
Then run kubectl apply -f replicaset-definition-1.yaml

spec 아래의 SELECTOR > MATCHLABELS > TIER와 template > metadata > labels > tier간의 차이가 무엇인가? 

6. 

7. 

8. 

9. 

10. 

