---
title: Socket.IO 与 WebSocket的区别和关系
date: 2024-11-15 10:10:46
tags: ["Websocket", "Socket.io"]
---

WebSocket是一个独立的协议，基于 TCP，可通过持久的单套接字连接在客户端和服务器之间实现双向、全双工通信。

Socket.IO是一个实时库，可实现 Web 客户端和服务器之间的低延迟双向通信。Socket.IO 建立在 WebSocket 协议之上，并提供额外的功能，例如自动重新连接、广播支持或回退到HTTP 长轮询。

WebSocket 是一种在客户端和服务器之间实现双向实时通信的技术。相比之下，Socket.IO 是一个在 WebSockets 之上提供抽象层的库，可以更轻松地创建实时应用程序。