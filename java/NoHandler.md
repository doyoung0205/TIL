### DispatcherServlet 들여다보기

DispatcherServlet의 doDispatch 메소드를 확인해보면, 
mappedHandler가 존재하지 않은 때, noHandlerFound 메소드가 실행된다.


throwExceptionIfNoHandlerFound false 이기 때문에 404의 응답만 보낸다.

@ConfigurationProperties의 설정은 외부 properties에 prefix에 해당하는 값들을 읽어드려 사용할 수 있다. 
즉, application.properties에 설정을 추가하자.
햣

```spring.mvc.throw-exception-if-no-handler-found=true```



하지만, 이 경우에 ResourceHttpRequestHandler 가 매핑되고 있었다.

ResourceHttpRequestHandler 가 매핑되고 있었다. 즉, 기본적으로 해당하는 URL이 없으면 resource를 조회하도록 설계되어 있고, 존재하지 않았을 때 404의 에러 메시지를 응답하는 것이다.

모든 경우에서의 ResourceHandler 매핑 끄기
WebMvcAutoConfiguration의 addResourceHandler 메소드를 살펴보면 된다. ResourceProperties의 addMapping을 false로 설정하면 간단하게 해당 설정을 진행할 수 있다. SpringBoot의 버전에 따라, properties를 관리하는 방식이 다르므로 확인해보고 버전에 맞게 설정을 진행하면 된다.

```spring.web.resources.add-mappings=false```




```java
public class SwaggerConfig implements WebMvcConfigurer {
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("swagger-ui.html")
                .addResourceLocations("classpath:/META-INF/resources/");
        registry.addResourceHandler("/webjars/**")
                .addResourceLocations("classpath:/META-INF/resources/webjars/");
    }
}
```


### NoHandlerFoundException 처리하기

```java

@RestControllerAdvice
public class ControllerAdvice {
    @ExceptionHandler(NoHandlerFoundException.class)
    public ResponseEntity<ExceptionResponse> noHandlerFoundHandle(NoHandlerFoundException exception) {
        ExceptionResponse response = ExceptionResponse.of(exception.getMessage());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(response);
    }
}
```


