---
layout: post
title:  "Express, Router, PM2"
author: SomeBodyHelpMe
---
## Express

* HTTP 요청에 대하여 라우팅(Routing) 및 미들웨어(Middleware) 기능을 제공하는 웹 프레임워크
  * 라우팅 : 기본적으로 어플리케이션 서버에서 경로를 제어하는 목적으로, 목적지까지 갈 수 있는 여러 경로 중 한 가지 경로를 설정해주는 과정
  * 미들웨어 : 중간에 껴넣는다는 의미로 부가적인 기능이나 처리를 제공하는 목적. 이기종의 환경을 연결해주는 소프트웨어를 가리킴
     ex. body-parser : POST 메소드에서의 Body 내부의 데이터 처리



### 설치

* express-generator 설치 : npm install –g express-generator

* express –h 를 통해 도움말을 살펴볼 수 있음

* express 프로젝트 생성 : express project_name

* 모듈 설치 : npm install (--save, -s 옵션을 줘서 설치한 것이나, package.json 에 기록되어 있는 모듈에 대한 설치)

* 참고 자료 : [http://](http://expressjs.com/ko/4x/api.html)[expressjs.com](http://expressjs.com/ko/4x/api.html)[/](http://expressjs.com/ko/4x/api.html)[ko](http://expressjs.com/ko/4x/api.html)[/4x/](http://expressjs.com/ko/4x/api.html)[api.html](http://expressjs.com/ko/4x/api.html)



### 구성

![component](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2018-04-20+%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB+1.45.48.png)

* bin : 프로그램 실행과 관련된 파일이 들어있는 폴더. 내부에 있는 www 파일을 실행해서 프레임워크를 실행. Port 번호 지정

* node_modules : 이 express에 필요한 module 저장

* public : image, js, css 파일과 같은 정적파일 관리

* routes : url 별로 수행되는 실제 서버의 로직 처리
     index.js 파일로 라우팅 관리

* views : html, jade, ejs 같은 웹 페이지 관리

* app.js : 이 프로젝트의 메인 소스 코드. 미들 웨어 설정, 라우팅 시작

* package.json : module 의 package.json 파일. 프로젝트 관리
  ​                 --save, -s 옵션으로 모듈 정보를 저장



### 기본적인 코드 작성

var express = require(‘express’);

var router = express.Router();

* 모듈식으로 등록하는 개념. 파일 단위로 모듈화를 시켜서 라우팅 등록

* 라우터 단위로 request가 발생하면 실행



module.exports = router;

* 현재 js 파일을 다른 파일에서 사용할 수 있도록 exports

***참고***

var app = express();

* 어플리케이션 전체 영역에서 처리 가능. 앱에 대한 request가 발생할 때마다 실행



### Request

* router.(Method)(‘url’, function(req, res) { });

* Method를 정해준다. (GET, POST, PUT, DELETE ...)

* req.query : url에 Query String 으로 데이터가 넘어옴. url에 따로 표시 X (‘/comment’)
   ex. localhost:3000/comment?board_idx=10  => req.query.board_idx

* req.param : url에 Parameter로 데이터가 넘어옴. url에 /:변수명 표시 (‘/comment/:board_idx)
   ex. localhost:3000/comment/10    => req.params.board_idx

* req.body : JSON body 로 데이터가 넘어옴  => req.body.user_id

* 참고 자료 : [http](http://expressjs.com/ko/4x/api.html)[://expressjs.com/ko/4x/api.html#req](http://expressjs.com/ko/4x/api.html)



### Response

* res.status(statuscode) : HTTP 응답 코드를 설정

* res.send(body) : 클라이언트에 응답을 보냄. JSON 형식으로 body 작성
   body의 내용으로 성공 or 실패 여부, 메세지, 전송할 데이터등을 담음

```
res.status(statuscode).send({
   “message” : “Success”,
   “data” : {
   				“key” : “value”
   }
 }); 
```

* 참고 자료 : [http](http://expressjs.com/ko/4x/api.html)[://](http://expressjs.com/ko/4x/api.html)[expressjs.com/ko/4x/api.html#res](http://expressjs.com/ko/4x/api.html)



## 라우팅

### 라우팅

* 간결하고 관리하기 쉽게 파일 단위로 모듈화를 시켜서 라우팅 등록

* index.js 파일을 통해 폴더별로 정리되어 있는 파일들을 관리



### 라우팅 구조

* app.js 파일에서 routes 폴더를 관리하는 index.js 로 접근

* url path에 맞는 라우터 모듈 파일이 나올 때 까지 계속 index.js 를 통해 내려간다

* 최종 파일에서 그 라우터에 맞는 작업을 수행



## Postman

* 웹에서 테스트 할 경우 한계가 있음
   ex. header, body로 데이터를 보내야 할 때

* API 테스트를 위해 사용

* header, parameter, body (data & file) 에 원하는 데이터를 작성해 테스트를 할 수 있음

* 설치 : [https://](https://www.getpostman.com/)[www.getpostman.com/](https://www.getpostman.com/)

* 주의사항 : Body 에 데이터를 담아서 보낼 때

  * file 없이 데이터를 보낼 경우
    * x-www-form-urlencoded 나 raw 에서 JSON(application/json) 으로 체크를 한 후에 데이터 필드를 작성
    * 데이터 필드에 적힌 값은 그에 맞는 type (string, number …) 적용

  * file 을 포함하여 보낼 경우
    * form-data 에 체크를 한 후 데이터 필드를 작성
    * text 필드에 적힌 값은 string type => 서버에서 처리할 때 형변환을 해줘야 함
    * 이 때, Headers 에서 Content-Type이 x-www-form-urlencoded 라고 세팅되어 있는지 확인 => 체크 해제

## PM2

* PM2 (Process Manager 2) : Node.js 프로세스 관리 도구

* 설치 : npm install –g pm2

* 서버 실행 : pm2 start ./bin/www

* name 옵션을 줄 경우 프로세스에 이름을 할당할 수 있음. 그렇지 않으면 이름은 실행한 파일명이 됨
   ex) pm2 start ./bin/www –name “example”

* 현재 돌아가는 프로세스 목록 확인 : pm2 list

* 프로세스 모니터링 : pm2 monit

* 실시간 로그 확인 : pm2 logs [--lines][--timestamp [format]] [‘all’ | ‘PM2’ | app_name | id]  
   로그 관련 정보 : [http](http://pm2.keymetrics.io/docs/usage/log-management/)[://pm2.keymetrics.io/docs/usage/log-management](http://pm2.keymetrics.io/docs/usage/log-management/)[/](http://pm2.keymetrics.io/docs/usage/log-management/)

* 프로세스의 정보 확인 : pm2 show / describe < app_name | id > 

* 프로세스 관리

  * 종료 : pm2 stop < app_name | id | ‘all’ | json_conf >

  * 재시작 : pm2 restart < app_name | id | ‘all’ | json_conf >

  * 삭제 : pm2 delete < app_name | id | ‘all’ | json_conf >

* 로그파일 저장 장소 : ~/.pm2/logs 
