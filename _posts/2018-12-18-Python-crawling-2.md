---
layout: post
title:  "Python & Crawling - 2"
author: SomeBodyHelpMe
tags: [post, python, crawling]
---
# Crawling - 2

## File 열고 닫기 - with

```
with open(filename, 'r') as file:
	for line in file:
		print(line)
```



## .startswith()

```
word = "superman"
print(word.startswith('s'))	# True
```



## split()

인자로 아무것도 넣지 않으면 띄어쓰기로, 인자에 값을 넣으면 그 값을 기준으로 스트링을 쪼갠다

```
string.split()
```



## tuple vs list

공통점 : 순서가 있는 원소들의 집합

차이점 : 각 원소의 값을 수정할 수 없음, 원소의 개수를 바꿀 수 없음



## Matplotlib

* Mathematical Plot Library
* 파이썬에서 그래프를 그릴 수 있게 하는 라이브러리
* 꺾은선 그래프, 막대 그래프 등을 모두 지원



## Dictionary

* { key : value }
* key : 값을 찾기 위해 넣어주는 데이터
* value : 찾고자 하는 데이터



### JSON - Dictionary

* JSON -> Dictionary : **loads()**
* Dictionary -> JSON : **dumps**



## Set

* 중복, 순서가 없는 데이터형
* 교집합 : &
* 합집합 : |
* 차집합 : -
* XOR : ^