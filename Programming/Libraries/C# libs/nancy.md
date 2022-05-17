# Nancy

- Nancy is a lightweight, low-ceremony, framework for building HTTP based services on .NET and Mono. 

- Nancy is designed to handle DELETE, GET, HEAD, OPTIONS, POST, PUT and PATCH requests and provides a simple, elegant, DSL(domain specific language)

- Core concept is hosts: 
	- a host acts as an adaptor for a hosting environment and Nancy, enabling Nancy to run on existing technologies such as ASP.NET, WCF and OWIN, 

- the method is the HTTP method that is used to access the resource. 
	- HEAD requests are automatically handled for all routes that are declared for GET requests

- A route also needs a pattern which declares the application-relative URL that the route answers to. 
	- literal segments
	- capture segments
	- capture segments(optional) 
	- capture segments(optional/default) 
	- RegEx Segment 
	- Greedy Segment
	- Greedy RegEx Segment 
	- Multiple Captures Segment 

- a route action is the behavior which is invoked when a request is matched to a route. it is represented by a lambda expression of type Func<dynamic, dynamic. where the dynamic input is a dynamicDictionary, 

- HTTp specification specifies how clients request data will be constructed and sent to the server, and how the servers respond to these requests. 

- HTTP is connections less
- HTTP is media independent
- HTTP is stateless 

- The HTTP protocol is a request/response protocol based on the client/server based architecture where web browsers, robots and search engines, etc. act like HTTP clients, and the web server acts as a server. 

- the HTTP client sends a request to the server in the form of a request method, URI, and protocol version, followed by a MIME-like message containing request modifiers, client information, and possible body content over a TCP/IP connection.

- Server
	- the http server responds with a status line, including the message's protocol version and a success or error code followed by a MIME-like message containing server information, entity meta information, and possible entity-body content 

- An IIS web server runs on the Microsoft.NET platform on the windows OS. 
- A web server hosts web applications
- allows an application to process messages that arrive through specific TCP ports
- web servers can either process all requests on one thread or spawn a new thread for each request 
- IIS can be managed via the CLI or using Powershell



- IDX (internet Data Exchange) 
- MLS (multiple listing service 
- If you set up HTTPS you need to set host name and port numbers 


Hosting Nancy: 
	- IIS/aspnet: Nancy is handled through a HTTP Handler, which is setup through the Web.Config. Example should be in 
	- By default IIS 6 does not support PUT and DELETE verbs. To enable is, you need to add a wildcard mapping to the virtual directory of your Nancy application
	- Prevent IIS from taking over errors place in system.web
	<httpError existingResponse="PassThrough"/>


<system.web> is the settings section for IIS6 and the built in Visual Studio test server

Configuration coded in <system.webserver> Tag are implemented on IIS and are only applied to Project or Web application to which corresponding web.config belongs  

web.config file contains the configuration that needs to be implemented on IIS for Current project. 

- System.Webserver is used to configure IIS 7.0 and later which includes an ASP.NET pipeline and some configuration differences
	- is the s