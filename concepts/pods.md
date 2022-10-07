1. POD 조회 명령어 
```bash
k get po
```

2. 팟들중에 가장 최근에 생성된 이미지는?
```bash

```

3. 팟이 생성된 노드는?
```bash
k describe pods | grep NODE -i
```

4. 특정 팟안의 컨테이너 개수 파악.
```bash
k get pod/webapp
```

5. What images are used in the new webapp pod?
```bash
k describe pod/webapp 
```

6. What is the state of the container agentx in the pod webapp?
```bash


```

7. 특정 팟의 컨테이너 상태 확인 명령어?
```bash

```

8. 컨테이너 오류 상태
```bash

```
10. get pods 명령어의 ready 컬럼이 의미하는 건
```bash

```

11. 특정 팟 제거 명령어
```bash
k delete pods/webapp
```

12. 특정 이미지를 특정 이름의 팟 생성
13. 생성된 팟의 컨테이너 이미지 변경
14. 간단하게 명령어를 이용하여 팟 이미지 변경