![2](https://github.com/dino-21/STEP7_replycnt_aop_tx/assets/80396471/fbf10b46-b00f-4d43-9650-efa84e6d65cf)
![9](https://github.com/dino-21/STEP7_replycnt_aop_tx/assets/80396471/7baf42e4-fccd-40f6-9f85-3c773e89ba7e)
![4](https://github.com/dino-21/STEP7_replycnt_aop_tx/assets/80396471/080282a2-05ce-42b9-9eb6-c175fa14ab3a)

1 AOP이해하기
- 업무 로직을 포함하는 기능을 핵심 기능(Core Concerns)
- 핵심 기능을 도와주는 부가적인 기능(로깅, 보안)을 부가기능(Cross-cutting Concerns) 이라고 부른다.


2 Spring AOP 특징
1. Spring은 프록시 기반 AOP를 지원한다.
2. 프록시(Proxy)가 호출을 가로챈다(Intercept)
3. Spring AOP는 메서드 조인 포인트만 지원한다.


​3 Spring AOP의 구현 방식

1. XML 기반의 POJO 클래스를 
이용한 AOP 구현
2. @Aspect 어노테이션을 
이용한 AOP 구현



4  스프링 AOP @구현 
pom.xml 
 -  maven 라이브러리



5 @Around 외에 타겟 메서드의 Aspect 실행 시점을 지정할 수 있는 - 어노테이션
xml

<aop:before>
<aop:after-returning>
<aop:after-throwing>
<aop:after>
<aop:around>



어노테이션
@Before(이전) 
@After(이후)
@AfterRunning
@AfterThrowing
@Around


6 AOP 실습 프로젝트 만들기
ex04만들기

7 pom.xml파일에
aspectjweaver 라이브러리 추가


8 org.zerock.service 패키지 만들고 서비스 인터페이스와 클래스 구현
SampleService.java   인터페이스
SampleServiceImpl.java

9 AOP 설정 
root-context.xml 선택해서 네임스페이스에 aop와 context를 추가

10 AOP 테스트 

11 add메서드전에 로그 찍히는지 확인

12 파라미터 추적되는지 확인


13 @AfterThrowing  
예외 발생 테스트 코드

14 @Around와 ProceedingJoinPoint
 SampleServiceTests.java  테스트파일 

@Around가 먼저 동작하고,
@Before등이 실행된 후에 메서드가 실행되는데 
걸린 시간이 로그로 기록됨




15 스프링에서 트랜잭션 관리
기존 프로젝트에서 root-context.xml에서 Namespaces 탭에서 aop항목, tx항목을 체크

16 댓글과 댓글 수에 대한 처리
오라클에서 alter 테이블하기
alter table tbl_board add(replycnt number default 0);


17 BoardVO 수정  코드 추가 – 댓글의 숫자를 의미하는 인스턴스 변수를 추가

BoardMapper 인터페이스에 새롭게 replyCnt를 업데이트하는 메서드를 추가

BoardMapper.xml 수정


18 
ReplyServiceImpl.java 수정  @Transactional의 처리가 필요

19  list.jsp파일     댓글의 숫자를 반영한다.
<td><a class="move" href='${board.bno}'> ${board.title}</a>  
                       <b>[  <c:out value="${board.replyCnt}" />  ]</b></td>

20 댓글을 작성하고 삭제하고 확인
