# Socket 통신 - 2

## 코드 구현 - 1

```
var server = require('http').createServer(app);
var root_io = require('socket.io')(server);

root_io.of(/\/(\d+)$/).on('connection', function (socket) {
  const newNsp = socket.nsp;
  let namespace = newNsp.name;
```

### 

## 코드 구현 - 2

```
socket.on('sendchat', async function (data) {
	var data = JSON.parse(data);
	let u_idx = data.u_idx;
	let chatroom_idx = data.chatroom_idx;
	let content = data.content;
	let type = data.type;
	root_io.of(newNsp.name).in(chatroom_idx).clients(async function(err, clients) {
		var count = clients.length;

		let result = await chatsql.insertNewMessage(u_idx, chatroom_idx, content, count, type);				
```



## 코드 구현 - 3

```
root_io.of(newNsp.name).in(chatroom_idx).emit('updatechat', null);
root_io.of(newNsp.name).emit('updatechatlist', null);			
```

