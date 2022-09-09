# IIS Architecture Basics
Internet Information Services (IIS) 7 and later provide a request-processing architecture which includes:
- The Window Processing Activation Service (WAS), which enables sites to use protocols other than HTTP HTTPS.
- A Web server engine that can be customized by adding or removing modules.
- Integrated request-processing pipelines from IIS and ASP.NET

## Components
IIS contains several components that perform important functions for the application and Web server roles.
Each Component has responsibilities
Such as...
- Listening for requests made to the server.
- Managing processes.
- Reading configuration files.

## Protocol Listeners
Protocol listeners receive protocol-specific requests, send them to IIS for processing, and then return responses to requesters.

E.G = When a client browser requests a Web page from the Internet, the HTTP listeners, HTTP.sys, picks up the request and sends it to IIS for processing. Once IIS processes the request, HTTP.sys returns a response to the client browser.

### HTTP.sys
- This is comes by default as of IIS 6.0 and higher. HTTP.sys listens for both HTTP and HTTPS protocols. IIS 7.0 and later also includes support for (SSL) Secure Sockets Layer.


### WCF
- To support other services and applications that use protocols other than HTTP and HTTPS, you can use technologies such as **Windows Communication Foundation** which has listeners and adapters that provide functionality of both a protocol listener and a listener adapter. 

## Hyper Text Transfer Protocol Stack
The HTTP listener is part of the networking subsystem of Windows OS's. And is implemented as a Kernel-mode device driver called the HTTP stack (HTTP.sys). 
- HTTP.sys listeners to the network for HTTP requests, passes the requests onto IIS for processing, and then returns the processed response back to the client browsers.

Benefits it provides: 
- Kernel-mode caching = Requests for cached responses are served without switching to user mode.
- Kernel-mode request queueing. Requests cause less overhead in context switching because the kernel forwards requests directly to the correct worker process. If no worker process is available to accept a request, the queue holds the request until a worker is able to pick it up and process it. 
- Request pre-processing and security filtering.

## Web Publishing Service
IIS 7 or later splits the responsibility of the WWW Publishing Service between the **WWW Service** and the new service **Windows Processing Activation Service (WAS)**. These two services run as LocalSystem in the same Svchost.exe process and share the same binaries.


### WWW Service
Handles:
- HTTP administration and Configuration
- Process management 
- Performance monitoring

### Windows Processing Application Service (WAS)
- Manages application pool configuration and worker processes instead of the WWW Service. This enables you to use the same configuration and processes model for both HTTP and non-HTTP sites.

### Configuration Management in WAS
On startup, WAS reads certain information from the **ApplicationHost.config** file, and passes the information on to listener adapters on the server.

**Listener Adapters**: are components that establish a connection between the **WAS** and **Protocol Listeners** (such as HTTP.sys). 

- Once listener adapters receive configuration information, they configure their related protocol listeners and prepare them to listen for requests.

## Modules in IIS
In newer versions of IIS, the majority of the functionality is not within the server itself but with the **Web server engine**. The Web Server Engine allows you to add or remove components based on your application needs. (These component are called **Modules**).

## Native Modules in IIS
| Module Name | Description | Resource |
| ----------- | ------------- | ------- |
| CustomErrorModule | Sends default and configured HTTP error messages when an error status code is set on a response. | Inetsrv\Custerr.dll
| HttpRedirectionModule | Supports configurable redirection for HTTP requests.| Inetsrv\Redirect.dll | ProtocolSupportModule | Performs protocol-related actions, such as setting response headers and redirecting headers based on configuration. | Inetsrv\Protsup.dll |