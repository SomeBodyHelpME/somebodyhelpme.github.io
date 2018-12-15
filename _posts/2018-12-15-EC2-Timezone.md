---
layout: post
title:  "EC2 인스턴스의 Timezone 변경"
author: SomeBodyHelpMe
---
## EC2 인스턴스의 Timezone 변경

![timezone1](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2018-05-25+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+6.53.53.png)

1. sudo rm /etc/localtime 입력

2. sudo ln –s /usr/share/zoneinfo/Asia/Seoul /etc/localtime 입력

3. date 라고 쳤을 때 KST라고 나오면 끝!

![timezone2](https://s3.ap-northeast-2.amazonaws.com/twentythirdsopt/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2018-05-25+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+6.58.53.png)
