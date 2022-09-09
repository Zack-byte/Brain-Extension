# Frontend Security 101
Total application security is only as good as the sum of its parts. And **YES** that also includes the sexiest part of any application...The Frontend :exclamation:. And nooo I'm not biased in the slightest :smirk:. All jokes aside the frontend is still definitely a place where a security first mindset should be taken place while developing your application. And yes this comes with exceptions, however for the case of these notes that's where we are headed.

## Start With the Pros
Just like chess application security has multiple millions (definitely way more) of possible scenarios, and out of those countless outcomes only a fraction have been discovered **And** accounted for. Leaving defenders and attackers in an endless battle over their applications. And also just like chess, you can either go in blind or "imitate before you innovate". Meaning, there are strategies that can be studied and accounted for on both the developer's side and the hackers side. Let's take a look at some of the big but still relevant vulnerabilities in the Frontend.

### **(XXS) Cross Site Scripting**
Cross Site scripting is where an attacker can input malicious or even non malicious code into your web application. It lies dormant until the site is served up to another user's browser, then it takes root and runs the added scripts.

E.G =
1. And attacker (User A) inputs malicious code into a form or form field. 
2. Submits the infected form which is processed by the application and saved in the DB.
3. User B then access the site, and requests to see the data in which the script hides.
4. The backend serves the data to the frontend.
5. User B's browser unknowingly executes the malicious code, under the impression that it is safe, since it came from the server.

**Prevention**
- **Filter input on arrival** - when the input is received, filter data based on what is expected as a valid input.
- **Encode data on output** - When user-controllable data is provided via HTTP responses, encode the output to prevent it from being executed by the HTML parser. Depending on the output context, this might require applying combinations of HTML, URL, Javascript, and CSS encoding.
- **Use Appropriate Response Headers** - To prevent XXS in HTTP responses that aren't intended to contain any HTML or Javascript, we can use the Content-Type and X-Content-Type-Options headers to ensure that browsers interpret responses the way they were intended. 

### Cross-Site Request Forgery (CSRF)
CSRF is an attack that tricks the victim into submitting a malicious request.

If a user is currently authenticated to a website, any HTTP requests made to that website will have any credentials associated with the site. Such As...
- Session Cookie
- IP Address
- etc

If the request is initiated by an attacker, when this request reaches the backend, the server will have no way to distinguish between a malicious request and a legitimate request.

These attacks target functionality that causes a state change on the server, such as changing the victim's email address or password or purchasing something.


### **How does this attack work?**
#### **Using a GET Request**
- An email can contain a URL which is disguised as an ordinary link, and when the victim clicks on it, the browser makes a GET call with all the credentials of John's user session on his net banking website.
```html
<a href="http://bank.com/transfer.do?acct=ATTACKER_ACCOUNT&amount=100000">You've been duped!!</a>
```
- Or the email can simply render a 0 X 0 image with a targeted URL which triggers a GET request automatically.
```html
<img src="http://bank.com/transfer.do?acct=ATTACKER_ACCOUNT&amount=1000" width="0" height="0" border="0">
```
#### **Using a POST Request**
- Even when a POST request is required for the attacker can get in, it's still possible like so...
```html
<form action="http://bank.com/transfer.do" method="POST">
    <input type="hidden" name="acct" value="ATTACKER_ACCOUNT"/>
    <input type="hidden" name="amount" value="100000" />
    <input type="submit" value="View my pictures">
</form>
```

**Prevention**
- For every user session, the server should generate a randomized token (**CSRF Token**) and send it to the client. The client can save the token, from where the javascript can read it.
- When a Web App is making an HTTP request, the application should include that randomized token (**CSRF Token**) in the header of each request.
- The value of this token should be randomly generated such that it cannot be guessed by an attacker. Use a well known hashing algorithm such as "SHA256/512" for generating solutions.
- When the request is made from the app, the server must verify the existence and validity of the token in the request compared to the token found in the user session. If the token was not found within the request, or the value provided does not match the value within the user session, then the request should be dropped, and the event can be logged as a potential **CSRF** attack in progress.

### DOS (Denial Of Service) Attack
A DOS attack is a cyber-attack in which a perpetrator seeks to make a server resource unavailable to the actual users by disrupting the services of a server connected to the internet.

This attack is carried out by overloading the system by a huge number of requests in a very short interval of time (every millisecond) and prevent legitimate requests to be served.

In a **distributed denial-of-service attack (DDOS)**, the incoming traffic flooding the victim originates from many different sources. This effectively makes it impossible to stop the attack simply by blocking a single source/IP address.

**Prevention**
- Using Captcha at public facing endpoints (login, registration, contact) a captcha is a computer program or system intended to distinguish humans from bots.

- Most of DOS attacks are carried out using bots.