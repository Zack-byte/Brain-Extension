# Microsoft NTLM

- **New Technology LAN Manager** (NTLM) is the authentication protocol used on networks that include systems running the Windows operating system and on stand-alone systems.

- **Kerberos** security package adds greater security than NTLM to systems on a network. 
- Although Kerberos is the protocol of choice, NTLM is still supported.
- NTLM must also be used for logon authentication on stand-alone systems. 

## What are they?
- NTLM credentials are based on data obtained during the interactive logon process and consist of a domain name, a user name, and a one-way hash of the user's password.
- Uses an encrypted challenge/response protocol to authenticate a user without sending the user's password over the wire.
- Instead the system requesting authentication must perform a calculation that proves it has access to the secured NTLM credentials. 

- Interactive NTLM authentication over a network typically involves two systems: 
  - **A Client System** where the user is requesting authentication
  - **A Domain Controller** where information related to the user's password is kept. 

- Non-interactive authentication, which may be required to permit an already logged-on user to access a resource such as a server application, typically involve three systems: 
  - **A Client**
  - **A Server**
  - **A Domain Controller** (Does the authentication calculations on behalf of the server)

- e.g of NTLM non-interactive authentication:
  - (Interactive Authentication Only) A User accesses a client computer and provides a domain name, user name, and password. The client computes a cryptographic hash of the password and discards the actual password.
  - The client sends the user name to the server (in plain text)
  - The server generates a 8-byte random number, called a challenge or nonce, and sends it to the client.
  - The client encrypts this challenge with the hash of the user's password and returns the result to the server. This is called the response
  - The Server sends the following three items to the domain controller:
    - User name
    - challenge sent to the client
    - response received from the client
  - The domain controller uses the user name to retrieve the hash of the user's password from the Security Account Manager database. It uses this password hash to encrypt the challenge.
  - The domain controller compares the encrypted challenge it computed (in step 6) to the response computed by the client (in step 4). If they are identical authentication is successful.

- Your application should not access the NTLM security package directly. instead it should use the Negotiate security package. 
- This allows your application to take advantage of more advanced security protocols if they are supported by the systems involved in the authentication. Currently, the negotiate security package selects between Kerberos and NTLM. Negotiate selects 

## Security Considerations for Implementers
- NTLM does not support any recent cryptographic methods, such as AES or SHA256