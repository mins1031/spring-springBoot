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
 > 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것, DI컨테이너 = 스프링 컨테이너 라고 한다.
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

## 8. spring, spring boot
 #### 스프링 컨테이너 생성과정
 ```
 ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class)
 ```
 * ApplicationContext를 스프링 컨테이너라고 하고 인터페이스이다
 * AnnotationConfigApplicationContext는 ApplicationContext의 구현체중 하나이다(구현체가 굉장히 많다)
 * 스프링 컨테이너는 XML기반으로 만들수도 있고 어노테이션 기반 자바 설정 클래스로 만들수 있다. 위의 AnnotationConfigApplicationContext는 자바 설정 클래스를 기반으로한 구현체이다. xml로 하려면 다른 구현체를 사용한다고 한다.
 * 위의 ApplicationContext가 AppConfig설정 정보를 통해 생성시의 과정을 조금더 간략화하면
   1) AppConfig.class의 설정을 기반으로 한 스프링 컨테이너 applicationContext가 생성 
   2) AppConfig.class의 빈설정을 기반으로 컨테이너에 스프링 빈 객체를 등록한다.
   3) 설정 정보를 통해 의존관계주입을 준비후 의존관계를 주입해준다.
   4) 스프링 컨테이너에 빈 객체로 등록된 MemberSerice를 주입 받게 되면 MemberSerice가 의존하고 있는 MemberRepository가 주입된 MemberSerice가 리턴되어 주입된다. 
 
 * 그런데 ApplicationContext는 어떻게 xml이나 자바 또는 다른 설정 형식을 지원할 수 있을까?
 * 그것은 BeanDefinition이라는 인터페이스를 통해 가능하다. 스프링 컨테이너는 xml형식인지,자바 형식인지 몰라도 되고 오직 BeanDefinition만 알면된다. 
 * BeanDefinition을 빈 설정 메타정보라고 한다.
 * AnnotationConfigApplicationContext는 AnnotatedBeanDefinitionReader를 통해 AppConfig를 읽고 BeanDefinaition을 ApplicationContext로 리턴해준다.
 * Xml은 위와 같은 방식으로 진행된다.
 * **스프링이 다양한 형태의 설정정보를 BeanDefinaition으로 추상화해서 사용하는것 정도만 이해하고 나중에 BeanDefinaition 관련 코드를 보았을때 이런 매커니즘을 떠올리면 된다. ** 
 
 #### 싱글톤
 > 웹 어플리케이션과 싱글톤
 스프링은 멀티쓰레드를 지원하고 하나의 요청에 하나의 스레드를 할당해준다. 만약 우리의 요청을 통해 내부동작중 주입받는 빈 객체들이 스프링컨테이너에서 새로 생성되어 주입된다면?(만약 MemberService를 주입 받아야 한다면 MemberService내의 MemberRepository도 빈이기에 같이 주입되 MemberService를 주입 받는다)우리의 요청 하나에 객체가 2개가 생성되어 동작한다. 다만 이러한 요청이 초당 1000개,1만개 늘어나게 되면 굉장히 비효율적으로 메모리를 사용하며 어플리케이션이 동작한다.
 * 이러한 현상을 해결한 것이 싱글톤 패턴으로 컨테이너를 구성하는 것이다. => 객체 1번만 생성후 참조값 공유
 > 싱글톤 패턴이란
 
 ```
 public class SingletonService {
    
    // 1.static 영역에 객체 instance를 하나 생성해 메모리에 올리고 해당 참조값을 반환하게 한다
    private static final SingletonService instance = new SingletonService();
    
    //2. 이 객체 인스턴스가 필요하다면 오직 getInstance() 메서드를 통해서만 조회할 수 있고 이 메서드는 같은 인스턴스를 참조하고 있기 때문에 항상 같은 인스턴스를 리턴한다.
    public static SingletonService getInstance(){
        return instance;
    }

    //3. private생성자를 통해 새로운 SingletonService객체를 생성하지 못하게해 하나의 객체만 생성되게 한다.
    private SingletonService() {
    }
 }
 ```
 * 위 처럼 코드 작성후 다른 참조변수 `SingletonService s1 = SingletonService.getInstance()`, ` SingletonService s2 = SingletonService.getInstance()` s1,s2의 참조값이 같다는 것을 확인할 수 있다.
 * 이처럼 요청마다 객체를 생성할 필요 없이 하나의 객체만 생성해 공유하는 단순하고 효율적인 방식이지만 많은 단점이 존재한다
   1) 싱글톤 패턴 구현을 위해 들어가는 코드가 많아진다. (위의 코드 처럼) 
   2) 의존관계상 클라이언트가 구체 클래스에 의존한다. -> DIP위반
   3) 클라이언트가 구체 클래스에 의존해 OCP 원칙 위반가능성이 높다.
   4) 테스트 하기가 어렵다
   5) 내부 속성을 변경하거나 초기화하기 어렵다.
   6) private 생성자로 자식클래스를 만들기 어렵다
   7) 결론적으로 유연성이 떨어진다. 안티패턴으로 불리기도 한다.
 
 > 싱글톤 컨테이너
 * 스프링 컨테이너는 싱클톤 패턴을 적용하지 않아도 객체 인스턴스를 싱글톤으로 관리한다.
 * 스프링 컨테이너는 싱글톤 컨테이너 역할을 한다. 이렇게 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라고 한다.
 * 스프링 컨테이너의 이런 기능 덕에 싱글톤 패턴의 단점들을 해결하며 객체를 싱글톤으로 유지할 수 있다
   * 싱글톤 패턴을 위한 지저분한 코드가 클래스에 들어가지 않아도 된다.
   * DIP,OCP,테스트, private 생성자로 부터 자유롭게 싱글톤을 사용할 수 있다. 
 * **스프링 컨테이너 덕에 요청 올떄마다 객체를 생성하는 것이 아닌 이미 만들어지 객체를 공유해서 효율적으로 재사용 할 수 있다.** 
 
 > 싱글톤 방식의 주의점
 * 객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 **상태를 유지하게(stateful)** 설계하면 안된다.
 * 무상태(stateless)로 설계해야 한다
   * 특정 클라이언트에 의존적인 필드가 있으면 안된다
   * 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다.
   * 가급적 읽기만 가능해야 한다.
   * 필드 대신에 자바에서 공유되지 않는 지역변수,파라미터 등을 사용해야 한다
 * 스프링 빈의 필드에 공유값을 설정하면 큰 장애를 맞을수 있다
 ```
 public class StatefulService {
   private int price; //상태를 유지하는 필드
   
   public void order(String name, int price) {
     System.out.println("name = " + name + " price = " + price);
     this.price = price; //여기가 문제!
   }
   public int getPrice() {
     return price;
   }
}
...테스트 코드

StatefulService statefulService1 = ac.getBean("statefulService",StatefulService.class);
StatefulService statefulService2 = ac.getBean("statefulService",StatefulService.class);
 
 //ThreadA: A사용자 10000원 주문
 statefulService1.order("userA", 10000);
 
 //ThreadB: B사용자 20000원 주문
 statefulService2.order("userB", 20000);
 
 //ThreadA: 사용자A 주문 금액 조회
 int price = statefulService1.getPrice();

 //ThreadA: 사용자A는 10000원을 기대했지만, 기대와 다르게 20000원 출력
 System.out.println("price = " + price);
 
 Assertions.assertThat(statefulService1.getPrice()).isEqualTo(20000);
 }
 ```
 * 결국 B사용자의 스레드인 B로 인해 값이 바뀌어서 A의 주문 금액역시 20000원이 되어버린것을 볼 수 있다.
 * 이렇게 되면..... 꼭 스프링 빈은 값을 무상태, 상태유지 필드가 있어도 값을 조작하지 못하게 해야한다.
 * 다만 스프링 컨테이너의 빈들사이에서 한 빈 객체를 여러번 호출하는 경우가 있을수도 있다. 그러면 스프링 컨테이너는 싱글톤을 어떻게 유지할 수 있을까
 * @Configuration 어노테이션이 있는 자바 설정 클래스가 빈 설정 파일로 등록되 해당 설정클래스는 물론 내부 @Bean이 붙은 메서드들의 메서드명이 빈 이름, 리턴값이 빈 객체로 설정된다.
 *  그런데 빈으로 등록된 설정 클래스의 정보릘 출력해보면 CGLIB라는 이름이 붙은 이상한 이름이 나오게 된다.
 *  이것은 스프링이 CGLIB라는 바이트 코드 조작 라이브러리를 이용해 설정 클래스를 상속받은 임의의 다른 더미 클래스를 만들고 그 다른 클래스를 스프링 빈으로 등록한 것이다.(내부의 @Bean들은 리턴값 자체가 등록된다.)그리고 이 임의의 클래스가 싱글톤이 보장되게 해준다.
   * 아마 @Bean이 붙은 메서드마다 스프링 컨테이너에 빈으로 존재하면 해당하는 빈 객체 리턴하고, 빈이 없으면 생성해서 빈으로 등록후 리턴값을 반환하는 코드가 동적으로 만들어지는듯 하다.
   * 이를 통해 궁극적 싱글톤이 보장되는 것이다.  

 #### 컴포넌트스캔
 * @Component, @Controller, @Service, @Repository, @Configuration 위의 어노테이션들이 붙은 클래스를 빈으로 등록할 클래스로 인식해 @ComponentScan 어노테이션이 붙은 클래스의 하위 디렉토리 클래스 들을 뒤져 해당 어노테이션들이 있는지 확인후 빈으로 끌어올려준다.(정확히는 @Component가 붙은 모든 클래스들을 스프링 빈으로 사용하는 것이다.)
 * 이때 스프링빈의 기본등록 이름은 클래스명을 사용하되 맨 앞글자만 소문자를 사용해준다.(만약 빈이름을 직접 지정하고 싶다면 @Component("빈 이름")이렇게 해주면 된다.)
 * 이처럼 컴포넌트 스캔으로 빈을 등록하는 것을 `자동 빈등록` @Bean으로 등록하는 것을 `수동 빈등록`이라고 한다
 * 그렇다면 똑같은 이름의 빈이 중복등록된다면 어떻게 될까? 
   * 우선 자동 빈 등록 vs 자동 빈 등록 => `ConflictingBeanDefinitionExceoption`예외가 발생한다
   * 수동 빈 등록 vs 자동 빈 등록 => 수동 빈이 자동빈을 오버라이딩 해버려 수동 빈이 등록된다.그러나 최근 스프링 부트는 이경우에도 에러가 나도록 디폴트 값을 바꾸었다고 한다. 
 #### 의존관계 주입 방식
 > 의존 관게를 주입하는 방법에는 크게 4가지 방법이 있다.
 * 생성자 주입
   * 생성자를 통해서 의존 관계를 주입받는 방법이다
   * 생성자 호출 시점에 딱 1번만 호출되는 것이 보장된다. 
   * 변하지 않고, 필수 의존관계에 사용한다
 * 수정자(setter) 주입 
   * setter라 불리는 필드 값을 변경하는 수정자 메서드를 통해 의존관계를 주입하는 방법이다.
   * 선택, 변경 가능성 있는 의존관계에 사용한다 
 * 필드 주입
   * 말그대로 필드에 선언해 주입하는 방식이다 `@Autowired  private MemberSerice ms`
   * 코드가 간결하지만 외부에서 변경할수 있는 방법이 아무것도 없어 테스트하기 힘들다.
   * DI 프레임워크가 없으면 무용지물 코드이다. 
 * 일반 메서드 주입

 * **웬만하면 생성자 주입을 선택하는 것이다!**
   * 불변
     * 대부분의 의존관계 주입은 한번 일어나면 어플리케이션 종료 시점까지 의존관계를 변경할 일이 없다. 오히려 대부분의 의존관계는 어플리케이션 종료전까지 변하면 안된다
     * 만약 상황에 따라 다른 관계를 의존해야 하는 경우는 상황에따른 모든 의존관계를 미리 가져와놓고 사용하는 것이 더 좋다 (의존관계 List,Map으로 받는 경우)
     * 또한 수정자 주입을 사용하면 setter메서드를 public으로 열어놔야 한다
     * 누군가 실수로 변경 할 수도 있고 변경하면 안되는 메서드를 열어두는 것은 좋은 설계방법이 아니다.
     * 생성자 주입은 객체를 생성할 때 딱 1번만 호출이 되므로 이후에 호출되는 일이 없다.  
   * 누락
     * 스프링 없이 순수한 자바 코드를 테스트 하는 경우 의존관계를 주입해서 사용해줘야 하는데 생성자의 경우는 어떤 의존관계를 필수로 주입해야하는지 파악할 수 있고 데이터 누락시 컴파일오류가 발생한다.
   * 생성자 주입을 선택하는 여러이유가 있지만 우선 기본으로 생성자주입을 사용하고 상황과 조건에따라 setter방식을 사용하는 것도 방법이다.
 
 
 ## 빈 생명주기 콜백
 * 스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공한다.
 * 개발자는 의존관계주입이 끝난 시점을 알아야 초기화 작업을 적용할 수 있다.
 * 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 준다.
 ```
 스프링 빈의 이벤트 라이프 사이클
 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백 -> 스프링 종료
 !!여기서 의존관계주입 방식에 따라 의존관계 주입 단계가 조금 달라지는데 생성자 방식의 경우 빈생성시 어느정도 의존관계가 주입되고 나머지 세터나 필드주입의 경우 위의 단계를 따른다.
 ```
 * 초기화 콜백 : 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출(여기서 초기화란 해당 객체가 처음 일을 시작하는 것을 의미한다 ex)네트워크 연결, 필드값 삽입,DB 커넥션 연결등등 )
 * 소멸전 콜백 : 빈이 소멸되기 직전에 호출
 * 스프링은 크게 3가지 방법으로 생명주기 콜백을 지원한다.
   * 인터페이스(InitializingBean, DisposableBean)
     * 스프링의 인터페이스 InitializingBean과 DisposableBean를 상속받아 콜백을 사용하지만 `스프링프레임워크`에 의존하기 때문에 좋지 않고 외부 라이브러리에 적용할수 없다. 
   * 설정 정보에 초기화 메서드, 종료 메서드 지정
     * @Bean에 초기화, 소멸 콜백 메서드를 지정해서 동작하게 할수 있다. 외부 라이브러리에 적용가능한점이 큰 장점이다. 메서드의 이름을 자유롭게 줄수 있다
     * 라이브러리는 대부분 close,shoutdown이라는 이름의 종료 메서드를 사용한다. @Bean의 destroyMethod는 기본값이 inferred으로 등록되어있고 이 추론 기능은 close, shutdown이라는 이름의 메서드를 자동으로 호출해준다.  
   * @PostConstruct, @preDestory 어노테이션 지원
     * 초기화, 소멸 메서드에 어노테이션 하나만 붙이면 된다
     * 스프링에서 가장 권장하는 방법이다
     * 스프링에 종속적인 기술이 아닌 자바 표준 기술이기 떄문에 다른 컨테이너에서도 동작한다. 
     * 유일한 단점은 외부 라이브러리엔 적용할수 없다는 점이다. 외부 라이브러리 초기화,종료시 @Bean기능을 이용하는게 좋다.     


## 9. 어노테이션
### 주요 어노테이션
1) `@Configuration` : 해당 어노테이션이 있는 클래스는 자바 빈설정을 담당하는 클래스가 된다. 해당 클래스 내의 `@Bean` 어노테이션이 붙은 메서드를 선언하면 해당 메서드를 통해 스프링 빈을 정의하고(주로 메서드 리턴값) 생명주기를 설정하게 된다.
2) `@ComponentScan` : @ComponentScan은 위의 @Configuration 설정 파일에 같이 적용해 사용해주면 해당 클래스는 자바 빈설정 클래스이고 이 @ComponentScan의 속성값 범위안에서 `@Component` 혹은 `@Component`를 포함한 다른 어노테이션을 모두 빈으로 만들어준다. 선호되는 방식은 @ComponentScan을 최상의 클래스에 적용해 사용하면 해당 클래스 밑의 클래스들에서 @Component 를 찾아 빈 설정하기 때문에 최상위 클래스에 적용하는것이 편하다.(Spring boot역시 이 방법으로 사용되고 있다.)
3) `@Component` : 빈으로 적용되는 클래스를 의미하는 어노테이션으로 @ComponentScan의 스캔 대상이다.@Service,@Controller,@RestController,@Repository등등의 어노테이션에도 포함되어있다
4) `@Autowired` : 해당 어노테이션은 원하는 스프링 빈을 주입해주는 어노테이션이다. 해당 클래스의 타입에 맞는 빈을 가져와 주입해 준다. 만약 타입의 빈이 1개 라면 해당 빈을 주입하지만 2개 이상이라면 `@Primary`나  `@Qualifier`를 활용해 추가 설정을 해줘야 한다.
5) `@Value` : 생성자, 필드,메서드등에 스프링에서 설정한 값을 주입할 수 있다. 주로 application.properties or yml 파일에 명시된 값이 필요할때 사용한다
6) `@Scope` : 빈의 생명주기를 설정한다. 기본값을 싱글톤이고 프로퍼티나 request,session,globalSession 같은 내용으로 설정할 수 있다.
7) `@SpringBootApplication` : 스프링 부트는 기본적으로 이 어노테이션을 기준으로 동작하도록 되어있다 스프링에서 필수적인 초기화를 담당하는 `@EnableAutoConfiguration`,`@ComponentScan`,`@Configuration ` 어노테이션이 포함되어 있다. 이클래스를 기준으로 빈 스캔을 하게 되며 해당 클래스 밑으로 개발을 해야한다.
8) `@EnableAutoConfiguration` : 스프링 부트의 핵심 어노테이션으로 여태까지 Springboot없이 XML이나 자바설정에서 필수적으로 스프링에 세팅하는 왠만한 것들을 자동 설정하여 돌아가게 하는 어노테이션이다.
9) `@RequsetMapping` : 해당 어노테이션을 메서드 위에 명시하면 해당 메서드는 이 어노테이션이 설정한 경로를 호출했을때 해당 메서드가 실행되어 메서드의 응답값을 받게 되며 컨트롤러 클래스 자체에 명시하면 어노테이션에 설정되 URL의 하위로 클래스내의 메서드들의 URL이 설정된다. 또한 특정HTTP메서드에만 응답 가능하도록 `@GetMapping`,`@PostMapping`,`@PatchMapping`,`@DeleteMapping`등 의 별칭 어노테이션도 존재한다. 또 `consume` 속성으로 요청값에 대한 유형을 한정지을수 있으며 `produce` 속성을 통해 응답 유형을 강제할 수 있다. 이 둘의 설정시 지정 타입이 안맞으면 400 bad Requset 응답을 하도록 스프링에서 설정되어있다.
10) `@MoelAttribute` : @MoelAttribute는 내부적으로 돌아가는 부분이 타 MVC어노테이션에 비해 조금 많다. @MoelAttribute는 클라이언트가 전송하는 multipart/form-data 형태의 `HTTP Body 내용과` `HTTP의 파라미터들`을 setter를 통해 1대1로 객체 필드에 바인딩하기 위해 사용된다.  메서드 파라미터에 @MoelAttribute선언시 
  1) @MoelAttribute 어노테이션이 붙은 객체를 자동으로 생성해 주는데 이떄 어노테이션이 붙은 객체는 POJO객체 여야한다.즉 필드들과 그에 따른 getter,setter가 존재하는 객체여야 한다 
  2) 생성된 인스턴스에 HTTP 헤더로(쿼리스트링으로)넘어 온 값들은 자동으로 바인딩한다. 해서 뷰에서 정의된 이름과 객체의 필드 이름이 같아야 한다. 값이 헤더로 넘어오면 객체의 setter를 이용해 필드에 바인딩 된다.
  3) @MoelAttribute 어노테이션이 붙은 객체가 자동으로 Model객체에 추가 되고 따라서 따로 Model에 넣어주지 않아도 응답시 뷰까지 전달된다.(@MoelAttribute("hi")처럼 괄호안의 이름으로 model에 추가된다)
일반 웹구성시 뷰에서 여러 데이터를 서버에서 전달 받을때 주로 사용했으며 API구성시 GET방식으로 여러 데이터를 한번에 전달받을때 주로 사용했었다.
11) `@RequsetParam` : @RequsetParam은 `1개의 HTTP 요청 파라미터를 받기 위해서` 사용한다. @RequsetParam은 필수 여부가 true이기 떄문에 기본적으로 반드시 해당 파라미터가 전송되어야한다.해당 파라미터가 전송되지 않으면 400 에러가 발생한다. `@RequsetParam(value = "뷰 필드값") String 파라미터 이름` 
12) `@RequestBody` : @RequestBody는 클라이언트가 전송하는 Json형태의 HTTP BODY의 내용을 자바 객체로 변환시켜주는 역할을 한다. @RequestBody와 @ResponseBody는 각각 HTTP 요청의 바디의 내용을 자바 객체로 변환하고 자바 객체를 HTTP 응답의 바디로 변환한다. 스프링은 @RequestBody나 @PathVariable 어노테이션을 사용해 요청의 파라미터 값을 받아올떄 HandlerMethodArgumentResolver를 사용해 값을 받아온다. 이 **HandlerMethodArgumentResolver는 컨트롤러 메서드에서 특정 조건에 맞는 파라미터가 있을때 원하는 값을 바인딩 해주는 인터페이스**인데 따로 커스텀하여 사용해야 하는 경우도 있다. 그렇다면 Json데이터가 @RequestBody로 받을시  HandlerMethodArgumentResolver는 어떻게 동작할까?  우선 HandlerMethodArgumentResolver의 구현체중 HandlerMethodArgumentResolverComposite 클래스에서 resolveArgment()(바인딩할 객체를 만들어 리턴하는 메서드) 메서드를 호출하고 내부에서 getArgumentResolver() 메서드를 호출하여 HandlerMethodArgumentResolver를 구현한 모든 클래스를 순회하여 supportsParameter()(파라미터 타입이 바인딩 지원되는 타입인경우 True리턴하는 메서드) 메서드를 호출해 알맞는 객체인   RequestResponseBodyMethodProcessor 인스턴스를 반환한다. RequestResponseBodyMethodProcessor 인스턴스의 resolverArgument()메서드를 호출해 @RequsetBody의 파라미터를 확인해 body를 읽어 들일 컨버터를 지정해 주는데 json타입이기에 MappingJackson2HttpMessageConverter 클래스가 읽어들이게 설정해준다.(MappingJackson2HttpMessageConverter는 application/json 요청이 들어올때 동작하도록 설계되어있다.) 이후 jackson의 ObjectMapper를 통해 요청바디의 json 데이터를 객체 필드와 바인딩해준다.이때 위에서 컨버터를 지정시 기본적으로 스프링은 HttpMessageConverter 인터페이스의 구현체들로 응답해주는데 HttpMessageConverter란 HTTP 바디 내용을 변환하거나 변환될때 사용된다. 문자열이나 정수 처리엔 StringHttpMessageConverter, 객체로 역,직렬화 과정엔 위의 MappingJackson2HttpMessageConverter를 사용하게 된다.
13) `@PathVariable` : @PathVariable 파라미터를 사용하면 해당 메서드 uri의 일부를 파라미터로 전달할 수 있다. API구성시 많이 사용된다. 위의 @RequestBody와 같이 HandlerMethodArgumentResolver를 통해 컨버터를 할당받아 사용 되게 된다.
