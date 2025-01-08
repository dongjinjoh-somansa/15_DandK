* SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client 해결 방법

  * 다음의 명령 실행
  ```
    docker exec -it mysql bash

    mysql -u root -p

    mysql> update mysql.user set plugin='mysql_native_password';
    mysql> alter user root identified with mysql_native_password by 'qwerty';
  ```

