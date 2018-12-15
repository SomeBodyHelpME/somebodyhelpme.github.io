---
layout: post
title:  "외부 모듈 - Multer, Moment"
author: SomeBodyHelpMe
---
# Multer

* 기존의 방법(x-www-form-urlencoded, application/json)로 파일 업로드 X

* multipart/form-data 방식으로 파일 업로드 가능

* multer 모듈로 생성한 upload 미들웨어가 req에 file 프로퍼티를 추가 
   => req.file로 접근 가능

* diskStorage 엔진으로 로컬폴더에 저장
   cf. The disk storage engine gives you full control on storing files to disk.

* multer-s3 모듈을 이용해 S3에 저장

* 참고 : [https](https://github.com/expressjs/multer)[://github.com/expressjs/multer](https://github.com/expressjs/multer)

### single(fieldname)

* fieldname 프로퍼티로 받은 하나의 파일을 req.file 에 저장

* req.file.location으로 파일 링크 가져옴

### array(fieldname[, maxCount])

* fieldname 프로퍼티로 받은 모든 파일을 배열의 형태로 req.files 에 저장

* maxCount값 이상 업로드 될 경우 에러 처리 가능

* req.files[i].location으로 파일 링크 가져옴

### fields(fields)

* 여러 name으로 여러개의 파일을 req.files에 저장

* fields 는 name과 maxCount(선택사항)을 포함하는 객체의 배열



# Moment

* Date() 객체를 사용하여 날짜를 생성하면, 불필요한 글자까지 포함되어 split 메소드를 사용해야함.
   ex. 2017-05-25T12:25:00.000z 

* 직관적이고 간단한 코드를 통해 시간 표현 가능

* 설치 : npm install --save moment

* 참고 : [https](https://momentjs.com/)[://momentjs.com](https://momentjs.com/)[/](https://momentjs.com/)

* format(‘’) 을 통해 여러 형태로 날짜 표현 가능
* String 의 형태로 리턴
