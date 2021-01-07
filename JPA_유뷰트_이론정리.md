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
