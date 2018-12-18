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
