# UDP
- The User Datagram Protocol, or UDP is a communication protocol used across the Internet for especially time-sensitive transmissions such as video playback or DNS lookups.
- It speeds up communications by not formally establishing a connection before data is transferred. 
- This allows data to be transferred very quickly, but it can also cause packets to become lost in transit -- and create opportunities for exploitation in the form of DDoS attacks

## How Does UDP work
- UDP is a standardized method for transferring data between two computers in a network. Compared to other protocols, UDP accomplishes this process in a simple fashion: it sends packets (units of data transmission) directly to a target computer, without establishing a connection first 
- indicating the order of said packets, or checking whether they arrived as intended (UDP packets are referred to as 'datagrams').
- UDP is faster but less reliable than TCP, another common transport protocol. In a TCP communication, the two computers begin by establishing a connection via an automated process called a 'handshake'. Once this handshake has been completed will one computer actually transfer data packets to the other.
- UDP communications instead can simply start sending data to the other.
- In addition, TCP communications indicate the order in which data packets should be received and confirm that packets arrive as intended. 
- If a packet does not arrive -- e.g due to congestion in intermediary networks --- TCP requires that it be re-sent UDP communications do not include any of this functionality
- If a UDP datagram is lost in transit, it will not be re-sent. As a result, applications that use UDP must be able to tolerate errors, loss, and duplications.
- (Technically, such packet loss is less a flaw in UDP than a consequence of how the INternet is built. Most network routers do not perform packet ordering and arrival confirmation by design, because doing so would require an unfeasible amount of additional memory. TCP is a way of filling this gap when an application requires it).

## What kind of services Rely on UDP
- UDP is commonly used in time-sensitive communications where occasionally dropping packets is better than waiting. 
- Voice and Video traffic are sent using this protocol because they are both time-sensitive and designed to handle some level of loss.
- For example VOIP (voice over IP) which is used by many internet-based telephone services, operates over UDP. This is because a staticy phone conversation is preferable to one that is crystal clear but heavily delayed.


## UDP and DDoS
- UDP 'risks' like packet loss are not a serious problem in most use cases. However, UDP can be exploited for malicious purposes.
- Since UDP does not require a handshake, attackers can 'flood' a targeted server with UDP traffic without first getting that server's permission to begin communication.
- A typical UDP flood attach sends a large number of UDP datagrams to random ports on its target computer. 
- This forces the target to respond with an equally large number of ICMP packets, which indicate those ports were unreachable. The computing resources required to responed to each fraudulent datagram can exhaust the target, resulting in a denial-of-service to legitimate traffic. Organizations can defend against UDP flood attacks with a variety of methods. 
- One is to limit the response rate of ICMP packets, though this approach can also filter out legitimate packets.
- Another method is to receive and respond to UDP traffic through an intermediary intermediary network of many distributed data centers, preventing a single origin server from being overwhelmed with fraudulent requests