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

* DB에 저장된 그룹의 이름을 namespace의 이름으로 사용

* 정규식으로 표현 => '/\/(\d+)$/' 

* 그룹 내의 채팅방은 DB에서 채팅방 인덱스와 대응



### 각 그룹별 여러 개의 채팅방 => namespace

* 하나의 채팅방에서 채팅을 할 경우, 채팅방내에 있는 사람에게 알림이 가야함
* 알림을 받아야 하는 사람이 다른 채팅방에 있을 경우, room 개념만 사용하면 보낼 방법이 없다
* 하나의 채팅방을 room에, 여러 채팅방을 포함하는 그룹의 개념을 namespace에 대응
* namespace로 묶여있기 때문에 그 아래 모든 채팅방에 알림을 줄 수 있음



### 채팅 등록 시

1. DB에 채팅 등록
2. 현재 채팅방에 접속중이지 않은 사람들에게는 fcm을 보냄
3. 현재 채팅방에 접속중인 사람은 emit으로 알림



### 현재 접속중인 사람 리스트

* room에 접속하면 그 룸에 부여된 배열에 사용자 index 추가
* room에서 나가면 사용자 index 제거
* 배열은 각각의 namespace + room 별로 모두 다르게 존재



## 채팅방 알림 메소드

### io.of(Nsp).in(Room).emit('event', null)

: namespace가 Nsp이고, room이 Room인 곳에 sender를 포함한 모든 사람에게 전송

### io.of(Nsp).emit('event', null)

: namespace가 Nsp인 곳에 sender를 포함한 모든 사람에게 전송



## 읽음 수 표시

### 순서도

1. 채팅방에 입장할 때, DB에서 현재 채팅방에서 사용자가 마지막으로 읽은 채팅 인덱스를 가져온다
2. 그 이후의 채팅의 읽음 수를 -1 처리한다
3. 채팅 정보를 클라에게 보내준다
4. 채팅 글이 올라올 경우, 채팅방 전체 인원에서 현재 채팅방에 들어와 있는 사람 수만큼 뺀 값을 디비에 저장한다
5. 채팅방에서 나갈 때, 마지막 채팅 인덱스를 DB에 저장한다.





## FCM

FCM을 통해 메시지 등록시, 사진, 비디오, 파일 등록시 다른 사용자들에게 알림

```
var message = { //this may vary according to the message type (single recipient, multicast, topic, et cetera)
	to: client_token,
	data: {
		data : statuscode.uploadMessage,
		result : result
	},
	priority: "high",
	content_available: true
};

fcm.send(message, function(err, response) {
	if(err) {
		console.log("Something has gone wrong!", err);
	} else {
		console.log("Successfully sent with response: ", response);
	}
}); // fcm.send
```



