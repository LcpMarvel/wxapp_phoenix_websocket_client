## Getting started

```javascript
  this.socket = new Websocket(`${app.serverHost('wss')}/socket`)
  this.socket.connect()

  // 你可以添加 callbacks 到 socket 中

  // 事件如下: 
  // connectSocketSuccess, connectSocketFail, connectSocketComplete
  // onSocketOpen
  // onSocketError
  // sendSocketMessageSuccess, sendSocketMessageFail, sendSocketMessageComplete
  // onSocketMessage
  // onSocketClose

  this.socket.addCallbacks('connectSocketSuccess', (res) => { console.log('connectSocketSuccess', res) })

  this.channel = this.socket.addChannel(channelName, joinParams || {})
  this.channel.join()

  this.channel.push("new_progress")
    .receive("ok", ({ percent }) => {
      this.setPercent(percent)
    })
    .receive("timeout", () => { console.log('timeout') })

  this.channel.on("new_progress", ({ percent }) => {
    this.setPercent(percent)
  })

  // 该库会自动管理websocket的重连, 如果想切断调用
  this.socket.disconnect() // 接受两个参数, opts - 参考[微信文档](https://mp.weixin.qq.com/debug/wxadoc/dev/api/network-socket.html#wxclosesocket), callback - 回调函数
```
