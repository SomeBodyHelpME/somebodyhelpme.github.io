---
layout: post
title:  "Python & Crawling - 1"
author: SomeBodyHelpMe
tags: [post, python, crawling]
---
# Crawling

## BeautifulSoup

### import

```
import urllib.request
from bs4 import BeautifulSoup

url = "http://www.naver.com"
req = urllib.request.Request(url)
sourcecode = urllib.request.urlopen(url).read()
soup = BeautifulSoup(sourcecode, "html.parser")

print(soup)
```



### find_all & get_text

```
for text in soup.find_all("div", class_="text_area"):
	print(text.get_text())
```



### pagination

```
# url = "http://sports.donga.com/Enter?p=1&c=02"
# url = "http://sports.donga.com/Enter?p=21&c=02"
# url = "http://sports.donga.com/Enter?p=41&c=02"

for i in range(0, 5):
	url = "http://sports.donga.com/Enter?p=" + str((i * 20) + 1) + "&c=02"
	
```



### href 페이지 수집

```
find("a")["href"]
```

