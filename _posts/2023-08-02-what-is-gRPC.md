---
title: 了解gRPC
tags: rpc
---

在了解gRPC前，首先要知道RPC和REST的區別。

REST(Representation State Trasfer) 代表一種軟體架構的風格。主要體現在HTTP的方法與URL的結合，以資源為主體，根據GET，POST，PUT，DELETE方法的使用來對資源進行操作，這樣更容易被理解。

RPC(Remote Procedure Call) 代表遠程調用協議。側重於函數的調用或操作，與REST不同，使用者需要知道特定的函數名字才能進行調用。
> POST /getProduct HTTP/1.1
通常一些複雜的操作例如操控遠程設備，調用複雜的算法，就能體現RPC的特點。

那gRPC又是什麼呢？
gRPC是Google對於RPC框架的補充來連結不同的微服務，不同語言直接可以連通。因為有Protobuf，一個序列化與反序列化的標準。正常的gRPC流程就會分成Client和Server，數據經過Protobuf encode翻譯成二進制形式，經過HTTP/2的連接傳輸到Server端，經過解析獲得數據。gRPC利用了HTTP/2 流的特性，在一個TCP長連接中同時發送或接收幾個響應或請求。

即使現在大部分瀏覽器已經支持HTTP/2，瀏覽器無法直接調用gRPC，只能通過gRPC-Web作為一個Proxy來進行調用。而微服務之間的調用/ios andriod app，即可以直接調用，充分發揮gRPC的優點。





[RPC和REST之間有什麼區別](https://aws.amazon.com/cn/compare/the-difference-between-rpc-and-rest/)

[What is RPC? gRPC Introduction](https://www.youtube.com/watch?v=gnchfOojMk4)

