# HTTP/2.0

#### HTTP history
In the beginning, there was gopher. Lines started with `\Reference` and response had a char at the
beginning of each line indicating the type.

Then, HTTP/0.9: with text content and HTML!

Then HTTP/1.0: with headers! Keep-Alive can keep connections alive.

Then HTTP/1.1: Keep-Alive is implicit, Host header is required.

#### HTTP/2.0
Problem with 1.1 is it's pretty slow! Syn, ack, synack, etc over TCP. No way for server to shut down
if the connection is alive (this is undefined in HTTP/1.1). Server FIN and client request can cross
in flight! Also sometimes you have to deal with \r\n instead of \n, etc.

HTTP/1/1 pipelining: you can try to send a lot of requests without waiting for responses, BUT this
doesn't work in practice because proxy servers (requests can get routed to different servers too,
etc).

Only like 6 connections at once are usually allowed from the same client. Sprite sheets are basically
because you can't request all the sprites seperately.

##### SPDY
Google did this, became start of HTTP/2.0.

##### How 2.0 works
Binary frame!

Frame length (12 bytes), frame type (two bytes, 1 = HEADERS), frame flags (two bytes), data.

[https://http2.golang.org](Go HTTP2 server)

With http2, you can ask for all resources at once, so latency is not as much.

#### 2.0 Headers
1. SETTINGS: negotiate peer limits, max frame size (16k-16M), max concurrent requests
2. PING: still there?
3. HEADERS/CONTINUATION: clients start a new stream, servers use response headers. Each strem has a unique id, clients always use odd numbers. :method="GET" for backwards compatibility.
4. DATA: the actual data
5. GOAWAY: server: "im shutting down and the last stream I saw was 17". browser: "oh, then the CC details didnt go through"
6. WINDOW_UPDATE:_: flow control. "I am willing to get 600 bytes of kittens.jpg, and the rest later."
7. PRIORITY: Changed my mind, i want kittens.jpg right now.
8. PUSH_PROMISE_: can give the structure of what a response for a given path would get.

HPACK: new compression format. Encodes header:value pairs. Algo uses a table with common keys. Also a dynamic table which is adjusted with the requests that you make. Uses huffman encoding to make common strings small.

Header compression: subsequent requests only need to be a diff!! WOAH.

#### Upgrading
For HTTPS sites, it's easy because SSL has stuff to agree on the language to speak. HTTP pretty much will never work unless the browser implemented some random part of the spec.

HTTP2 always runs on tcp:443.

#### Next steps after HTTP/2.0
Packet loss is a real problem, byte alignment is important.

QUIC is HTTP2/TLS/TCP (with TCPFO) built into one protocol. Works over UDP, because internet only knows how to speak TCP and UDP.
