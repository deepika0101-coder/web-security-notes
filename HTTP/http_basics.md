## __HTTP__
- http protocol is used to fetch files. it is used mainly in`client-server artitechture`. Request are initiated by the browser. Document is constructed from text,images,scripts etc.
- client server exchange messages (instead of stream of data).
- HTTP needs reliable protocol like `tcp or tls-encrypted `tcp connection. HTTP also used to post data to server,like `form result's`. can be used to fetch part of document to update web page.

## __Component's of HTTP-based systems:__
- request sent by `user-agent`(mostly `browser` or `proxy` on behalf) but it can be anything like `web-crawler`(robot crawls through web pages to update index's in search-engine(ex-google)).
- numerous entities b/w client-server like proxies 

### I am not continuing with the complete notes as the docs are already very consised so...

## __Proxies (Wikipedia)__
- a proxy act's as a intermediatiry b/w client & server;
- client sometime direct's request to the proxy server there it get `evaluated and network transaction`(transfer that HTTP request further to server) get performed. so it is basically helps in `load balancing`(distributing request b/w many server(no overwhelming)),`security`(no exposure of true origin ip).


## __Types:-__
- proxy can reside on same computer or in b/w. proxy that passes unmodified request and responses is a `gateway`or `tunneling proxy`.

- forward-proxy is internet facing retreive data from wide range of resource.
- reverse-proxy is internal-facing do `laod-balancing,authentication,decryption,caching`.

## __Open proxies(forward proxy):-__
- there are hundreds of thousands" of open proxies.
- `it reveals it's identity as proxy server but not origin ip address`.
- `HTTP header` - `X-Forwarded-For ` is widely used HTTP request header. `is a standard header for identifying the origin ip of client connection through proxy serve`r.(Standard version - `Forwarded`(less used))

```
X-Forwarded-For: <client>, <proxy>
X-Forwarded-For: <client>, <proxy>, …, <proxyN>
```
- content filtering can be also done by proxies through administrative provilege restrict content or authorize access.

- __Insight:-__ proxies works at application layer.

### __proxies(mdn)__
- proxies caching depends on `cache-control header: private`
means shared proxies and CDN could not cache it and if they there is possibilites of caching login credentials or other critical info. then it is prone to attacks.

  - `caching` - it stores frequently accessed data for a short period of time. if it allow's accessing unauthorized data the it is vunlerable.

  - `logging` - where it store data permanently for audit's. and if it store's user credential's then it is vulnerable.

## __Session authentication:-__
- it allows the server to rember the user when they log's in. so you don't have to renter the credential's again-n-again.

### __session authentication using cookies:-__
- `step1` - user logs in.
- `server validate credential's` by checking in database.

- if correct then it `create a session id`(random string).

- stores `session id in database or memory mapped to user-specific data`.
- `server send's set-cookie header` which has session id etc.

```pgsql
HTTP/1.1 200 OK  
Set-Cookie: sessionId=ABC123XYZ456; HttpOnly; Secure; Path=/; SameSite=Strict
```
- another time when user make request to same domain another page browser include's cookie which has session-id.

```vbnet
GET /dashboard HTTP/1.1  
Host: example.com  
Cookie: sessionId=ABC123XYZ456
```
- server authenticate user using the cookie matching session id and checking if it is expired or not.


## __HTTP/1.1__
- `browser will establish a tcp connection to the server.(it uses two way communication).you make one request from tcp (get html). then that part is busy you cant send another request as long as your request getting processed(socket is busy).but the socket is very underutilized as it capable of handling muuch.. more request.`

 - ` if i parse index.html and realize i need /man.js or main.css then you do the same thing you wait for the response.if you want to send through same TCP connection.so on.`

 - `so browser basically establish 6 TCP connection's to neglect delay. that's what browser will do today if the web server support http/1.1`

- `but the thing is http/1.1 is very inefficient and expensive(wasting resources) and that's where http/2 comes in.
`

## __HTTP/2__

![alt text](image.png)

- there is single a TCP  connection get established.there many request flow's through the single tcp connection.

- `but the thing is that how the server will be able to identify which request is for what or that  response is for which request ?. that's where we need stream id tag. it's numeric identifier assigned to each stream in http/2(check img 📸 above.). so the server instead of processing a single request for that socket start processing multiple request(may be multiplexing). and send the same in stream form with stream ids'`.

- `so here in http/2. we can compress the data & header's also (not in http/1.1).`


- `server push is a feature where server send's the resource's to the client before the client explicitly ask for them. ex-`
  - Client sends a normal request, e.g., for `/index.html`.

  -` Server responds with the main HTML content AND pushes additional resources, like /style.css and /script.js`, over the same HTTP/2 connection without waiting for the client to request them.

  - `The client receives all resources at once and can render the page faster.`

  -  Application layer protocol negotiation.(ALPN)
    so during tls handshake the server client negotiate for the appropriate protocol to use(HTTP/1.1,HTTP/2...).
    - client hello start tls hanshake there ALPN extension list the protocol client support's as server support's many protocol so it can choose the apropriate one from the client list.for that particular channel.

    ## __HTTP/1.0 vs HTTP/1.1__
 - in `http/1.0` every time a web page reloaded `it needed to create a new tcp connection for each resource(css,js,img),`
  it was slow opening and closing connection take time (`tcp handshake + tls handshake(if https)`).

  - `http/1.1` resolves this issue by using the exsiting tcp connection for fetching other resources.

  - http/1.0 nomrmally sends request and wait for response then send another request in sequence.

  - http/1.1 introduces pipelining so multiple request can be send before receiving the response.

  - ⚠️ Pipelining wasn't widely adapted because of issue's (head-of-line blocking).

   ## __Pipelining__
   - the biggest issue  head-of-line blocking. if the first response take's long time all the following responses are blocked until first one sent.

   - it could degrade much more performance than making single request. more it's hard to implement, cause bugs.

   -  if a single request in pipline failed it is tricky to handle or retry indidvidual request.

  ## __Chunked encoding:-__
  - in traditional http browser respond's to client usually send content-length headeer.
  - problem server must know the full size of response body in advance.
    - it is problem when content is generated dynamically generated.
    - the content is too large to buffer (video streaming)(the server cant store it in RAM to calc the complete size).
    - the server does'nt know the full content length.(unknown len of logs(ex-real time content getting wrote on the serverf),real time API's etc)
    
    __chunked transfer encoding__:-
    - allow's server to serve response in chunks.
    - The client doesn’t need to know the total size.
    - Transfer-encoding: chunked.
    - each chunk preceded by size header in bytes.

```
  4\r\n
  Wiki\r\n
  5\r\n
  pedia\r\n
```

```
  Line	Meaning
7\r\n	Next chunk is 7 bytes (hex) long → "Hello, "
Hello, \r\n	The chunk content
6\r\n	Next chunk is 6 bytes → "world!"
world!\r\n	The chunk content
0\r\n	Zero-length chunk → End of response
```

## __cache-control__ :-
- in http/1.1 caching is more sophisticated has`cache-control headers`.
ex - cache-control , ETag, last-modfied.
- it helps the browser to decide to use cached copy or ask the server for fresh version,reducing network traffic.

- `Note: more in HTTP caching`.


## __Host header__:-
- the ability to host different domain's from the same ip (server).
- host request header specifies the host and port number. of the server to which request is sent.
- if no port included the default port is (443 - https,80 - http).
- now as server can host many website's for ex - virtual hosting.
- host header field must be send in all HTTP/1.1 request messages.


## HOP(head-of-line)
- ⚠️ even `http/2 `improved lot by multiplexing as all data sent from underlying TCP layer.` AT TCP layer HOL can still occur If one TCP packet is lost during transmission, TCP’s reliability mechanism (guaranteeing in-order delivery) forces the entire connection to wait until the lost packet is retransmitted and received.`


## __HTTP & SSL__:-
- instead of sending HTTP over basic TCP/IP stack an additional encrypted transmission layer was created by netscape. which was SSL it's early versions were not public. but later version SSL 2.0 SSL 3.0 were available to used by ecommerce website.

- as encrypted and gurantee of authenticity of the message's. SSL was late became TLS and it was standarizes.

- as web no longer used in just academic network . it became a jungle of advertiser , random people or criminal' for private data. as later application needed require accesss to private data email,location etc. TLS became necessary.


## __HTTP for complex applications__:-
- __check out mdn__:- https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Evolution_of_HTTP#using_http_for_complex_applications

- webDAV - authoring,editing,collaborating through http on server's.

## __REST (representational state transfer)__
- `restfull api` - so what does a restfull api do ? 
    ok as we know communcation happens b/w server and client which is basic req and response and for doing that what are the best practices ,rules, standards that restfull api gives. 

  - works on client-server artitechture.
  - scenarios - SSR - server side rendering. n SSR, the client requests data (like blogs), and the server fetches from DB, renders an HTML page, and returns it. Browsers can render this, but non-browsers (mobile, Alexa) can’t use HTML effectively, making clients dependent on the server’s output.

 - In REST, the server returns raw data (JSON has key/value pairs /XML) instead of HTML. Any client (browser, mobile, Alexa) can consume it and render as needed, making clients independent of the server’s presentation.

 - if your are sure that your client is a browser than it's best to send for ex-html it reduces a step. like in (google.com). 

## Spoiler alert: `also you have to do mdn client server database`
 - alway's respect HTTP method's - like GET , PUT , POST, PATCH , DELETE etc.
 - ok so let's see for what we commonly use these.
    - GET /user = user data read kro and return kro.
    - POST /user = handel new user creation.
    - PATCH /user = update the user.

- but if we use them the wrong way, opposite way it will not gonna affect any thing much but we can't say it as correct then also it is wrong.
   - POST /update user ---> user update.
   - POST /create user ----> create.
   - POST /delete user -----> delete user.
      NOT A BEST PRACTICE .

    - CSR - we got JSON data first than it get rendered on client side. (Client side rendering).

### just for API check freecodecamp not for REST as it mostly wrong
 
## What is API ?
- Application programming interface . it establish connection b/w program's so that they can transfer data.

### just for API check freecodecamp not for REST as it mostly wrong.

## REST ?
- it is an artitechtural style that make's communication easier bw client and server. REST API's use existing HTTP request method's to work with resources present on the server. and CRUD operation's are also done like CRUD create read update Delete.


firstly let's learn a lil bit about how fetch is getting used in JS. 
- fetch is getting used to fetch a resource from the server as we are talking about REST through an endpoint which is basically a URL we'll be seeing that later.

```javascript
 fetch('https://jsonplaceholder.typicode.com/todos/5')
 .then(res => res.json())
 .then(data => {
  console.log(data.title)
 })
 ```
 
 - here in the code we are using for a to get resource using an endpoint. and then the res we get wew take it as it would be in JSON or(in old days in XML).convert it to simple data .then use the data the way you want.

 - NOW there could be two cases - 1.`if broken internet --> fetch goes directly to .catch`. 
   2. `404 response or else --> fetch is "okay" with this you just got a res with res.ok = false.`

  ```javascript
    fetch('https://jsonplaceholder.typicode.com/todos/53r')
 .then(res => {
  if (!res.ok){
    console.log("problem")
    // return;
  }

   return res.json()
 })
 .then(data => {
  console.log(data.title)
 })
 .catch(error => {
  console.log("this is error",error);
 })
 ```

- as here what we did we passed undefined or not present endpoint param . so it would have return with `404 error in html not in JSON`. so as we are trying parse it as json to data in `res.json()`. which is not even present because above even we tried to handel the issue but there we not return or exit from this before parsing so hence error is not what is expected it's shows network issue.

```
 NetworkError when attempting to fetch resource.
```
