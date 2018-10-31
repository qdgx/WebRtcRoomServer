# WebRtcRoomServer
WebRtcRoom Server，使用Node js开发，信令服务器使用 Socket.IO

Android，iOS，Html，Server均做了实现，若有需要可分别查看。

WebRtcRoomHtml: https://github.com/qdgx/WebRtcRoomHtml

WebRtcRoomAndroid: https://github.com/qdgx/WebRtcRoomAndroid

WebRtcRoomIOS: https://github.com/qdgx/WebRtcRoomIOS

# 接口说明

通过Socket.Io进行数据交互，Json格式

----------------------------------------Client To Server----------------------------------------

1：事件名：createAndJoinRoom    客户端通知服务器创建并加入room中，若room已存在则直接加入 {room}

    room：房间名称，字符串

2：事件名：offer 发送offer消息 {from,to,room,sdp}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    sdp：发送者设备sdp描述，字符串

3：事件名：answer 发送answer消息 {from,to,room,sdp}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    sdp：发送者设备sdp描述，字符串

5：事件名：candidate  发送candidate消息 {from,to,room,candidate{sdpMid,sdpMLineIndex,sdp}}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    candidate：发送者设备candidate描述，Json类型
      sdpMid：描述协议id，字符串
      sdpMLineIndex：描述协议的行索引，字符串
      sdp：sdp描述协议，字符串
 
6：事件名：exit  发送exit消息 {from,room}

    from: 发送者socket连接标识，字符串
    room：房间名称，字符串

----------------------------------------Server To Client----------------------------------------

1：事件名：created   服务器通知客户端信令连接成功 {id,room,peers[{id}]}

    id: 当前socket连接标识，字符串
    room：房间名称，字符串
    peers：Json数组，房间其他客户端socket连接标识集合
      id：房间其他socket连接标识

2：事件名：joined   服务器通知客户端当前房间有新连接加入 {id,room}

    id: 新socket连接标识，字符串
    room：房间名称，字符串

3：事件名：offer  服务器转发offer消息 {from,to,room,sdp}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    sdp：发送者设备sdp描述，字符串

4：事件名：answer  服务器转发answer消息 {from,to,room,sdp}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    sdp：发送者设备sdp描述，字符串

5：事件名：candidate  服务器转发candidate消息 {from,to,room,candidate{sdpMid,sdpMLineIndex,sdp}}

    from: 发送者socket连接标识，字符串
    to:接收者socket连接标识，字符串
    room：房间名称，字符串
    candidate：发送者设备candidate描述，Json类型
       sdpMid：描述协议id，字符串
       sdpMLineIndex：描述协议的行索引，字符串
       sdp：sdp描述协议，字符串

6：事件名：exit  服务器转发exit消息 {from,room}

    from: 发送者socket连接标识，字符串
    room：房间名称，字符串
