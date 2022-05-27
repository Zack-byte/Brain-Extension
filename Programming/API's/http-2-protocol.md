# HTTP 2.0

- version 2.0 of the Hyper Text Transfer Protocol will make applications faster, simpler, and more robust. By allowing devs to undo many of the HTTP/1.1 workarounds previously done withing applications.
- The primary goal of Http 2 is reducing latency. by enabling full request and response multiplexing, minimize protocol overhead via efficient compression of HTTP header fields, and add support for request prioritization and server push.
- Other version two enhancements include:
  - new flow control
  - error handling
  - upgrade mechanisms
  - etc...

- Does not modify the application semantics of HTTP. All the core concepts such as methods, status codes, URIs and header fields, remain.
- HTTP/2 modifies how the data is formatted (framed) and transported between the client and server, both of which manage the entire process, and hides the complexity from applications within the new framing layer. 

- Introduces a new binary framing layer that is not backward compatible with previous HTTP servers and clients. 


## HTTP/1 problems
- need to use multiple connections to achieve concurrency and reduce latency
- does not compress request and response headers, (causing unnecessary network traffic)
- Does not allow effective resource prioritization, (resulting in poor use of the underlying TCP connection)

## HTTP/2 Solutions
- Introduced header field compression and allowing multiple concurrent exchanges on the same connection
- allows interleaving of request and response messages on the same connection. 
- Uses efficient coding for HTTP header fields
- Allows for prioritization of requests, letting more important requests complete more quickly, further improving performance.


## Binary Framing Layer
- at the core of all the performance enhancements HTTP/2 is the new binary framing layer, which dictates how the HTTP messages are encapsulated and transferred between the client and server.
- The **"layer"** refers to a design choice to introduce a new optimized encoding mechanism between the socket interface and the higher HTTP API exposed to applications. 
- THis changes the way HTTP verbs, methods, and headers are encoded while in transit. 
- All HTTP/2 communication is split into smaller messages and frames, each of which is encoded in binary format. (HTTP/1 is newline delimited plaintext) 
  - As a result of the new Binary encoding both client and server must switch so that they can understand each others requests/responses.

## Streams Messages and Frames
- **Stream**: A bidirectional flow of bytes withing an established connection, which may carry one or more messages.
- **Message**: A complete sequence of frames that map to a logical request or response message.
- **Frame**: The smallest unit of communication in HTTP/2, each containing a frame header, which at a minimum identifies the stream to which the frame belongs.

- The relation of these terms can be summarized as follows:
  - All communication is performed over a single TCP connection that can carry any number of bidirectional streams.
  - Each stream has a unique identifier and optional priority information that is used to carry bidirectional messages
  - Each message is a logical HTTP message, such as a request, or response, which consists of one or more frames.
  - The frame is the smallest unit of communication that carries a specific type of data --e.g HTTP headers, message payload, and so on. Frames from different streams may be interleaved and then reassembled via the embedded stream identifier in the header of each frame.

## Request and Response Multiplexing
- HTTP/1 if the client wants to make multiple parallel request to improve performance, then multiple TCP connections must be used.
- This is a direct consequence of the HTTP/1.x delivery model, which ensures that only one response can be delivered at a time (response queuing). per connection. This also results in head-of-line blocking and inefficient use of the underlying TCP connection.

- The new binary framing layer in HTTP/2 removes these limitations, and enables full request and response multiplexing, by allowing the client and server to break down an HTTP message into independent frames, interleave them and then reassemble them on the other end.

- The ability to break down an HTTP message into independent frames, interleave them, and tne reassemble them on the other end is the single most important enhancement of HTTP/2. 

## Stream Prioritization
- Once an HTTP message can be split into many individual frames, and we allow for frames from multiple stream to be multiplexed, the order in which the frames are interleaved and delivered both by the client and server becomes a critical performance consideration. 
- To facilitate this, the HTTP/2 standard allows each stream to have an associated weight and dependency.
  - Each stream may be assigned an integer weight between 1 and 256.
  - Each stream may be given an explicit dependency on another stream.

- The combination of stream dependencies and weights allows the client to construct and communicate a "Prioritization tree" that expresses how it would prefer to receive responses. In turn, the server can use this information to prioritize stream processing by controlling the allocation of CPU, memory, and other resources, and once the response data is available, allocation of bandwidth to ensure optimal delivery of high-priority responses to the client.

- A stream dependency within HTTP/2 is declared by referencing the unique identifier of another stream as its parent; if the identifier is omitted the stream is said to be dependent on the "root stream". Declaring a stream dependency indicates that, if possible, the parent stream should be allocated resources ahead of its dependencies. 

## One connection per origin
- With the new binary framing mechanism in place, HTTP/2 no longer needs multiple TCP connections to multiplex streams in parallel; each stream is split into many frames, which can be interleaved and prioritized. As a result, all HTTP/2 connections are persistent, and only one connection per origin is required, which offers numerous performance benefits.

- Most HTTP transfers are short and bursty, whereas TCP is optimized for long-lived, bulk data transfers.

## Flow Control
- is a mechanism to prevent the sender from overwhelming the receiver with data it may not want or be able to process: the receiver may be busy, under heavy load, or may only be willing to allocate a fixed amount of resources for a particular stream. 
- E.G The client may have requested a large video stream with high priority, but the user has paused the video and the client now wants to pause or throttle its delivery from the server to avoid fetching and buffering unnecessary data. 
- Alternatively, a proxy server may have fast downstream and slow upstream connections and similarly wants to regulate how quickly the downstream delivers data to match the speed of upstream to control its resource usage; and so on.
- TCP flow control is both not granular enough and does not provide the necessary application-level APIs to regulate the delivery of individual streams. To address this, HTTP/2 provides a set of simple building blocks that allow the client and server to implement their own stream- and connection-level flow control:
  - Flow control is directional. Each receiver may choose to set any windows size that it desires for each stream and the entire connection.
  - Flow control is credit-based. each receiver advertises its initial connection and stream flow control window (in bytes), which is reduced whenever the sender emits a DATA frame and incremented via a WINOW_UPDATE frame sent by the receiver.
  - Flow control cannot be disabled. when the HTTP/2 connection is established the client and server exchange SETTINGS frames, which set th eflow control window sizes in both directions. the default value of the flow control window is set to 65, 535 bytes, but the reciever can set a large max window size and maintain it by sending a WINDOW_UPDATE frame whenever any data is received.
  - Flow control is hop-by-hop, not end-to-end. That is, an intermediary can use it to control resource use and implement resource allocation mechanisms based on own criteria and heuristics.


## Server Push
- Another new feature is the ability of the server to send multiple responses for a single client request. That is, in addition to the response to the original request, the server can push additional resources to the client without the client having to request each one explicitly.

## Header Compression
- Each HTTP transfer carries a set of headers that describe the transfered resource and its properties. In HTTP/1.x, this metadata is always sent as plain text and adds anywhere from 500-800 bytes of overhead per transfer, and sometimes kilobytes more if HTTP cookies are being used.
- To reduce this overhead ans improve performance, HTTP/2 compresses request adn response header metadata using  **HPACK** 
- compression format that uses two simple but powerful techniquest:
  - It allows the transmitted header fields to be encoded via a static Huffman code, which reduces their individual transfer size.
  - It requires that both the client and server maintain and update an indexed list of previously seen header fields ( in other words, it establishes a shared compression context), which is then used as a reference to efficiently encode previously transmitted values.
- These compression techniques reduces 85% to 88% of excess weight of the transferred header data, 
