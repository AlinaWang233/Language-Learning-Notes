# HTTP
前端： 终端 - 前端路由 - 页面 - 状态管理 - API接口 - HTTP请求

后端： 数据库 - 业务逻辑 - 后端路由 - 请求解析 - HTTP请求

## HTTP protocol
边界： 开始 结束 ||
携带信息：什么消息， 消息类型

Request/Status Line - Header - Body

Request Method: GET/HEAD/POST/PUT(full)/DELETE/CONNECT/OPTIONS/TRACE/PATCH(part)

Process：
```
业务层： client server
服务治理层：service/govermance
中间件层：middleware 
路由层: n/a  route
协议编（解）码层: codec
传输层：transport
```

Disadvantage

HTTP1: 队头阻塞，传输效率低， 明文传输不安全

HTTP2： （improve）多路复用，头部压缩，二进制协议

QUIC：基于UDP（不是TCP）解决队头阻塞，加密减少握手，支持快速启动

## Design and realization
![Alt text](http_img/structure.png)
API design: simple, understandable
middleware: onion(common wrap around core)
router: prefix tree
protocol: don't store contexts inside a struct type: pass a Context to each function as the first parameter; to read & write on connection, pass the conn
network: B(blocked)IO/NIO(netpoll)

## Optimization
### Network Package
go net
- store all headers
- less times to use system
- reuse allocation space
- read multiple times
=> go net with bufio(buffer)
![Alt text](http_img/bufio.png)
**better for streams & small package**

netpoll
- store all headers(2 half linked nodes)
- copy complete body(2 half linked nodes)
netpoll with nocopy peek
- allocation enough buffer(headers together & body together in one buffer instead of nodes)
- limit max buffer size
**better for mid & large package and better latency**

### Protocol
**header**
boundary of header line:\r\n => find \n and check whether there's a \r in front

better: SIMD(single instruction multiple data) ex. sonic

filter using the first char of header key & byte slice (better than byte) to manage corresponding header
- con: no map structure

stadardized header key format
- pro: better efficiency to transform (40x faster than net.http)
- con: extra space & cumbersome to change hashing method

**requestContext pool**
- pro: less allocation, more reusability, less pressure for GC
- cons:extra reset logic, request validity, difficult to locate problems
## Industry


