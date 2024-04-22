# express-session MySQL

express-mysql-session 모듈은 express-session의 세션 정보를 MySQL에 저장할 수 있도록 도와주는 모듈임.

express-session을 이용해 서버를 재실행 할 때마다 세션 정보가 초기화되는 문제 발생, 이는 express-session이 기본적으로 세션 정보를 인 메모리(In-Memory)에 저장하기 때문에 발생하는 문제로, 서버가 종료될 때 마다 이전에 생성된 세션 정보가 사라지게 됨.
이러한 문제를 해결하기 위해, 외부 세션 스토리지를 사용하여 서버가 종료되더라도 사용자의 세션 정보가 외부 스토리지에 영구적으로 남을 수 있도록 리팩토링을 해야함.
이를 위해 MySQL를 외부 세션 스토리지로 사용하여, 사용자의 세션 정보를 MySQL에 저장하고 관리할 수 있도록 프로젝트를 개선해야함.

```
# 외부 세션 스토리지를 사용하기 위한, express-mysql-session 설치 명령어
yarn add express-mysql-session
```

express-mysql-session 모듈의 가장 큰 문제점은 세션 ID로 정보를 조회할 때마다 MySQL의 조회 쿼리를 매번 실행한다는 점임.
이러한 문제를 해결하기 위한 다양한 방법들이 존재하는데, 이전에 사용한 JWT 쿠키를 이용하는 것도 하나의 방법이며, 외부 세션 스토리지를 캐시 메모리 데이터베이스인 Redis로 변경하는 것도 해결책 중 하나.
따라서, 어떤 기술 스택을 선택할지는 현재 상황에서 가장 효율적이고, 적합한 기술을 선택하는 것이 중요
예를 들어, 외부 세션 스토리지 사용을 원하지 않는다면, JWT 쿠키를 사용할 수 있으며, 성능 개선이 필요하다면 Redis를 도입하는 것처럼 방법은 여러가지가 있음.
//