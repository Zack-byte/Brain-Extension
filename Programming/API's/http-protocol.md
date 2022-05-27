# HTTP
- Hyper Text Transfer Protocol

- It is a Application Layer protocol

- For fetching resources such as HTML documents. 

- Is a client server protocol. 

- Clients and server communicate by exchanging individual messages (as opposed to a stream). The messages sent by the client are called requests and the messages sent by the server are called responses.

- Designed in the early 1990's

- Sent over **TCP** or a **TLS-encrypted TCP connection** could also theoretically be used through any reliable transport protocol. 

## Extensible
- With the introduction of HTTP headers. The protocol is easy to extend and experiment with.

- A new functionally can be introduced by a simple agreement between a client and a server about a new header's semantics

## Stateless but not Sessionless
- there is no link between two requests being successively carried out on the same connection. 

- HTTP cookies allow the use of stateful sessions. 

- using header extensibility. HTTP cookies are added to the workflow, allowing session creation on each HTTP request to share the same context, or the same state.

## Connections
- HTTP relies on **TCP** standard which is connection-based

- before a client and server can exchange an HTTP request/response pair, they must establish a TCP connection.

- This process requires serverl round-trips. 

- HTTP/1.0 opens a separate TCP connection for each HTTP request/response (this is very inefficient).

- HTTP/1.1 introduced **pipelining** and **persistent connections** the underlying TCP connection can be partially controlled using the **Connection** header.

- HTTP/2 went a step further by multiplexing messages over a single connection (keeps things more efficient.

## What can be controlled by HTTP

### Caching:
- Can instruct proxies and clients about what to cache and for how long.

### Relaxing
- relaxing the origin constraint To prevent snooping and other privacy, invasions, web browsers enforce strict seperation between Web sites. 

### Authentication:
- There are a wide variety of authentication methods. Basic ones include WWW-Authenticate and HTTP Cookies.

### Proxy and TUnneling
- Http requests can go through proxies to cross network barriers. 



## HTTP Messages
- in HTTP/1.1 and earlier, are human readable. In HTTP/2 these messages are embedded into a binary structure, **A Frame**, allowing optimizations like compression of headers and multiplexing. 

- There are two types of HTTP Messages
  - **Requests**
  - **Response**



### Requests
- Consists of:
  - An HTTP Method:
    - **GET**
    - **POST**
    - **OPTIONS**
    - **HEAD**
  - The path of the resource to fetch.
  - The version of the HTTP protocol
  - Optional Headers
  - A body for some methods like POST. 

### Responses
- The verion of HTTP
- A Status Code
- A Status Message
- HTTP headers
- Optionally a body containing the fetched resource


## API's based on HTTP
- Most commonly used API based on HTTP is the **XMLHttpRequest** API, which can be used to exchange data between a user agent and a server. 

- Modern **Fetch API** provides the same features with a more powerful and flexible feature set.

- Another API **Server-sent events** is a one-way service that allows a server to send events to the client, using HTTP as a transport mechanism. Using the **EventSource interface** 
