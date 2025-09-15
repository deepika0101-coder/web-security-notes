## HTTP header's :-

`HTTP header` - `X-Forwarded-For ` is widely used HTTP request header. `is a standard header for identifying the origin ip of client connecting through proxy server`.(Standard version - `Forwarded`(less used))

- `rightmost ip recent proxy . leftmost origin client ip`.
```
X-Forwarded-For: <client>, <proxy>
X-Forwarded-For: <client>, <proxy>, …, <proxyN>
```
- For example, an IPV6 client IP in the first header, an IPV4 client IP in the second header, and an IPV4 client IP and an IPV6 proxy IP in the third example:

```
X-Forwarded-For: 2001:db8:85a3:8d3:1319:8a2e:370:7348
X-Forwarded-For: 203.0.113.195
X-Forwarded-For: 203.0.113.195, 2001:db8:85a3:8d3:1319:8a2e:370:7348
```

- client connect's to server the client's ip is written in server logs. but if it passes through anytype proxy the server's sees final proxy ip of little use.if the proxy is load-balacer of same deployment. so X-Forwarded-For is used.

- `worst case is if your backend support's HTTP/2 and (client) the browser also support's it. but your load balancer support's HTTP/1.1 than you did a huge wastage of resources. as when client will try to setup tls connection with balancer it will terminate it ,hence your browser will endup with 6 tcp connection's (boom..).`
