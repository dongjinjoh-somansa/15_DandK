# 실습 시 참고할 내용
## 12.2
### 352p
minikube를 다음과 같이 실행한다. (node 3개 생성, CNI로 Flannel 사용)
~~~
$ minikube start -n 3 --cni=flannel
~~~

## 12.3
### 355p
다음의 사유로 인해, 이후로는 `mysql-sts.yml` 대신 `mysql-sts-affinity-novolume.yml`을 사용한다.
* node 삭제를 수행하기 위해서는 pod가 worker node에 생성되어야 한다. 따라서 pod가 생성될 worker node를 `affinity`로 지정하는 것으로 한다.
* `hostpath`는 node의 파일 시스템을 참조하므로 multi node를 사용하는 경우는 사용할 수 없다. 하여, PV와 PVC는 생성하지 않도록 한다.

### 356p
drain이 실패하는 경우가 있어, drain 시 `--force`를 붙여준다.
~~~
$ kubectl drain <node> --ignore-daemonsets --force
~~~

## 12.4
### 356p
minikube에서 node를 중지하려면 다음과 같이 수행한다.
~~~
$ minikube node stop <node>
~~~
 
### 357p
`kubectl delete node <node>` 명령으로 node를 삭제한 경우 minikube에서는 삭제된 node에 대한 제어가 불가하여, 모든 객체들을 삭제하고 새로 만들어야 한다.
~~~
$ minikube delete
$ minikube start -n 3 --cni=flannel
~~~
