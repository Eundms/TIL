## Filter 
> 인코딩, 로깅, 인증/인가, 큰 파일 압축
응답 요청/반환 이전 이후에 여러 작업 처리할 수 있도록 하는 servelt API 인터페이스 중 하나이다.
- init : 필터객체 초기화 & 서비스에 추가
- doFilter : request, response, filterchain
- destroy : 필터 객체를 서비스에서 제거하고 사용하는 자원을 반환하기 위한 메소

- 스프링 컨테이너에 존재하는 빈들을 사용할 수 없어 , 비즈니스 로직과 연관된 작업을 수행할 수 없다. 
https://mangkyu.tistory.com/221 

## Interceptor
> 디스패처 서블릿이 컨트롤러를 호출하기 전에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공

- preHandle   
: preHandle 메소드는 컨트롤러가 호출되기 전에 실행된다. 그렇기 때문에 컨트롤러 이전에 처리해야 하는 전처리 작업이나 요청 정보를 가공하거나 추가하는 경우에 사용할 수 있다.

- postHandle  
: postHandle 메소드는 컨트롤러를 호출된 후에 실행된다. 그렇기 때문에 컨트롤러 이후에 처리해야 하는 후처리 작업이 있을 때 사용할 수 있다. 이 메소드에는 컨트롤러가 반환하는 ModelAndView 타입의 정보가 제공되는데, 최근에는 Json 형태로 데이터를 제공하는 RestAPI 기반의 컨트롤러(@RestController)를 만들면서 자주 사용되지는 않는다.

- afterCompletion  
afterCompletion 메소드는 이름 그대로 모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실행된다. 요청 처리 중에 사용한 리소스를 반환할 때 사용하기에 적합하다.

## Aspect Oriented Programming (AOP)
- 공통 부가 기능(Cross Cutting concern)을 모