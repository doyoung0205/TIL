Circuit Breaker가 필요한 이유는, 누전차단기가 전기사고가 발생하기 전에 전기를 미리 차단하는것과 동일하게,
문제가 있는 마이크로서비스로의 트래픽을 차단하여 전체서비스가 느려지거나 중단되는것을 미리 방지하기 위해서 입니다.

Spring Cloud 커뮤니티에서는 EOS(End Of Service: 더 이상 업그레이드와 지원 없음)된 Hystrix의 대안으로 Resilience4J를 권고

Resilience4J는 Java 전용으로 개발된 경량화된 Fault Tolerance(장애감내) 제품입니다.
Resilience4J는 아래 6가지 핵심모듈로 구성되어 있습니다.

- Circuit Breaker: Count(요청건수 기준) 또는 Time(집계시간 기준)으로 Circuit Breaker제공
- Bulkhead: 각 요청을 격리함으로써, 장애가 다른 서비스에 영향을 미치지 않게 함(bulkhead-격벽이라는 뜻)
- RateLimiter: 요청의 양을 조절하여 안정적인 서비스를 제공. 즉, 유량제어 기능임.
- Retry: 요청이 실패하였을 때, 재시도하는 기능 제공
- TimeLimiter: 응답시간이 지정된 시간을 초과하면 Timeout을 발생시켜줌
- Cache: 응답 결과를 캐싱하는 기능 제공
