* 08.6 자동 복구

  * `학습 환경 2` 대신, minikube에서 테스트하기 위해, 다음의 명령 실행
  ```
    minikube delete                 	# Network Policy를 지원하는 CNI(Container Network Interface) 플러그인으로의 교체를 위해, 기존의 클러스터 삭제
    minikube start -n 3 --cni=calico	# calico 네트워크 플러그인을 활성화하는 새 클러스터 생성 및 node 3개 생성
  ```
