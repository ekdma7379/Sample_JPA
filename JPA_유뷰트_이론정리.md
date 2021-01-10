<!-- <span style="color:rgb(255,72,72)"></span> -->

## 4강 정리
- JPA(JAVA Persistence 영구적인 API)  
기존 RAM(전기) - 휘발성 데이터
하드디스크 & DB 등 여러 비휘발성 데이터를 이용해서 데이터를 비휘발성으로 만들어주는 언어

- 프로토콜 VS 인터페이스  
약속인데
인터페이스 : 한쪽이 파워(강제성을 부여)가 있는 통신  
EX) 장보고가 만든 프로그램 속 A라는 데이터를 새벽 6~9시까지만 받아! 라고 하면 나머지 사람들은 무조건 들을 수 밖에 없다.
프로토콜 : 모두 다 동등한 통신

- JPA란 
JAVA PERSISTENCE APPLICATION PROGRAMMING INTERFACE  
자바에서 데이터를 영구적으로 저장하기위한 인터페이스(강제성을 띤다).
___
## 5강 정리

ORM이란? Object Relational Mapping   
ORM이란 나의 하인이다.

예제  
테이블 이름 Team 
|COLUMN|DATATYPE|
|--|--|
|ID|INT|
|NAME|VARCHAR2|
|YEAR|VARCHAR2|
    
이 데이터를 클래스로 만들면
```
class Team{

    int id;
    string name;
    string year;
}
```

하지만 JPA의 인터페이스를 사용하면 클래스부터 만들고 해당 클래스를 DB화 할 수 있다.

또한 ORM을 사용하지 않고 직접 쿼리를 날려서 object에 데이터를 세팅하는 일을 단순 반복의 일이다.  
**루틴** : JAVA -> DB connect -> sql exec -> DB result response -> JAVA Set   
위 일을 함수처럼 사용하여 사용할 수 있다.
___  
## 6강
영속성 : 데이터 -> 영구적으로 저장  
    
컨텍스트란? (context) : 대상의 모든 정보  
ex) 난 영숙 너의 모든 컨텍스트를 알고 싶어 = 영숙이의 모든것을 다 알고싶어  
  
자바 프로그램에서 사자 데이터를 얻고싶으면 db가 아닌 영속성 컨텍스트에 먼저 물어본다.  
1. 만약 영속성컨텍스트에 사자 데이터가 없다면?  
JAVA -> 영속성컨텍스트 -> DB -> DB result to JAVA Object -> 영속성 컨텍스트 -> 자바  
  
2. 만약 영속성컨텍스트에 사자 데이터가 있다면?  
JAVA -> 영속성컨텍스트 -> 자바
  
3. 만약 자바에서 사자 데이터를 호랑이 데이터로 바꾸게 된다면?  
JAVA -> 영속성컨텍스트 -> DB와 비교 -> UPDATE문 자동 호출

<span style="color:rgb(255,72,72)"> 영속성 컨텍스트에서 일어나는 모든 일들은 자동으로 작동한다.</span>
  
DB와 OOP의 불일치성 또한 해결할 수 있다.  
  
  **Table Team**
  
|ID|구단이름|창단년도|
|--|--|--|
|1|롯데|1990|
|2|NC|2008|  
  
  **Table Player**  
  
|ID|이름|TEAM ID|
|--|--|--|
|1|이대호|1|
|2|홍길동|2|
RDBMS에서는 데이터의 한 컬럼에서는 구조체같은 객체를 저장할 수 없다.
  
하지만 JPA 사용시에는
```
Class player {
    int id;
    string name;
    Team team;
}
```
과 같이 선언시 자동으로 Team에 위의 데이터가 저장되게 된다.
___
## 7강 OOP의 관점에서 모델링이란? dialect 방언처리란?
1. oop 관점 모델링 예제
  ```
class Car {
    int id;(PK)
    string name;
    string color;
    Engine engine
}

class Engine {
    int id;(PK)
    int power;
}
  ```

위의 클래스를 이용해서
 
  **Table car**
  
|ID|name|color|engineId|
|--|--|--|--|
|1|bmw|white|2|
|2|sonata|black|1|
 
  **Table engine**
  
|ID|power|
|--|--|
|1|4000|
|2|2000|
  
2. oop 관점 + 상속, 컴포지션, 연간검색(어노테이션 키워드로 조회 가능)
```
class Car extends EntityDate
{
    int id;(PK)
    string name;
    string color;
    Engine engine
}

class EntityDate {
    Timestamp input_dtime
    Timestamp update_dtime
}
  ```
|ID|name|color|input_dtime|update_dtime|
|--|--|--|--|--|
|1|bmw|white|yyyy-mm-dd hh24:mi:ss|yyyy-mm-dd hh24:mi:ss|
|2|sonata|black|yyyy-mm-dd hh24:mi:ss|yyyy-mm-dd hh24:mi:ss|

3. JPA는 여러 DB 사용 가능(MSA에 유리)  
오라클이든 마리아DB, MSSQL등 Migration 유리
___
<span style="color:rgb(255,242,158)">여기서 부터 스프링부트 관련 강의</span>
___
## 8강 http의 탄생 http통신이란?   
  
  http는 문서(html확장자를 가지는) 를 원하는 사람에게 전달하는 통신  
  stateless -> 한번 요청을 하면(a.txt를 줘) 동작을 해주고(a.txt를 response해주고) 통신을 끊어버림

  - 웹 브라우저(한글 2007같은 친구) 문서(.html)파일을 읽어주는 친구  
  - 아파치 : 웹서버 인데 문서만 찾아주는 친구  
  - 톰켓 : 웹브라우저는 html,css,javascript같은 파일만 읽을수 있으므로 자바가 포함되어 있는 .jsp 파일을 알아 들을 수 있도록 .html 파일로 컴파일 해주는 컴파일러

  통합 자원 지시자 URL(locator) : 자원 접근  
  통합 자원 식별자 URI(identifier) : 식별자 접근  

  하지만 JPA에서는 URL 접근을 제한한다.
  따라서 요청시에는 무조건 자바를 거친다.  
    
  URL예제 : http://naver.com/a.png  
  URI예제 : http://naver.com/picture/a

  서블릿 생명주기  
  request -> 서블릿컨테이너(톰켓)에서 스레드 생성 -> 서블릿 객체  
  위의 주기는 request가 올때마다 생성한다.
  MAX 쓰레드풀이 20개라면 21번째 request가 올때 해당 request는 대기한다.
___
  ## 9강 web.xml이란?
  web.xml 키워드 예시 성(서버) 문 앞에 문지기(web.xml)가 있다.  
- ServletContext의 초기 파라미터
```
  문지가가 말하길 암구호는 왈라이다.  
  문을 통해 정상적으로 들어온 A는 암구호를 물어볼때 대답 가능  
  문을 통해 들어오지 않은 B는 암구호를 물어볼때 대답 불가능  
```  
- Session의 유효시간 설정
```
  문을 통해 들어온 A는 서버가 인증해준 session을 가지고 있는다.
  문지기가 성안에 존재할 수 있는 시간은 3일이라고 말한다.
  3일이 지나기 전에 A는 문지기에게 3일보다 더 있고 싶다 라고 하면 문지기는 세션을 초기화해준다.  
  문을 통해 들어오지 않은 B는 초기화 불가능
```
- Servlet/JSP에 대한 정의 및 매핑
```
이제 A가 성 안에 101호의 주인(특정 JSP)을 만나고 싶다고 말을 하게 되면 
web.xml은 101호의 주인이 홍길동이라는 것을 알고있어서 소개(매핑)해주게 된다.
```  
- Mime Type 매핑 
```
A가 성 안에 101호의 주인을 만나러 들어올때, 흙이 묻은 감자를 들고 들어왔다.
문지기는 이 감자를 일단 창고에 넣어놓고 이 쌀이 성안에 들여보낼 수 있는 감자인지 아닌지 판단한다. 이 성에서는 감자만 처리할 수 있는데 못된 B는 고구마를 들고 와서 처리하려고 하면 성 안은 아수라장(에러발생)이 되게 된다.
``` 
- Welcome File list  
```
C라는 애는 성에 도착하긴 했는데 어디로 가야할 지 모르는 아이다. 그러면 일단 문지기는 C라는 아이를 광장(이건 개발자가 설정하기 나름 - 보통 index)으로 보내고 생각하게 한다.
```
- Error Pages 처리  
```
성에는 101~104호까지밖에 없다. 근데 105호로 가고 싶어하는 친구가 생겼다면 생각하지 말고 이상한 친구들만 모아놓는 광장으로 보내줘야 한다.
```
- 필터/보안 설정
```
성에 들어오고 싶어하는 친구 중에 총을 들고 들어오려는 친구 E가 있으면 
이 친구에게서 총을 빼앗고(필터) 성 안으로 들여준다. 
옆성에 사는 친국 F는 아예 들어올 수 없게 막는다(필터 / 보안).
```
- 리스너 설정
```
성 안에 성주가 문지기한테 술을 잘 먹는 친구 좀 찾아달라고 하엿지만 문지기는 일이 너무 많아서 해당 일을 못하겠다고 배째라 한다. 그러자 성주가 다른 감시자(리스너)를 하나 둬서 문지기에게 가기 전에 먼저 물어본다. 술을 잘하는 친구라면 술을 먹여보고 잘버티면 문지기에게 내가 데려가겠다고 한 뒤 성주에게 데려간다.
```  
___
## 10강. Frontcontroller
여기에서 Servlet/JSP 매핑시(web.xml에 직접 매핑 or @WebServlet 어노테이션 사용)에 모든 클래스에 매핑을 적용시키기에는 코드가 너무 복잡해지기 때문에 FrontController 패턴을 이용함.

참고 : https://galid1.tistory.com/487

FrontController 패턴
- 최초 앞단에서 request 요청을 받아서 필요한 클래스에 넘겨준다. 왜? web.xml에 다 정의하기가 너무 힘듬.  
- 이때 새로운 요청이 생기기 때문에 request와 response가 새롭게 new될 수 있다. 그래서 아래의 RequestDispatcher가 필요하다.

RequestDispatcher
- 필요한 클래스 요청이 도달했을 때 FrontController에 도착한 request와 response를 그대로 유지시켜준다.

DispatcherServlet
- FrontController 패턴을 직접짜거나 RequestDispatcher를 직접구현할 필요가 없다.  
(왜냐하면 스프링에는 DispatcherServlet이 있기 때문이다. DispatcherServlet은 FrontController 패턴 + RequestDispatcher이다.)
- DispatcherServlet이 자동생성되어 질 때 수 많은 객체가 생성(IoC)된다. 보통 필터들이다. 해당 필터들은 내가 직접 등록할 수 도 있고 기본적으로 필요한 필터들은 자동 등록 되어진다.

스프링 컨테이너  
- DispatcherServlet에 의해 생성되어지는 수 많은 객체들은 ApplicationContext에서 관리된다. 이것을 IoC라고 한다.

static - main()이 실행되기 전부터 메모리에 존재하는 친구
자바객체 - 실행되야 하는 객체

스프링은 객체의 생명주기를 스프링이 관리한다.
따라서 com.cos.blog 이하에 있는 모든 클래스를 component scan하여 객체를 미리 생성한다.  
(@Controller, @RestController, @configration, @Repository, @Service, @Component 등 이 있으면 무조건 메모리에 띄워)

하지만 공통적으로 사용되는 객체(DB connection등)은 하나만 띄워놓고 다같이 사용해도 괸다.

따라서 사용자 A가 보낸 request -> 톰켓 -> web.xml -> <span style="color:rgb(255,242,158)">ContextLoaderListener</span>(root_ApplicationContext 파일을 읽는다.) -> DispatcherServlet -> 로드된 메모리 중 class에 매핑시켜준다.

강의 속 내용
```
ApplicationContext

IoC란 제어의 역전을 의미한다. 개발자가 직접 new를 통해 객체를 생성하게 된다면 해당 객체를 가르키는 레퍼런스 변수를 관리하기 어렵다. 그래서 스프링이 직접 해당 객체를 관리한다. 이때 우리는 주소를 몰라도 된다. 왜냐하면 필요할 때 DI하면 되기 때문이다.

DI를 의존성 주입이라고 한다. 필요한 곳에서 ApplicationContext에 접근하여 필요한 객체를 가져올 수 있다. ApplicationContext는 싱글톤으로 관리되기 때문에 어디에서 접근하든 동일한 객체라는 것을 보장해준다.

ApplicationContext의 종류에는 두가지가 있는데 (root-applicationContext와 servlet-applicationContext) 이다.

a. servlet-applicationContext(웹만 바라보는 변태)

servlet-applicationContext는 ViewResolver, Interceptor, MultipartResolver 객체를 생성하고 웹과 관련된 어노테이션 Controller, RestController를 스캔 한다.

============> 해당 파일은 DispatcherServlet에 의해 실행된다. 

b. root-applicationContext 

root-applicationContext는 해당 어노테이션을 제외한 어노테이션 Service, Repository등을 스캔하고 DB관련 객체를 생성한다. (스캔이란 : 메모리에 로딩한다는 뜻)

============> 해당 파일은 ContextLoaderListener에 의해 실행된다. ContextLoaderListener를 실행해주는 녀석은 web.xml이기 때문에 root-applicationContext는 servlet-applicationContext보다 먼저 로드 된다.

당연히 servlet-applicationContext에서는 root-applicationContext가 로드한 객체를 참조할 수 있지만 그 반대는 불가능하다. 생성 시점이 다르기 때문이다.

Bean Factory

필요한 객체를 Bean Factory에 등록할 수 도 있다. 여기에 등록하면 초기에 메모리에 로드되지 않고 필요할 때 getBean()이라는 메소드를 통하여 호출하여 메모리에 로드할 수 있다. 이것 또한 IoC이다. 그리고 필요할 때 DI하여 사용할 수 있다. ApplicationContext와 다른 점은 Bean Factory에 로드되는 객체들은 미리 로드되지 않고 필요할 때 호출하여 로드하기 때문에 lazy-loading이 된다는 점이다.
```
___
## UTF-8이란?
컴퓨터는 1 or 0 -> 표현할 수 있는 수는 2의 3승

2의 8승은 256가지 수
알파벳(대문자, 소문자),숫자, 기호등을 표현하려면 2의 8승이 필요하다.  
문자 1개의 표 = 아스키 코드  
8bit -> 1
byte  
RAM은 한 구분에 1Byte를 담을 수 있다. 따라서 RAM은 하나의 문자를 담을 수 있다.
하지만 우리나라 기준 한 글자는 2byte, 중국은 3byte가 필요하다.

세계화가 된 이 시대에 byte를 통일하자! -> UTF-8(3byte)

___
## spring 의존성
1. spring boot devtool 
- 파일 변경시 바로 컴파일 해준다.
2. Lombok
- getter, setter등 자동생성 라이브러리
3. spring data JPA
- JPA를 이용하여 ORM을 사용할 예정
4. Mysql driver
- mysql 접속하기 위해 사용
5. Spring security
- 필터 등 여러가지 기능을 쉽게 구현 (추후 나중에 공부한다.)
6. OAuth2 client
- 카카오 로그인 같은 등 쉽게 구현할 수 있지만 이번에는 노가다로 구현해본다.
7. 