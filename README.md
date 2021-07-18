# spring-springBoot
**!!Colinch4님의 spring 기술면접 블로그 내용을 보며 이해하는 것 + 필기 형식으로 작성하였다.**
# 1.Servlet와 JSP
 ## 1) 서블릿 
  > 자바를 이용하여 웹페이지를 동적으로 생성하는 서버측 프로그램이다. 웹서버의 성능을 향상하기 위해 사용되는 자바 클래스의 일종.
  ### 1.1 서블릿의 특징
    * HTML을 사용하여 요청에 응답한다.
    * java Thread를 이용하여 동작한다.(정확히는 WAS가 web.xml을 참조해 Servlet에 대한 스레드를 생성하는 것.)
    * 서블릿 컨테이너가 이해 할 수 있도록 순수 자바 코드로만 이루어져 있다.
    * MVC 패턴에서 Controller로 이용된다.
    *  HTTP 프로토콜 서비스를 지원하는 HttpServlet클래스를 상속받아 요청,응답을 처리 할 수 있다
  ### 1.2 서블릿의 동작 방식
    1) 클라이언트에서 요청시 이를 서블릿 컨테이너(WAS)로 전송
    2) 서블릿 컨테이너는 HttpServlet요청,응답 객체를 생성한다
    3) web.xml은 사용자가 요청한 URL을 분석하여 어떤 서블릿에 대한 요청인지 찾는다(한 서블릿 = 한 컨트롤러)
    4) 서블릿 찾으면 해당 서블릿 스레드에서 service 메서드 호출후 요청의 post,get여부에 따라 doGet or doPost메서드를 호출해준다.
    5) do메서드는 동적페이지를 생성한후 HttpServletResponse객체로 응답해준다.
    6) HttpServlet클래스 소멸.
 ## 2) WAS(서블릿 컨테이너)
 > 서블릿 컨테이너는 서블릿을 관리하며 네트워크 통신, 서블릿 생명주기 관리, 스레드 기반의 병렬처리를 대행한다. 가장 대표적인 것으론 Tomcat이 있다.
 ## 3) WS vs WAS(Apache vs Tomcat)
  > 웹서버 는 클라이언트의 요청을 기다리고 요청에 대한 데이터를 만들어서 응답하는 역할을 한다. 이때 데이터는 정적인 데이터(html, css, 이미지등)로 한정된다. 말그대로 미리 정해진 자원들을 응답해 주는 것이다.

  > WAS는 클라이언트의 요청이 있을 때 내부 프로그램을 통해 결과를 만들어내고 이것을 다시 클라이언트에게 돌려주는 역할을 한다. 이는 WS의 기능 일부와 웹 컨테이너의 결합으로 다양한 기능을 컨테이너에 구현하여 다양한 역할을 수행한다.
  + 전에는 정적 파일은 웹서버에서 제공하고 동적 기능들은 WAS를 쓰는것이 효율적이라는 말이 있었지만 톰캣 5.5부터 httpd의 네이티브 모듈을 사용해서 스태틱 파일을 처리하는 기능을 체공한다. => WAS만으로 성능 챙길수 있게되었다.
## 4) JSP 
> 기본 서블릿 같은 경우 응답으로 동적 페이지를 주려면 상당히 귀찮은 작업이 필요했다. 그래서 등작한 것이 JSP이다.
기존 방식보다 html 작성이 용이하게 바뀌었다. 내부적으로 톰캣이 jsp는 servlet으로 바꾸어서 돌린다고 한다.
# 2 Spring DI,IOC
 ## 2-1) IOC(제어의 역전)
 > 프로그램의 흐름을 직접 제어하는것이 아니라 외부에서 관리하는 것을 **제어의 역전(IoC)** 이라고 한다.

 * 기존엔 클라이언트 객체가 스스로 필요한 서버 구현 객체를 생성,연결,실행 했다. 한마디로 구현 객체가 프로그램의 제어 흐름을 스스로 제어했다.
 * 반면 spring 컨테이너를 통해 프로그램에 대한 제어 흐름에 대한 권한은 모두 컨테이너가 가지고있다.
 * 이렇게 구현 객체는 자기 자신의 로직만을 실행하고 필요한 요소는 스프링이 알아서 주입해준다.
 ## 2-2) DI(의존성 주입)
 > 어플리케이션 실행시점(런타임)에 외부에서 실제 구현객체를 생성, 클라이언트(주입당하는 객체)에 던달해서 클라이언트와 서버의 실제 의존관계가 연결되는 것을 의존관계주입 이라고 한다
 * Ioc를 실제로 구현하는 방식이라고 할 수 있다.
 * 객체 인스턴스를 생성하고 그 참조값을 전달해서 연결된다.
 * 의존관계 주입을 사용하면 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스
를 변경할 수 있다.
 * 의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽
게 변경할 수 있다
 ## 2-3) 스프링 컨테이너란?
 > 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것, DI컨테이너= 스프링 컨테이너 라고 한다.
 ## 2-4) 스프링 컨테이너의 종류
 * BeanFactory
 > DI의 기본사항을 제공하는 가장 단순한 컨테이너이다.BeanFactory 는 빈을 생성하고 분배하는 책임을 지는 클래스 빈 자체가 필요하게 되기 전까지는 인스턴스화를 하지 않는다 (lazy loading)
 
 * ApplicationContext
  > 빈팩토리와 유사한 기능을 제공하지만 좀 더 많은 기능을 제공한다.
   * 국제화가 지원되는 텍스트 메시지를 관리해 준다.
   * 이미지같은 파일 자원을 로드 할 수 있는 포괄적인 방법을 제공해준다.
   * 리스너로 등록된 빈에게 이벤트 발생을 알려준다.
   * Lazy Loading이 아니라 컨텍스트 초기화 시점에 모든 싱글톤 빈을 미리 로드한다.
# 3 Spring MVC 동작 원리
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile21.uf.tistory.com%2Fimage%2F992B234C5C807FD1146507" />

 1) 웹 어플리케이션이 실행되면 WAS에 의해 배포서술자 web.xml 파일이 로딩된다.
 2) WAS는 web.xml 에 등록되어있는 ContextLoaderListner를 생성한다.
   * 자동으로 스프링컨테이너(ApplicationContext) 초기화
   * Servlet(아마 컨트롤러)을 사용하는 시점에 ServletContext에 ApplicationContext를 등록
   * Servlet이 종료되는 시점에 ApplicationContext삭제
 3) 위에서 생성된 ContextLoaderListner는 root-context.xml을 로딩한다
   * root-context.xml은 어플리케이션의 bean을 정의하는 설정파일
 4) Root Spring Container 구동
   * ContextLoaderListner가 root-context.xml의 설정 기반으로 root spring container를 기동
 5) 사용자 요청 받음
   * 최초의 클라이언트 요청이면 DispatcherServlet 객체가 생성된다.
 6) 두번째 Spring Container 구동 (DispatcherServlet)
   * 두번째 스프링 컨테이너에는 컨트롤러 bean들이 들어있고, 기존 root-container 클래스를 상속받는다
   * DispatcherServlet객체는 servlet-context.xml 파일을 로딩하여 두번째 스프링 컨테이너를 구동한다
   * servlet-context는 @Controller 어노테이션을 스캔하여 bean을 등록한다
 7) DispatcherServlet의 doService() 호출
   7-1) doService()에는 사용자의 요청을 처리하기 위한 Handler와 Adapter을 찾아 호출하기 위해 doDispatch() 호출
   7-2) doDispatch() 에서는 HandlerMapping 을 통해서 요청에 맞는 Controller 의 HandlerMethod를 찾고,
   HandlerMethod를 호출할 수 있는 HandlerAdapter를 찾는다
   7-3) HandlerAdapter가 HandlerMethod 호출
 8) Controller 요청 처리후 Controller는 view와 ModalAndView 리턴
 9) 리턴받은 viedw는 ViewResolver가 먼저 받아 해당 view가 존재하는지 검색
 10) DispatcherServlet은 ViewResolver로부터 JSP등 최종 표시 결과를 받아서 최종결과를 사용자에게 
# 4 AOP기본
 ## 4-1 AOP 용어
  1. Advice
   * 언제 공통관심 기능을 비즈니스 로직에 적용할지 정의
   * 예를들어 '메서드를 호출 하기 전에 트랜잭션 시작' 기능을 적용한다는 것을 정의하고 있는것.
  2. JoinPoint
   * advice를 적용 가능한 지점을 의미
   * 메소드 호출, 필드값 ㅕㄴ경등이 조인포인트에 해당한다.
  3. Weaving : Advice를 비즈니스로직에 적용하는 행위
  4. Aspect : 여러 객체에 공통으로 적용되는 기능. 트랜잭션, 보안등이 Aspect의 예
 ## 4-2 Weaving 방식
  1) 컴파일시에 Weaving하기
  2) 클래스 로딩 시에 Weaving하기
  3) 런타임시에 Weaving하기
  > 1,2번의 경우 AspectJ라이브러리를 추가하여 구현할때 사용됨. 런타임시 위빙같은 경우는 Spring-Aop에서 사용하는 방식으로, 소스코드나 클래스 자체를 변경하는 것이 아니라 프록시 객체를 사용하여 모듈을 위빙하고 비즈니스 로직을 실행한다..
# 5 스프링 부트 
 ## 스프링 부트의 특징
 * Embedded Tomcat(WAS)제공
   * DispatcherServlet도 자동 설정된다.
   * 즉 서블릿 컨테이너만들고 서블릿넣는 것이 자동이고 톰캣역시 내장톰갯으로 가지고 있다.
 * 의존성 관리와 설정의 편리함
   * 스프링에서 xml이나 자바로 설정해줘야했던 많은 것들을 스프링 부트는 Spring Web이라는 의존성패키지 하나에 거의 담겨있다.
 * @SpringBootApplication 어노테이션으로 xml 설정대체
   * @SpringBootApplication는 @ComponentScan 과 @EnableAutoConfiguration을 포함하고 있다.
   * 스프링 부트는 bean을 @ComponentScan 후 @EnableAutoConfiguration이 동작한다
   * @ComponentScan은 프로젝트 패키지 내의 어노테이션 정보를 통해 bean을 찾아 등록한다.
   * @EnableAutoConfiguration은 클래스 패스내에 의존성 관련 자동설정. 의존성 주입 어노테이션이다.
 * 독립실행 가능한 어플리케이션 지향 (JAR도 독립실행 가능)
   * mvn package를 하면 실행 가능한 JAR 파일 하나가 생성됨.
   * 스프링부트는 JAR파일들을 읽어 들이는 로더를 제공한다
   * JAR 런처를 사용해서 main함수가 있는 jar 파일을 실행한다.
  
 스프링 부트의 장점 =>
 1. 의존성관리
 2. 설정의 간편화
 3. 임베디드 톰캣(독립실행 가능한 어플리케이션 )

# 6. JPA vs MyBatis
 ## 6-1) 영속성 
  * 데이터를 생성한 프로그램의 생명이 다하더라도 데이터는 남아있는 것.
  * 우리는 데이터베이스를 통해 영속성을 부여한다
  * Persistence Layer (Mapper or Repository)는 데이터에 영속성을 부여해 주는 계층이다.
  * 여기서 JDBC없이 영속성을 갖게 도구가 Persistence Framework
 ## 6-2) SQl Mapper 와 ORM
 Persistence Framework 대표적으로 두가지가 있다
  1) SQL Mapper
    * SQL <- mapping -> object필드(DAO)
    * 대표적인 예로 MyBatis가 있고 mapper.xml에 실제 SQL을 작성해 줘야 한다.
    * 직접 SQL을 많이 조작해야 하는 쿼리가 있는 경우에 유용하다
    * XML파일에 쿼리를 작성하고 @Autowired하는 방식이다. 주로 mapper인터페이스와 같이 사용.
  2) ORM (Object-Relation Mapping)
    * 객체와 RDB 테이블의 데이터를 자동으로 매핑해 주는 도구
    * SQL을 자동으로 생성한다.
    * SQL 쿼리 대신 직관적인 method로 트랜잭션 할 수 있다.
    2-1) JPA 그리고 Hibernate
      * JPA는 자바 어플리케이션에서 데이터베이스를 사용하는 방식을 정의한 인터페이스이다.
      * Hibernate는 JPA를 구현한 구현체이다.
      * 주로 Spring Data JPA와 함께 사용한다.
  3) ORM의 장점과 단점
    * 장점 :
      * 객체지향적인 코드로 직관적이고, 비즈니스 로직에 더 집중할수 있다.
      * DBMS에 종속적이지 않다.
      * 재사용 및 유지보수의 편리성이 증가한다.
      * JPA의 경우 여러 방법이 있지만 QueryDSL과 함께 사용하는 것이 최적의 효과를 볼 수 있다
     * 단점 :
      * 자주 사용되는 대형 쿼리는 별도의 튜닝이 필요한 경우가 있다.
      * 최적화된 SQL쿼리를 사용할 때는 MyBatis가 나은점이 있다.
 # 7. Spring Security
 
 > Spring security는 어플리케이션 보안(인증과 권한, 인가등)을 담당하는 스프링 하위 프레임워크 이다. Spring security는 인증과 권한에 대한 부분을 firterChain의 흐름에 따라 처리하고 있다. 필터는 Dispatcher Servlet으로 가기 전에 적용됨로 가장 먼저 요청을 받지만 인터셉터는 Dispatcher와 Controller사이에 위치한다는 점에서 적용시기의 차이가 있다.
 
 * 인증(Authorization) : 해당 사용자가 본인이 맞는지 확인하는 절차 
 * 인가(Authentication) : 인증된 사용자가 요청한 자원에 접근 가능한지를 결정하는 절차
 => Spring security는 기본적으로 인증절차를 거친 후에 인가 절차를 진행하게 되며 인가 과정에서 해당 리소스에대한 접근 권한이 있는지 확인을 하게 된다. Spring security에서는 이러한 인증과 인가를 위해 Principal(=접근주체 : 보호받는 리소스에 접근하는 대상)을 아이디로, Credential(=비밀번호: 리소스에 접근하는 대상의 비밀번호)을 비밀번호로 사용하는 Credential기반의 인증 방식을 사용한다.
 
  ## Spring Security의 동작방식
  <img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAp74D%2FbtqAWyBRZsE%2FLk6EL0R680ykd45G6A5rK1%2Fimg.png" />
  
   1) 사용자가 로그인을 요청
   2) 필터체인중 AuthenticationFilter가 이 요청을 가로채고 이때 가로챈 정보를 통해 UsernamePasswordAuthenticationToken 이라는 '인증용 토큰객체'를 생성한다
   3) AuthenticationManager의 구현체인 ProviderManager에게 2)의 인증용 토큰객체를 전달한다.
   4) 그다음 다시 AuthenticationProvider에게 인증용 토큰객체가 전달된다
   5) 실제 db에서 사용자 인증 정보를 가져오는 UserDetailService(=PrincipalDetailsService)에 사용자정보(id)를 넘겨준다.
   6) 넘겨받은 id를 통해 DB에서 찾은 사용자 정보인 UserDetails객체를 생성한다
   7) AuthenticationProvider는 UserDetails를 넘겨받고 사용자 정보를 비교한다.
   8) 비교하여 인증이 완료되면 권한등의 사용자 정보를 담은 Authentication 객체를 반환한다
   9) 다시 최초의 AuthenticationFilter에 Authentication 객체가 반환된다
   10) SecurityContextHolder에 Authentication 객체를 저장한다.

 ## 메이븐
  https://goddaehee.tistory.com/199 참고하여 공부후 내용 서술하며 복기했다.
  ### 1. 빌드란
  > 소스코드 파일을 컴퓨터에서 실행할 수 있는 독립 소프트웨어 가공물로 변환하는 과정이나 그에 대한 결과물이다. 쉽게말해 작성한 소스코드(java)와 프로젝트에서 쓰인 각각의 파일 및 자원등(.jpg,jar.yml등)을 jvm이나 was가 인식할 수 있는 구조로 패키징 하는 과정 및 결과물이라고 할 수 있다.

  ### 2. 빌드도구
  * 빌드도구란 프로젝트 생성,테스트,배포등의 작업을 위한 전용 프로그램
  * 빠른기간동안 계속해서 늘어나는 라이브러리추가, 프로젝트 진행하며 라이브러리 버전동기화의 어려움을 해소하고 자 등장하였다.
  ### 3. 메이븐 정의 및 특징
  * Maven은 자바용 프로젝트 관리도구로 Apache ant의 대안으로 만들어졌다
  * Maven은 프로젝트의 전체적인 라이프 사이클을 관리하는 도구이며, 많은 편리함과 이점으로 널리 사용되고 있다
  * Maven은 필요한 라이브러리를 특정문서(pom.xml)에 정의해놓으면 정의된 라이브러리 뿐만아니라 해당 라이브러리가 동작하는데 필요한 다른 라이브러리도 관리하여 네트워크를 통해 자동으로 다운받아준다.
  * 간단한 설정을 통한 배포관리가 가능하다.
  ### 4. 메이븐 라이프사이클
  * 4-1) 라이프 사이클 
   * Maven은 프레임워크기 때문에 동작 방식이 정해져 있고 미리 정의하고 있는 빌드 순서가 있다. 이를 '라이프 사이클'이라고 한다
   <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile21.uf.tistory.com%2Fimage%2F999B12465BBC992C202A89"/>
   
   <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FU37jP%2FbtqBs1h7mS3%2F6kyUiTE6y1SuRfpLrzkn7K%2Fimg.png"/>
   
   * clean : 빌드시 생성되었던 파일들을 삭제하는 단계
   * Validate : 프로젝트가 올바른지 확인하고 필요한 모든 정보를 사용할 수 있는지 확인하는 단계
   * Compile : 프로젝트의 소스코드를 컴파일하는 단계
   * Test : 단위 테스트를 수행하는 단계
   * package : 실제 컴파일된 소스코드와 리소스들을 jar,war등의 파일로 배포를 위한 패키지로 만드는 단계
   * Verify : 통합 테스트 결과에 대한 검사를 실행하여 품질 기준?을 충족하는지 확인하는 단계
   * install : 패키지를 로컬 저장소에 설치하는 단계
   * site : 프로젝트 문서와 사이트 작성,생성하는 단계
   * Deploy : 만들어진 package를 원격 저장소에 release하는 단계

   * 최종 빌드 순서는 complie -> test -> package이다.
     1) compile : src/main/java 디렉토리 아래의 모든 소스코드가 컴파일 된다.
     2) test : src/test/java, src/test/resources 테스트 자원 복사 및 테스트 소스 코드 컴파일 된다.   
     3) packageing : 컴파일과 테스트가 완료된후 jar,war 등의 형태로 압축하는 작업
  * 4-2) Phase(단계)
    > 빌드 라이프사이클의 각각의 단계를 phase라고 한다. phase는 의존관계를 가지고 있어 해당 phase가 수행되려면 이전단계 phase가 '모두'수행 되어야 한다. 즉 이전단계의 phase들이 성공적으로 수행되었을때 현재 phase가 실행된다는 것이다.
  * 4-3) goal
    * 특정 작업, 최소한의 실행단위이다.
    * 하나의 플러그인에서는 여러 작업을 수행할 수 있도록 지원하며, 플러그인에서 실행 할 수 있는 각각의 기능을 goal이라고 한다.
    * **각각의 phase에 연계된 goal을 실행하는 과정을 build라고 한다.**
    * 플러그인의 goal을 실행하는 방법은 '-mvn plugin:goal' 로 실행한다.
 
  ### 5. 메이븐 설정파일
  1) setting.xml 
   * 메이븐 빌드 툴과 관련한 설정파일
   * MAVEN_HOME/conf 디렉토리에 위치 (메이븐 설치시 기본 제공)
   * 메이븐 자체 설정값을 바꾸는 일은 잘없..다?
  2) POM.xml
   * pom.xml은 메이븐을 이용하는 프로젝트의 root에 존재하는 xml파일이다.
   * 메이븐 기능을 이용하기 위해 pom.xml이 사용됨. 
   * 파일은 프로젝트마다 1개이며 프로젝트의 모든 설정,의존성등을 알 수 있다.
  ```
  <?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.min</groupId>
    <artifactId>dockerbuild</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>dockerbuild</name>
    <description>Demo project for Spring Boot</description>
    <url>https://github.com/mins1031/spring-springBoot</url>
    <properties>
        <java.version>11</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
  ```
 #### pom.xml 정보
 * modelVersion : POM model의 버전. pom.xml 파일형식의 버전이라고 보면된다
 * parent : 프로젝트의 계층 정보
 * groupId : 프로젝트를 생성하는 조직의 고유 아이디를 결정한다. 일반적으로 도메인 이름 거꾸로 적는다.
 * artifactId : 프로젝트 빌드시 파일 대표 이름이다. groupId내에서 유일해야 한다.
 * version : 프로젝트의 현재 버전, 프로젝트 개발 중일 떄는 SNAPSHOT을 접미사로 사용
 * packaging : 패키징 유형(ajr,war,ear등)
 * name : 프로젝트, 프로젝트 이름
 * discription : 프로젝트에 대한 간략한 설명
 * url : 프로젝트에대한 참고 
 * properties : 버전 관리시 용이하다.
 * dependencies : dependencies 태그 안에는 프로젝트와 의존 관계에 있는 라이브러리들을 관리 한다.  
 * build : 빌드에 사용할 플러그인 목록이다.
