---
layout: post
title: "SpringBoot Study"
subtitle: ""
date: 2021-04-03 12:00:00 -0400
background: '/img/posts/bg-post.jpg'
---

이 포스팅은 패스트 캠퍼스에서 진행하는 Java 웹 개발 마스터 올인원 패키지를 통해 관리자 페이지를 제작해보면서 SpringBoot에 대해 배운 내용을 정리해보기 위해 작성되었습니다. 포스팅 작성이 서툴러 부족한 부분이 많을 것으로 생각됩니다. 이에 대한 코멘트는 감사히 받겠습니다.
* [나의 git repository](https://github.com/qnbz209/Adminpage-SpringBoot)

SpringBoot?
======

> 자바 플랫폼을 위한 오픈 소스 프레임워크로서 동적인 웹 사이트를 개발하기 위한 여러 가지 서비스를 제공한다.


Rest API
-----

HTTP 프로토콜에 있는 메소드를 활용한 아키텍쳐 스타일이다.
HTTP 메소드를 이용해 CRUD의 개념으로 resource를 처리하기 위해 사용된다.

* HTTP - GET Method
  * 정보를 얻을 때 사용하는 메소드로 주소 창에 파라미터가 노출된다. 브라우저가 주소 캐시를 할 수 있다.
  * e.g. http://localhost:8080/search?id=account&password=1234

* HTTP - POST Method
  * 클라이언트에서 서버로 데이터를 전송할 때 사용되는 메소드로 주소 창에 파라미터가 노출되지 않아 주소 길이 제한이 없다. 브라우저가 주소 캐시를 하지 못한다.
  * e.g. http://localhost:8080/search

* HTTP - PUT/PATCH Method
  * POST 메소드와 마찬기자로 BODY에 데이터가 들어 있으며, 주로 update를 위해 사용된다.

* HTTP - PUT/PATCH Method
  * GET 메소드와 마찬가지로 주소에 파라미터가 들어가며, 데이터를 삭제할 때에 사용된다.


Lombok
-----
Model을 만들고 각 멤버변수에 접근할 수 있는 메소드를 제작할 때, 어노테이션의 설정으로 이를 가능케 하는 라이브러리이다.

e.g.
* @AllArgsConstructor: 모든 매개변수의 생성자 사용
* @NoArgsConstructor: 매개변수가 없는 기본 생성자 사용
* @RequiredArgsConstructor: 초기화 되지않은 final 필드나, @NonNull 이 붙은 필드에 대해 생성자를 생성, 주로 의존성 주입(Dependency Injection) 편의성을 위해서 사용
* @Builder: 빌더 패턴을 사용할때 사용
* @Getter: Entity의 state를 get해오는 함수를 사용할 수 있게 한다.
* @Setter: Entity의 state를 set해주는 함수를 사용할 수 있게 한다.
* @Accessors(chain = true): 체이닝 패턴을 사용할때 사용
* @Data
  * @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor 모두 포함
  * JPA 에서 OneToMany, ManyToOne 같은 부분에 사용하면 toString()에서 문제 발생 @Exclude를 사용해서 제외 하거나 다른 방법으로 설정
* @Autowired: 각 상황에 맞는 Bean을 자동으로 주입해 객체의 의존성을 갖는 부분에 적어 쉽게 의존성을 부여받을 수 있도록 한다.


JPA
------

ORM(Object Relational Mapping)으로, 자바객체와 관계형 데이터베이스의 맵핑을 통해 보다 손쉽게 객체지향을 활용할 수 있도록 도와주는 도구이다.

Entity
-----
Entity란 DB에서 영속적으로 저장된 데이터를 자바 객체로 매핑하여 '인스턴스의 형태'로 존재하는 데이터이다.

* Camel Case: 단어의 시작을 소문자로, 띄워쓰기 대신 대문자를 사용함으로써 단어를 구분해 Java의 변수를 선언할 때 사용된다.
* Snake Case: 단어를 모두 소문자로 표기하면서, 띄워쓰기 때신 '_'를 사용해 데이터베이스의 컬럼에 사용된다.

* e.g.
  * @Entity: 해당 class가 entity임을 명시
  * @Table: 실제 DB 테이블의 이름을 명시
  * @Id: Index primary key를 명시
  * @Column: 실제 DB Column의 이름을 명시
  * @GeneratedValue: Primary key 식별키의 전략 설정


Repository
-----
따로 쿼리문을 작성하지 않아도 CRUD를 사용할 수 있게 한다.

```
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

ERD
------
테이블들간의 상호간의 관계를 정의할 때 사용된다.

e.g.
* @OneToOne: 1 대 1
* @OneToMany: 1 대 N
* @ManyToOne: N 대 1
* @ManyToMany: N 대 N
* fetch = FetchType.{}: {}에 LAZY를 사용한 지연로딩을 통해 연관관계가 걸려있음에도 원하는 값만을 조회할 수 있도록 해준다.
* mappedBy = "": 연관관계에 있는 테이블에서 Foregin Key를 갖는 owner를 넣어 사용한다.

Controller
-----
CRUD에 대한 조작을 실행해줄 메소드로 controller를 선언해 사용하였다.

* @RestController: MVC에서 View에 JSON을 반환해주기 위해 주로 사용된다.
* @RequestMapping: 해당 어노테이션이 선언된 controller가 어느 URL으로 사용될지를 정하기 위해 사용된다.
* @PostMapping, @GetMapping, @PutMapping, @DeleteMapping: 해당 메소드가 불리우는 URL을 정하기 위해 사용된다.
* @RequestBody: Request 요청의 body 부분을 Java 객체로 받을 수 있게 해주는 어노테이션 (주로 JSON을 받을 때 사용된다.)
* @PathVariable: URL에 파라미터가 노출되는 Get 메소드를 사용하는 경우에 이를 깔끔하게 사용할 수 있게 한다.
