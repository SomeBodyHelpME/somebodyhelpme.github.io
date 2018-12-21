---
layout: post
title:  "Chatting - Socket.io"
author: SomeBodyHelpMe
tags: [post, Node.js, socket.io]
---
# Socket 통신

## 구현해야 할 기능

* 실시간 채팅 기능
* 읽음 수 표시
* 사진, 비디오, 파일 업로드
* 각 그룹별 여러 개의 채팅방 => 카카오톡 채팅방보다 depth가 더 깊다 => 정규식 사용



## 실시간 채팅 기능

```
var server = require('http').createServer(app);
var root_io = require('socket.io')(server);

root_io.of(/\/(\d+)$/).on('connection', function (socket) {
  const newNsp = socket.nsp;
  console.log('Namespace : ', newNsp.name);
  let namespace = newNsp.name;
  
  socket.on('sendchat', async function (data) {
		var data = JSON.parse(data);
		let u_idx = data.u_idx;
		let chatroom_idx = data.chatroom_idx;
		let content = data.content;
		let type = data.type;
		root_io.of(newNsp.name).in(chatroom_idx).clients(async function(err, clients) {
			var count = clients.length;
			
			let result = await chatsql.insertNewMessage(u_idx, chatroom_idx, content, count, type);
			if (!result) {
				root_io.of(newNsp.name).in(chatroom_idx).emit('updatechat', null);
				root_io.of(newNsp.name).emit('updatechatlist', null);
			} else {
				root_io.of(newNsp.name).in(chatroom_idx).emit('updatechat', result);
				root_io.of(newNsp.name).emit('updatechatlist', result);
			}
		});
		
	});
  
});
```

### 각 그룹별 여러 개의 채팅방 => 정규식

/\/(\d+)$/



## 읽음 수 표시

### 순서도

1. 채팅방에 입장할 때, DB에서 현재 채팅방에서 사용자가 마지막으로 읽은 채팅 인덱스를 가져온다
2. 그 이후의 채팅의 읽음 수를 -1 처리한다
3. 채팅 정보를 클라에게 보내준다
4. 채팅 글이 올라올 경우, 채팅방 전체 인원에서 현재 채팅방에 들어와 있는 사람 수만큼 뺀 값을 디비에 저장한다
5. 채팅방에서 나갈 때, 마지막 채팅 인덱스를 DB에 저장한다.







