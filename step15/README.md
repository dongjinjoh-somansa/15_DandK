# 실습 시 참고할 내용
## 15.2
### 448p
minikube에서는 profile울 여러 개 생성하면 multi cluster인 것처럼 동작하게 할 수 있다.
profile을 생성하려면 다음과 같이 실행한다.
~~~
$ minikube start -p <profile>
~~~
active profile을 지정하려면 다음과 같이 실행한다.
~~~
$ minikube profile <profile>
~~~
profile을 삭제하려면 다음과 같이 실행한다.
~~~
$ minikube delete -p <profile>
~~~

## 15.4
### 454p
`실행 예 9`의 첫째 줄에 `db_client.yml`를 `reg_secret_env.yml`로 변경한다.

### 455p
`실행 예 10`을 실행하기 전, 다음의 명령을 실행하여 .crt와 .key 파일을 생성한다.
~~~
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt
~~~

### 456p
`실행 예 11`의 첫째 줄에 `apl.yml`를 `secret_volume.yml`로 변경한다.

## 15.5
### 458p
`실행 예 12`의 경우 `step15/config-nginx/prod` 폴더로 이동하고 실행한다.

### 460p
`실행 예 13` 내용 중 다음의 부분들을 변경한다.
* `kubectl apply -f pod.yml`를 `kubectl apply -f cm-env-read.yml`로 변경한다.
* `kubectl exec -it web-apl env`를 `kubectl exec -it web-apl -- env`로 변경한다.

## 15.9
### 474p
`실행 예 18`에서는 토큰 목록을 보여주고 있는데, Kubernetes 1.24부터 토큰이 자동 생성되지 않고 파드가 실행될 때 토큰이 발급되므로, 다음과 같이 실행하여 토큰을 수동으로 발급한다.
~~~
$ cd setup-prod
$ kubectl apply -f secret.yml
$ cd ../setup-test
$ kubectl apply -f secret.yml
~~~

### 475p
`실행 예 20`에서는 개발자용 토큰과 인증서를 파일에 저장하는데, 토큰을 수동으로 생성했으므로 토큰 이름이 예시와 다르다. 하여 대신 다음과 같이 실행한다.
~~~
$ cd developer/
$ kubectl get secret developer-token -n test -o jsonpath={.data.ca\\.crt} | base64 --decode > ca.crt
$ kubectl get secret developer-token -n test -o jsonpath={.data.token} | base64 --decode > token-dev-test.txt
$ kubectl get secret developer-token -n prod -o jsonpath={.data.token} | base64 --decode > token-dev-prod.txt
$ ls
ca.crt			token-dev-prod.txt	token-dev-test.txt
~~~
`실행 예 21`에서는 운영 담당용 토큰과 인증서를 파일에 저장하는데, 토큰을 수동으로 생성했으므로 토큰 이름이 예시와 다르다. 하여 대신 다음과 같이 실행한다.
~~~
$ cd ../operator
$ cp ../developer/ca.crt .
$ kubectl get secret sysop-token -n test -o jsonpath={.data.token} | base64 --decode > token-sysop-test.txt
$ kubectl get secret sysop-token -n prod -o jsonpath={.data.token} | base64 --decode > token-sysop-prod.txt
$ ls
ca.crt			token-sysop-prod.txt	token-sysop-test.txt
~~~

### 486p
`실행 예 33`의 busybox 실행문을 다음과 같이 변경한다.
~~~
kubectl run -it client --image=busybox --restart=Never -- /bin/sh
~~~

### 487p
`실행 예 34`의 busybox 실행문을 다음과 같이 변경한다.
~~~
kubectl run -it client --image=busybox --restart=Never -- /bin/sh
~~~

### 489p
minikube에서는 아래의 명령을 실행하여 host와 minikube 환경 간 tunnel을 뚫어 이를 통해 접근해야 한다.
~~~
minikube tunnel
~~~
위와 같이 실행해 놓은 다음, `https://127.0.0.1`에 접속한다.
