# spring-springBoot

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
 > 프로그램의 제어 흐름을 직접 제어하는것이 아니라 외부에서 관리하는 것을 **제어의 역전(IoC)** 이라고 한다.
 * 기존엔 클라이언트 객체가 스스로 필요한 서버 구현 객체를 생성,연결,실행 했다. 한마디로 구현 객체가 프고르매의 제어 흐름을 스스로 제어했다.
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
## 3 Spring MVC 동작 원리
 1) 웹 어플리케이션이 실행되면 WAS에 의해 배포서술자 web.xml 파일이 로딩된다.
 2) WAS는 web.xml 에 등록되어있는 ContextListner를 생성한다.
  * 자동으로 스프링컨테이너(ApplicationContext) 초기화
  * Servlet(아마 컨트롤러)을 사용하는 시점에 
 3) 
  
