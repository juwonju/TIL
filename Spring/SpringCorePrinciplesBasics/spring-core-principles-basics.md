# 스프링 핵심 원리 - 기본편

> [스프링 핵심 원리 - 기본편](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)

# 객체 지향 설계와 스프링

## 자바 진영의 추운 겨울과 스프링의 탄생

2000년 초기에는 자바 기술의 표준이 **EJB(Enterprise Java Beans)**.  
이 EJB는 이론 자체는 좋았지만, 복잡하고 어렵고 느리다는 치명적인 단점 존재.

그래서 이후에 EJB를 버리고 다시 순수한 옛날 자바, 즉 **POJO(Plain Old Java Object)**로 돌아가자는 기조가 생겼다.

이렇게 EJB를 대체하고자 새로 오픈소스 두 가지가 만들어졌는데, 바로 Rod Johnson의 **Spring**과 Gavin King의 **Hibernate**.

- 스프링
    - EJB 컨테이너 대체
    - 단순함의 승리
    - 사실상 현재 표준 기술
- 하이버네이트
    - EJB 엔티티 빈 기술을 대체
    - 하이버네이트를 기반으로 만든 **JPA(Java Persistence API)**가 새로운 자바 표준으로 정의됨

JPA 같은 표준 기술은 인터페이스만 있고, 구현체는 따로 만들어야 한다.  
그래서 지금은 JPA라는 표준 인터페이스와 그 구현체들로 Hiberante, EclipseLink 등이 존재함.  
결과적으로 자바 ORM 시장은 JPA가 지배하고, 구현체로는 80% 이상이 Hibernate.

따라서 **자바 진영의 제일 중요한 두 가지는 스프링과 JPA**.

### 스프링 탄생

2002년 Rod Johnson(로드 존슨)의 책이 출간되어 EJB의 문제점을 지적함.  
EJB 없이도 충분히 고품질의 확장 가능한 애플리케이션을 개발할 수 있음을 보여주고, 30,000 라인 이상의 기반 기술을 예제 코드로 선보임.  
여기에 지금 스프링 핵심 개념과 기반 코드가 들어있다(BeanFactory, ApplicationContext, POJO, 제어의 역전, 의존관계 주입).

책 출간 직후 Juergen Hoeller(유겐 휠러), Yann Caroff(얀 카로프)가 로드 존슨에게 오픈소스 프로젝트를 제안함.  
스프링의 핵심 코드의 상당수는 유겐 휠러가 지금도 개발.  
**스프링 이름**은 전통적인 J2EE(EJB)라는 겨울을 넘어 **새로운 시작이라는 뜻**으로 지음.

왜 스프링을 쓰는데 이런 역사를 알아야할까?  
강의의 시작은 스프링의 처음과 같다. 스프링과 비슷한 코드를 짜면서 한 단계씩 왜 스프링이 필요하고 대단한지 느끼게 될 것.

## 스프링이란?

스프링은 특정 하나를 지칭하기 보다는 여러 기술들의 모음이다.

### 스프링 생태계

- 필수
    - 스프링 프레임워크
    - 스프링 부트
- 선택
    - 스프링 데이터
    - 스프링 세션
    - 스프링 시큐리티
    - 스프링 Rest Docs
    - 스프링 배치
    - 스프링 클라우드

### 스프링 프레임워크

- 핵심 기술 : 스프링 DI 컨테이너, AOP, 이벤트, 기타
- 웹 기술 : 스프링 MVC, 스프링 WebFlux
- 데이터 접근 기술 : 트랜잭션, JDBC, ORM 지원, XML 지원
- 기술 통합 : 캐시, 이메일, 원격접근, 스케줄링
- 테스트 : 스프링 기반 테스트 지원
- 언어 : 코틀린, 그루비

이러한 스프링 기술 중에 가장 중요한 것이 스프링 프레임워크이고, 이 모든 기술을 사용하도록 도와주는 것이 스프링 부트.  
이 **강의에서 초점**을 두는 부분은 **스프링 프레임워크의 핵심 기술(스프링 DI 컨테이너, AOP, 이벤트, 기타)**. 나머지는 전부 파생적인 부분이다.

### 스프링 부트

- 스프링을 편리하게 사용할 수 있도록 지원, 최근에는 스프링 프레임워크와 함께 거의 기본으로 사용
- 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
- Tomcat 같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 됨
- 손쉬운 빌드 구성을 위한 starter 종속성 제공(라이브러리를 쓸 때 필요한 것들을 알아서 땡겨줌)
- 스프링과 3rd party(외부) 라이브러리 자동 구성
- 메트릭(운영 단계), 상태 확인, 외부 구성 같은 프로덕션 준비 기능 제공
- 관례에 의한 간결한 설정

**스프링 부트**는 스프링 프레임워크와 **별도로 사용할 수 있는 것이 아니다**.  
스프링 부트는 여러 스프링 프레임워크, 데이터 등의 것들을 중간에서 **편리하게 사용할 수 있게 기능을 제공**하는 것이다.  어떻게 보면 껍데기 기능.  
말 그대로 프레임워크가 돌아가도록 도와주는 기술이지 , 스프링 부트만으로 돌아가는 것은 아니다.

### 스프링 단어?

스프링이라는 단어는 문맥에 따라 다르게 사용되기도 한다.

- 스프링 DI 컨테이너 기술
- 스프링 프레임워크
- 스프링 부트, 스프링 프레임워크 등을 모두 포함한 스프링 생태계 전반

### 스프링 핵심 개념

왜 스프링을 만들었을까? 스프링의 핵심은?

- 스프링은 자바 언어 기반의 프레임워크
- 자바 언어의 가장 큰 특징 - **객체 지향 언어**
- 스프링은 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크
- 스프링은 **좋은 객체 지향 애플리케이션을 개발할 수 있게 도와주는 프레임워크(도구)**

단순히 스프링의 API 사용법을 아는 게 아니라, 핵심 컨셉을 알아야 한다.

## 좋은 객체 지향 프로그래밍이란?
