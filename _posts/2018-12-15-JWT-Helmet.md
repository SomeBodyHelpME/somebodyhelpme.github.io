---
layout: post
title:  "보안 - JWT, Helmet"
author: SomeBodyHelpMe
---
# JWT

## Cookie / Session / Token

* Cookie : 사용자 인증 정보를 쿠키에 담아서 클라이언트가 저장

* Session : 사용자 정보를 서버에 저장 => 사용자가 많아지거나 서버가 확장될 때 문제

* Token : 암호화된 정보가 오고가기 때문에 보안적인 측면에서 안전 + 서버에 부담 X



## JSON Web Token

* JSON 포맷으로 통신하기 때문에 어떤 Client 에서든 Data 통신에 JSON을 이용하면 토큰을 이용할 수 있다

* 수많은 프로그래밍 언어(C, Java, Python, C++, R, C#, PHP, Javascript, Ruby, Go, Swift 등)에서 지원

* 자가 수용적(Self-contained) : JWT는 필요한 모든 정보를 자체적으로 가지고 있다. + 검증됐다는 것을 증명해주는 signature 포함하고 있다



### JWT 기본 구성

* 헤더(Header) : JWT 웹 토큰의 헤더 정보
  * typ : 토큰의 타입, JWT만 존재
  * alg : 해싱 알고리즘. (HMAC SHA256 or RSA). 헤더를 암호화 하는게 아니다. 토큰 검증시 사용

* 정보(Payload) : 실제 토큰으로 사용하려는 데이터가 담기는 부분

* 서명(Signature) : Header와 Payload의 데이터 무결성과 변조 방지를 위한 서명

  ​			Header 와 Payload의 인코딩한 값을 합친 후, Secret 키와 함께 Header의 해싱 알고리즘으로 인코딩



### JWT 구조

* JWT는 [Header Payload Signature] 각각 JSON 형태의 데이터를 base 64 인코딩 후 합친다

* Header . Payload . Signature 순서로 . 을 이용해 합친다




### jsonwebtoken

* http 헤더 설정을 바꿔주는 모듈

* 설치 : npm install --save jsonwebtoken

* 참고 자료 : [https://](https://www.npmjs.com/package/jsonwebtoken)[www.npmjs.com/package/jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) 

  ​		 https://jwt.io](https://jwt.io/)

* 주요 메소드
  * jwt.sign(payload, secretKey, option)
    * secretKey : 임의의 문자열, 랜덤으로 만들어 서버가 가지고 있음 
    * option : 알고리즘, Token 유효기간
  * jwt.verify(token, secretKey)



### JWT 인증 과정

![jwt](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2018-05-31+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+5.44.27.png)

1. 클라이언트가 로그인을 한다

2. 로그인 정보를 바탕으로 secret key를 이용해 토큰을 생성한다(sign method 사용)

3. 로그인이 성공 시, 토큰을 준다 => 클라에서 저장

4. 클라이언트가 사용자 정보가 필요한 API를 요청할 때, token을 header에 담아 같이 보낸다

5. token 정보를 확인하여 유효한지 파악한다

6. 들어온 정보로 얻은 데이터를 포함한 response를 보내준다



# Helmet

* HTTP 헤더 정보를 설정하는 모듈

* 많이 알려진 웹 취약점으로부터 앱을 보호

* 설치 : npm install --save helmet

* 참고자료 : [https://](https://www.npmjs.com/package/helmet)[www.npmjs.com](https://www.npmjs.com/package/helmet)[/package/helmet](https://www.npmjs.com/package/helmet)

* 적용 방법 : app.js 파일에 추

   ```
  var helmet = require(‘helmet’);
  app.use(helmet());
   ```

### 참고

* **csp**는 Content-Security-Policy 헤더를 설정하여 XSS(Cross-site scripting) 공격 및 기타 교차 사이트 인젝션을 예방합니다.

* **hidePoweredBy**는 X-Powered-By 헤더를 제거합니다.

* **hpkp**는 Public Key Pinning 헤더를 추가하여, 위조된 인증서를 이용한 중간자 공격을 방지합니다.

* **hsts**는 서버에 대한 안전한(SSL/TLS를 통한 HTTP) 연결을 적용하는 Strict-Transport-Security 헤더를 설정합니다.

* **ieNoOpen**은 IE8 이상에 대해 X-Download-Options를 설정합니다.

* **noCache**는 Cache-Control 및 Pragma 헤더를 설정하여 클라이언트 측에서 캐싱을 사용하지 않도록 합니다.

* **noSniff**는 X-Content-Type-Options 를 설정하여, 선언된 콘텐츠 유형으로부터 벗어난 응답에 대한 브라우저의 MIME 가로채기를 방지합니다.

* **frameguard**는 X-Frame-Options 헤더를 설정하여 clickjacking에 대한 보호를 제공합니다.
* **xssFilter**는 X-XSS-Protection을 설정하여 대부분의 최신 웹 브라우저에서 XSS(Cross-site scripting) 필터를 사용하도록 합니다.
