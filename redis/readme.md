1) Redis 는 어떤 것이고 어떤 식으로 사용할 수 있는가?
2) Reids 기본 기능
3) Redis 운영시 장애 포인트등 잘 쓰는법

### Cache first

Cache 는 나중에 요청을 미리 저쟁하 두었다가 빠르게 서비스를 해주는 것을 의미

### 아주 추상적인 웹서비스 구조

Client -> Web Server -> DB

DB 안에는 많은 데이터들이 있고, 이 때 주로 디스크에 내용이 저장되게 됩니다.

| 2:8 파레토 법칙

전체 요청의 80% 는 20%의 사용자가 요구하고 있다.

### Look Aside Cache

![look_aside_cache.png](look_aside_cache.png)

1. Web Server 는 데이터가 존재하는지 Cache 먼저 확인
2. Cache 에 데이터가 있으면 Cache 에서 가져온다.
3. Cache 에 데이터가 없다면 DB 에서 얻어온다.
4. DB 에서 얻어온 데이터를 Cache 에 다시 저장한다.




