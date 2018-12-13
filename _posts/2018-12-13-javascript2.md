# Node.js

* Javascript 기반의 서버 플랫폼

* Single Thread 기반의 비동기 I / O 지원

* Google Chrome V8 엔진으로 개발

* 이벤트 기반의 프로그래밍 모델 사용
* File, Network 등에 대해서 비동기 IO 처리를 하는 서버 미들웨어



## Single Thread 기반의 비동기 I / O 지원

* 상황 : 3가지 일을 해야 한다. 빨래, 설거지, 청소 각각 한 시간씩 걸린다.

* 빨래를 다 하고 나서 그 다음에 설거지를 다 하고, 그 다음에 청소를 한다. => 총 3시간이 걸린다!
   

* **방법 1** : 3명이서 각각 하나의 일을 맡아 수행한다. 
  * 동기방식, Thread를 여러개 만들어서 동시에 일을 처리
  * 동기 방식은 작업 요청이 들어올 때마다 Thread를 여러 개 만들어 동시에 일을 처리
  * 일이 많아질수록 Thread를 더 많이 만들어야 하므로 메모리 사용량 계속 증가. 동기화의 문제도 있음

* 방법 2 : 각각의 일을 수행하는 업체가 있다.
  * 업체에 전화를 건다.하나의 작업을 하나의 업체에 맡긴다. 작업이 끝나면 알려달라고 말한다.
  * 비동기방식. 한 개의 Thread로 여러 개의 일을 요청 후 결과를 받는 방식(이벤트)
  * 뭐가 먼저 될 지는 모름
  * 작업이 아무리 많아도 시스템 리소스의 변화가 없다.
  * Node.js 의 방식 -> 대규모 네트워크에 적합 

##이벤트 기반

![eventloop](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/KakaoTalk_Photo_2018-12-12-18-43-21.jpeg)

* Event Loop 는 NodeJS의 싱글 쓰레드에서 돌아가며 I/O Bound 작업들을 비동기적으로 처리해주기 위해서 필요하다. 

* I/O 처리나 네트워크 처리 등이 발생하면 이벤트를 요청하고 다른 작업을 수행한다.

* 이벤트처리가 완료되면, 콜백을 받아 다시 작업을 수행한다.



## Node.js 장, 단점

### 장점

* Javascript 를 사용

* 구글이 제공하는 V8 엔진을 사용

* 성능이 매우 빠름 : **Single Thread 기반의 비동기 I/O처리. 이벤트 처리 방식**

* 시스템 리소스의 부하가 적음

### 단점

* 하나의 작업 자체가 시간이 많이 걸리면, 전체 시스템의 성능 급격하게 떨어짐

* V8 성능 이슈 : Garbage Collection시 CPU의 사용률 증가

* 멀티코어 머신에서 CPU 최적화 X

* 코드의 가독성 떨어짐 -> 유지 보수 어려움. Callback Hell

* 에러가 날 경우 프로세스 자체가 죽는다



# 기본 내장 모듈

## URL

* url 모듈 : url 정보를 파싱할 때 사용하는 모듈

* url 정보를 파싱하여 객체로 가져와 분석, 문자열로 바꿔주는 기능등을 수행

* 주요 메소드
  * parse(urlStr) : url 문자열을 url 객체로 변환해 리턴
  * format(ulrObj) : url 객체를 url 문자열로 변환해 리턴
  * resolve(from, to) : 매개변수를 조합해 완전한 url문자열을 생성해 리턴

* 그 외의 메소드 : [https](https://nodejs.org/dist/latest-v8.x/docs/api/url.html)[://nodejs.org/dist/latest-v8.x/docs/api/url.html ](https://nodejs.org/dist/latest-v8.x/docs/api/url.html)



## Query String

* query문?
  * HTTP에서 데이터를 전달하는 방식
  * url path와 query는 ? 로 구분
  * key1=value1&key2=value2&…
  * http://localhost:3000/test?key1=value1&key2=value2

* querystring 모듈 : url 객체의 query 와 관련된 모듈

* query문을 파싱하여 JSON 객체로 반환 

* 주요 메소드
  * parse(queryString) : query 문자열을 객체로 변환해 리턴
  * stringify(JSONObject) : 객체를 query 문자열로 변환해 리턴

* 그 외의 메소드 : <https://nodejs.org/dist/latest-v8.x/docs/api/querystring.html>



## File System

* File System 모듈 : 파일을 읽고 쓰는데 사용하는 모듈

* 파일 읽기, 쓰기, 디렉토리 생성, 열기

* 주요 메소드
  * readFile(path[, options], callback)
  * readFileSync(path[, options], callback)
  * writeFile(path, data[, options], callback)
  * writeFileSync(path, data[, options], callback)

* Sync가 붙어 있는 메소드는 동기방식

* 그 외의 메소드 : [https://](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[nodejs.org](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[/](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[dist](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[/latest-v8.x/docs/](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[api](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[/](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)[fs.html](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)



## Crypto

* Crypto 모듈 : 문자열을 암호화, 복호화, 해싱하는 모듈

* 비밀번호를 해싱하여 저장하는데 주로 사용

* 주요 메소드
  * createHash(algorithm)
  * update(string)
  * digest(encoding)
  * randomBytes(length, callback)
  * pbkdf2(string, salt, iterations, length, algorithm, callback)

* 그 외의 메소드 : [https://](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[nodejs.org](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[/](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[dist](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[/latest-v8.x/docs/](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[api](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[/](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[crypto.html](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)[ ](https://nodejs.org/dist/latest-v8.x/docs/api/crypto.html)

### 단순 방식 암호화

* crypto.createHash(algorithm)	: 사용할 해시 함수 선택
  ​	   .update(string) 			: 선택한 해시 함수와 string을 해싱하는 과정
  ​           .digest(encoding);		: encoding된 digest 코드를 만듬

  의 방법으로 string을 해싱한다.

* Hashing Algorithm : SHA256, SHA512, SHA1, MD5…

* 주로 SHA256, 최근에는 SHA512 많이 사용

* Encoding으로는 data64, hex 등이 사용

* 레인보우 테이블을 가진 레인보우 공격에 취약하다! 

* 실제로는 절대 이 방법만 사용해서는 안됨. 하나마나한 해싱 

### Salt

* Salt : 해싱을 할 때 추가되는 바이트 단위의 임의의 문자열

* Salt를 해싱할 문자열에 추가하여 해싱하는 것을 Salting 이라고 한다

* Salt와 암호화할 String을 섞어 해시 함수에 넣어 digest 생성

* 모든 String에 같은 Salt를 사용하면 무용지물!

* 랜덤바이트를 생성하여 임의의 Salt 정보를 생성 -> DB에 Salt 값을 같이 저장

### Key Stretching

* String의 digest를 생성 -> digest를 입력 값으로 다시 digest 생성 -> 반복 

* 동일한 횟수만큼 해시해야만 일치 여부 확인할 수 있다

* digest를 생성할 때 어느 정도 시간이 소요되게 설정 => brute-force attack에 대비

### Salt + Key Stretching

![Salt+KeyStretching](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/key_stretching.png)

* Salt와 String을 해시함수에 넣는 과정을 반복

* 반복횟수가 많아 질수록 복호화하기 어려워지지만 그만큼 시간도 많이 소모 

* crypto.randomBytes(length, callback) 으로 랜덤 salt 생성

* crypto.pbkdf2(string, salt, iterations, length, algorithm, callback) 으로 해싱

* 생성된 값들은 toString을 사용하여 인코딩 해줘야 함 

* 해싱 알고리즘으로는 검증된 SHA256, SHA512 등을 선택

* length는 해싱된 문자열의 길이로 임의로 설정