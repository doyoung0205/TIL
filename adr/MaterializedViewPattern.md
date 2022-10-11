Materialized View 패턴 (MV) : 비정규화와 CQRS 를 같이 적용한 케이스
(실제 DBMS의 Materialized view 가 아님)

<Event 기반 Oracle 과 Mongodb 간의 데이터 동기화>
MAIN DB:: Table 에 trigger를 걸어 변경이 일어날 경우 event 테이블에 insert 그리고 배치 어플리케이션이 event 테이블을 보고 중복을 제거하고 카프카에 메시지 발행
MAIN DB 이외 :: Domain API 는 ReadSidePush 어노테이션을 직접 만들어 API 메서드의 어노테이션을 달아 카프카 발행


<캐싱>
EHCache 를 사용한 점 JGroups 을 통한 ec2 들 끼리 캐시 동기화 지원 (Heep메모리 비율 지정가능)


<피처 플래그>
피처 플래그 : Consul (지금의 최신 스프링 부트에서는 되게 간편하게 연동할 수 있음)
DNS기반 ’Service Discovery’ 와 원격 ‘Key/Value Store’ 제공
설정 파일을 원격으로 관리할 수 있음

<주의사항>
‘쓰기’ 쪽 저장소에 변경이 있을 경우 ‘읽기 (MV)’ 쪽에서도 맞춰 변경해야함 (엔카 닷컴의 경우 개발 조직 전체메일을 통해 ‘쓰기’ 쪽 변경을 서로 공유)
’쓰기’ 쪽 대량 업데이트 (Batch) 발생 시 ‘읽기’ 쪽에서도 대량의 업데이트가 일어나므로 대비해야함 (Consumer Capacity, Circuit Breaker)
관리 포인트가 많아짐
SQL 연산 비용이 적거나 실시간 트랜잭션 결과가 중요한 서비스의 경우 ‘EDM’ 이 적절치 않음

<img width="953" alt="스크린샷 2022-10-10 오후 11 03 02" src="https://user-images.githubusercontent.com/39691109/195130443-c9cc9f67-3232-4bfd-9e1e-4794da333b6b.png">
<img width="1293" alt="스크린샷 2022-10-10 오후 11 28 57" src="https://user-images.githubusercontent.com/39691109/195130485-8f5250c0-9377-4779-8321-e3f0b096b68b.png">

