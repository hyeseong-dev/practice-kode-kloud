1. Let us deploy metrics-server to monitor the PODs and Nodes. Pull the git repository for the deployment files.

Run: git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git


Ok

HINT >> 꿀팁! 
컨트롤 + 시프트 + 브이 명령어를 통해서 코드클라우드 실습환경에 붙여넣기 기능을 사용할 수 있음.

```bash

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

SOLUTION >>


```bash

```


```yaml

```

3. Deploy the metrics-server by creating all the components downloaded.

Run the kubectl create -f . command from within the downloaded repository.

CheckCompleteIncomplete
Metrics server deployed?

HINT >> 특정 디렉토리 지정(절대, 상대경로)시 그 안의 파일을 읽어서 한번에 다수의 인스턴스를 생성시켜줌

```bash
k create -f .
```

SOLUTION >>


```bash

```


```yaml

```

4. It takes a few minutes for the metrics server to start gathering data.

Run the kubectl top node command and wait for a valid output.

HINT >> 

```bash

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

SOLUTION >>


```bash

```


```yaml

```

6. Identify the node that consumes the most Memory.

- node01
- node03
- controlplane
- node02

HINT >> Run the 'kubectl top node' command and identify the node that uses the most memory.

```bash

```

SOLUTION >>
You can also use the --sort-by='memory' flag like this:
```bash
root@controlplane:~# kubectl top node --sort-by='memory' --no-headers | head -1 
controlplane   183m   2%    662Mi   3%    
root@controlplane:~# 
```
Here we have used head -1 command to print the node first in the sorted order, which is the one that uses the most memory.

NOTE: The result you see above is just an example. The actual values may differ from what you see here.


7. Identify the POD that consumes the most Memory.

rabbit
tiger
lion
elephant

HINT >> Run the 'kubectl top pod' command and identify the pod that uses the most memory.

```bash

```

SOLUTION >> You can also use the --sort-by='memory' flag like this:

```bash
root@controlplane:~# kubectl top pod --sort-by='memory' --no-headers | head -1 
rabbit     134m   201Mi   
root@controlplane:~# 
```
Here we have used head -1 command to print the pod first in the order, which is the one that uses the most memory.

NOTE: The result you see above is just an example. The actual values may differ from what you see here.




```bash

```


```yaml

```

8. Identify the POD that consumes the least CPU.



lion
tiger
rabbit
elephant

HINT >> 상기 동일

```bash

```

SOLUTION >> 상기 유형과 동일 


```bash

```


```yaml

```

9. 

HINT >> 

```bash

```

SOLUTION >>


```bash

```


```yaml

```

