# RestSharp
- The main purpose of RestSharp is to make synchronous and async calls to remote resources over HTTP. 
- Of course making the main audience of RestSharp devs who use REST API's. 
- However RestSharp can call any API over HTTP, as long as you have the resource URI and request parameters that you want to send comply with W3C HTTP standards.
- One of the main challenges of HTTP API's for .NET devs is to work with requests and responses of different kinds and translate them to complex c# types.
- RestSharp can take care of serializing the request body to JSON or XML and deserialize the response. 
- It can also form a valid request URI based on different parms kinds 
  - Path
  - Query
  - Body




## Authenticators
- RestSharp includes authenticators for basic HTTP (Authorization header), NTLM and parameter-based systems.

### Basic Authentication
- The **HttpBasicAuthenticator** allows you to pass a username and password as a basic **Authorization** header using a base64 encoded string.

### OAuth1
- For OAuth1 authentication the **OAuth1Authenticator** class provides static methods to help generate an OAuth authenticator.


### OAuth2
- RestSharp has two very simple authenticators to send the access token as part of the request.
- **OAuth2UriQueryParameterAuthenticator** accepts the access token as the only constructor argument, and it will send the provided token as a query parm **oauth_token**
- **OAuth2AuthorizationRequestHeaderAuthenticator** has two constructors. One only accepts a single argument, which is the access token. The other constructor also allows you to specify the token type. The authenticator will then add an **Authorization** header using the specified token type or **OAuth** as the default token type.

### JWT
- JWT authentication can be supported by using **JwtAuthenticator** 
- For each request it will add an **Authorization** header with the value **Bearer (your token)** 


### Custom Authentication
- You can write your own implementation by implementing. **IAuthenticator** and registering it with your RestClient.