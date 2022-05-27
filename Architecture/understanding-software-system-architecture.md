# Understanding Software and System Architecutre
- **Architectural style** ultimately is defined by how the components are connected, data is exchanged, and how they all work together as a coherent system.  

## Software Architecture
- refers to the logical organization of a distributed system into software components. Instead of one big monolithic application
- distributed systems are broken down into multiple components. the way in which these components are broken down impacts everything from system performance to reliability to response latency.

## System architecture
- Refers to the placement of these software components on physical machines. Two closely related components can be co-located or placed on different machines. The location of components will also impact performance and reliability.

# Software Architecture
- There are many different architectural styles:
  - **layered architectures**
  - **object-based**
  - **service-oriented**
  - **RESTful**
  - **pub/sub**

- The style used ultimately depends on the application
- Additionally, as you start building more complex, interconnected systems,
- distributed systems grow in size.
- As a result processes such as communication must be simplified and streamlined

# Layered Architecture
- In a layered architecture, components are organized in layers.
- higher layers make down calls to lower layers
- lower levels can make upcalls to higher levels. They usually only respond to higher layer requests.
- Consider Google docs as an example
  - **Interface Layer** You request to see the latest doc from your drive
  - **Processing Layer** Processes your request and asks for the information from the data layer
  - **Data Layer** Stores persistent data (aka your file) and provides access to higher-level layers.

# Object-Oriented, Service-Oriented Architectures, Microservices, and Mesh Architectures
- These are all more loosely organized and represent an evolutionary sequence. 
- While they are grouped together, (OOP) Object Oriented isn't an architectural style but rather a programming methodology that makes service-oriented architectures(SOAs) and microservices possible.

## Object-Based Architectural Styles
- OOP is a methodology generally used in the context of monolithic apps (although it's also used in more modern architectures). 
- Within a monolith, logical components are grouped together as objects. While they are distinguishable components, objects are still highly interconnected and not easy to seperate. Object Oriented is a way to organize functionality and manage complexity within monoliths.
- Each object has its own encapsulated data set, referred to as the object's state. You may have heard of stateful and stateless applications that refer to whether or not they store data. 
- In this context state stands for data. An object's method is the operations performed on that data.

- Objects are connected through a procedure call mechanisms. During a procedure call, an object "Calls" on another object for specific requests
- So when you hear "Procedure call" think of a request.

## Service Oriented Architecture
- Objects form the foundation of encapsulating services into independent units leading to the development of SOAs. 
- Services are self-contained, independent objects that make use of other services. Communication happens over a network via "messages" sent to each interface

## Microservices
- are the next step in this evolutionary sequence. these Microservices are smaller than services in an SOA, less tightly coupled, and more lightweight. 
- The more significant difference from a business perspective, however, is their ability to decrease time to market.
- Unlike with SOAs, where developers need to design and map out all interactions and interfaces before deploying a service (a process that can take months),
- Microservices are more independent, allowing developers to push out updates without worrying about architectural details. Additionaly, developers can use any programming language they want.
- Selecting the best language for a particular program further increases speed and thus time to market.

## Mesh Architectures
- are formed by services or processes running on nodes that cannot be easily accounted for.
- They may connect and disconnect frequently, some may not even use the internet.
- These services establish temporary peer-to-peer connections and can stay anonymous throughout the process.
- E.gs are peer-to-peer technologies like TOR, torrents, p2p messengers, blockchain, etc.
- Mesh architectures bring two additional qualities:
  - **Interacting services/processes are more uniform**: there may be just a few or even one type of service participating in a mesh network. They are considered equal to each other---equally trustworthy or untrustworthy if we are speaking about security, for instance. This is quite different from traditional service-based architectures where there are usually dozens of non-uniform services.
  - **There is a higher emphasis on its distributed nature**

- Mesh technologies are able to remain efficient even in highly unstable environments where connectivity between components is easily broken. 
- In some cases event most components, are not directly connected. 
- Instead they communicate over multiple "hops" via other system elements. (messages "hop" or "jump" from one element to another until reaching its destination).

## Representational State Transfer (REST) or RESTFUL Architectures
- REST is an architectural style widely adopted for the Web (a Web-native architecture)
- A distributed system is viewed as a huge collection of resources, individually managed by components. 
- Resources, in the context of REST, are a unique form of services that follow these conventions:
  - They understand a limited set of commands, often restricted to put, get, delete, and post
  - THere is only one (URL-based) naming scheme
  - Resource interfaces follow the same conventions and semantics
  - Messages are fully self-described
  - **stateless execution** After executing an operation on a resource, the resource forgets everything about the call from the client, except for the resulting changes in the service state

- Why all these restrictions on commands and interface specs? Well, just think of the vastly diverse systems that must communicate over the internet.
- By standardizing interfaces and reducing commands, developing compatible systems is much easier.
- REST is basically a simplification to deal with the diversity in a huge distributed system like the internet.
- Despite these restrictive commands, developers have enough flexibility to express anything they need. 

## Publish Subscribe Architectures
- pub/sub is an even more loosely coupled architecture that allows processes to easily join or leave. 
- The Key difference here is how services communicate. 
- Instead of calling and getting a response. services send one-way, usually async messages, generally not to a specific receiver.
- They rely on a configurator, administrator, or developer to configure who'll receive what message
- In some cases, the receivers themselves can sign up to receive messages.


## Centralized Organizations: Client-Server Systems
- A server is a process implementing a specific service (e.g database service). The client is a process requesting that service from a server. 
- The client sends the request and waits for the reply (request-reply behavior). 
- Where these processes are physically distributed will lead to different multitiered architectural styles.
- 