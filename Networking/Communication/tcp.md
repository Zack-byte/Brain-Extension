# TCP IP
- The **Internet Protocol** is the address system of the Internet and has the core function of delivering packets of information from a source device to a target device. 
- IP is the primary way in which network connections are made, and it establishes the basis of the Internet.
- IP does not handle packet ordering or error checking. 
- Such functionality requires another protocol,
- Typically TCP.

- The TCP/IP relationship is similar to sending someone a message written on a puzzle through the mail. 
- The message is written down and puzzle is broken into pieces. Each Piece then can travel through a different postal route.
- some of which take longer than others. 
- When the puzzle pieces arrive after traversing their different paths, the pieces may be out of order.
- The IP makes sure the pieces arrive at their destination address. The TCP protocol can be thought of as the puzzle assembler on the other side who puts the pieces together in the right order, asks for missing pieces to be resent, and lets the sender know the puzzle has been received.
- TCP maintains the connections with the sender from before the first puzzle piece is sent to after the final piece is sent.

- IP is a connectionless protocol, which means the each unit of data is individually addressed and routed from the source device to the target device, and the target does not send an acknowledgement back to the source. That's where protocols such as TCP come in
- TCP is used in conjunction with IP in order to maintain a connection between the sender and the target and to ensure packet order.

- For example, when an email is sent over TCP, a connection is established and a 3-way handshake is made.:
  - An **SYN** "initial request" packet is sent from the source to the target server in order to start the dialogue.
  - Then a **SYN-ACK** "request acknowledgment" is sent back to the source server from the target server
  - Lastly the source sends an **ACK** packet to the target to confirm the process, after which the message contents can be sent.

- The email message is ultimately broken down into packets before each packet is sent out into the Internet, where it traverses a series of gateways before arriving at the target device where the group of packets are reassembled by TCP into the original contents of the email.
