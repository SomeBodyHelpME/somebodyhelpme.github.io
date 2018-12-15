---
layout: post
title:  "REST, MySQL"
author: SomeBodyHelpMe
---
# REST API

## REST

* Representational State Transfer

* HTTP URI 로 잘 표현된 리소스에 대한 행위를 HTTP Method로 정의. 리소스의 내용은 json, xml, yaml 등의 다양한 표현 언어로 정의

* ‘무엇을 (HTTP URI 로 정의된 리소스) 어떻게 한다 (HTTP Method + Payload)’ 로 잘 정의된 API 를 REST API 

* URI 와 HTTP 메소드를 이용해 객체화된 서비스에 접근하는 것



## REST의 구성 요소

```
HTTP POST http://localhost:3000/login
{
    "users" : {
        "id" : "myid",
        "pw" : "mypw"
    }
}
```

* 자원(Resource) : URI

* 행위(Verb) : Method

* 표현(Representation) : Body(Message Payload)



## REST의 특징

* Uniform Interface : HTTP표준에만 따른다면 어떤 기술에서 사용 가능한 인터페이스 스타일

* Stateless : 상태를 저장하지 않음

* Cacheable : HTTP 웹 표준을 그대로 사용 => SSL, Cache 기능등을 사용할 수 있음

* Client – Server 구조 : 클라이언트와 서버의 역할이 확실히 구분

* Self – descriptiveness : REST API 메세지만 보고 쉽게 이해 가능한 자체 표현 구조

* Layered System : 다중 계층으로 구성 가능



## HTTP Method

* REST에서는 CRUD(Create Read Update Delete)에 해당하는 4가지의 메소드만 사용

* POST(Create)

* GET(Read)

* PUT(Update)

* DELETE(Delete)



## REST API 설계 가이드

* URI는 정보의 자원을 표현해야 한다. 동사가 아닌 명사 위주로 작성

* 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE) 으로 표현한다

* URI는 리소스만 표현하고, 자원에 대한 행위는 HTTP Method을 표현한다
   GET : users/update/1 (X)  PUT : users/1 (0)

* URI에 리소스명은 복수로 표현한다
   GET : /user/329 (X)  GET : /users/329 (0)

* URI에 파일 확장자는 포함시키지 않는다. (Accept Header 에 담아서 보낸다)
   /images/main.jpg (X)   /images/main accept : image/jpg

* URI 에 슬래시 구분자 ( / ) : 계층 관계를 나타내는데 사용하고 URI 마지막 문자로 슬래시를 포함하지 않는다

* 가독성을 위해 URI에 (-)은 사용,  (_, underscore) 문자를 사용 하는 것 자제

* URI는 소문자가 적합하다





# MySQL

## INSERT문

* INSERT INTO table_name VALUES (value1, value2, ...);

* auto increment 되는 값은 데이터 값을 넣지 않아도 알아서 1씩 증가

* 삽입할 필드는 생략 가능 => 테이블의 column 순서로 데이터 입력

* 특정 필드에만 데이터를 입력할 경우, 입력할 필드 이름만 나열하고 그에 해당하는 데이터를 입력. column 개수와 value 개수 일치해야 함
    ex. INSERT INTO table_name (col1, col2, ...) VALUES (value1, value2, ...);



## SELECT문

* SELECT col1, col2, ... FROM table_name [ WHERE 검색조건 ];

* 테이블의 모든 데이터를 검색 : 컬럼명을 * 로 하면 모든 컬럼 의미
   ex. SELECT * FROM table_name;

* WHERE 문을 사용하여 특정 조건에 맞는 데이터만을 검색
   ex. SELECT * FROM table_name WHERE col1 = value;

* WHERE 조건문이 여러개일 경우( AND / OR )
    ex. SELECT * FROM table_name WHERE col1 = value1 AND col2 = value2;

* 결과 데이터를 정렬 (ORDER BY ) ( cf. 내림차순 : DESC / 오름차순 : ASC )

* LIKE / DISTINCT / LIMIT / COUNT() / AS



## UPDATE문

* UPDATE table_name SET col1 = value1, col2 = value2 WHERE col3 = value3;
   : 테이블에서 col3 의 값이 value3 인 튜플의 col1 값은 value1 로, col2 값은  value2 로 수정



## DELETE문

* DELETE FROM table_name WHERE col1 = value1;
   : 테이블에서 col1 의 값이 value1 인 튜플 삭제



## mysql 모듈

* Node.js 에서 데이터베이스에 접근해 데이터를 생성, 조회, 수정, 삭제 하기 위해 모듈 필요

* 대표적인 오픈소스 RDBMS인 MySQL 지원

* 설치 방법 : npm install mysql

* 모듈 설명 : <https://www.npmjs.com/package/mysql>

* connection 객체를 생성하여 그 객체를 이용해 DB와 통신

* connection 설정은 config 폴더 내에 저장

* connection을 생성하는 방법
  * createConnection()
  * createPool()

* connection 을 사용한 후에 반드시 end(), release() 를 이용해서 connection을 끊어야 한다
   => end(), release() 는 비동기로 수행 => connection.query()의 callback 함수 내에 작성

* connection을 사용하는 방법
  * connection.query(query, [values], callback)
  * query문은 string, values는 query문에 들어갈 동적으로 할당될 변수, callback(err,  result)

* SELECT의 결과값 : [{Object1}, {Object2}, {Object3}, ...]
  * 특정 Object에 접근하기 위해서는 result[i].value

* INSERT / UPDATE / DELETE의 결과값 : 결과값이 담긴 JSON 객체



### createConnection

* 매 번 connection 을 생성 =>  비효율적. 생성될 때 많은 시간이 소모되기 때문

* createConnection() 메소드를 통해 connection 객체를 하나 생성

* 연결 종료 : connection.end();



### CreatePool

* createPool() 메소드를 통해 connection pool을 생성

* connection 을  pool에서 가져와 사용 => createConnecion 보다 효율적

* connection의 개수 제한 O => 반환해주지 않을 경우 connection limit에 걸릴 수 있다.

* connection 반환 : connection.release();
