@Configuration 어노테이션에서는 proxyBeanMethods 속성이 있다.

기본: proxyBeanMethods = true 이다.

proxyBeanMethods 은 런타임에 동적으로 @Bean 메서드 반환값이 객체를 프록시로 생성할지 말지를 컨트롤한다.

프록시가 하는 역할은 내부에 있는 @Bean 이 한 번만 생성되도록 관리한다
proxyBeanMethods 가 true 인 경우에는 아래의 코드에서 new SomeBean() 이 딱 한번만 호출되도록 관리할 수 있다.
반대로 false 인 경우는 프록시가 생성되지 않아 new SomeBean()이 두번 실행된다.

이때 프록시 생성 비용이 성능적인 이슈가 있어서 굳이 @Bean 이 하나 있거나 여러번 생성해도 부담이 없을 경우에는 프록시를 생성하지 않아도된다.


```
@Configuration
public class Config {

  @Bean
  SomeBean someBean() {
    return new SomeBean(); 
  }

  @Bean
  NothingBean nothingBean() {
    return new NothingBean(someBean());
  }
}
```


[참고자료1](https://tecoble.techcourse.co.kr/post/2021-10-14-springboot-autoconfiguration/)
[참고자료2](https://github.com/spring-projects/spring-boot/issues/9068)
