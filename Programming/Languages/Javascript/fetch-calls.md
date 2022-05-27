# Fetch API

- Provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. 

- Provides a global fetch() method that provides an easy, logical way to fetch resources async across the network.

- This was previously achieved using **XMLHttpRequest**. 

- Fetch is a better alternative that can easily be used by **Service Workers**.

- Provides a single logical place to define other HTTP-related concepts such as CORS and extensions to HTTP.


## Different from JQuery().Ajax()
- The Promise returned from fetch() **won't reject on HTTP error status**. The promise will resolve with the ok property of  the response set to false. And it will only reject on network failure.

- Unless fetch() is called with the credentials option set to include fetch() won't send cookies in cross-origin requests
- won't set any cookies sent back in cross-origin responses.

```javascript
fetch('http://example.com/movies.json')
.then(response => response.json())
.then(data => console.log(data))
```

- The response object from a fetch call returns the entire HTTP response

- To get the body content returns use **.json()**


## Supplying request options

- fetch() has an optional second parm that allows you to control a number of different settings.

- **mode: "no-cors"** retricts headers to:
  - **Accept**
  - **Accept-Language**
  - **Content-Language**
  - **Content-Type**

- To include credentials on both same-origin and cross-origin. add **credentials: 'include'**


