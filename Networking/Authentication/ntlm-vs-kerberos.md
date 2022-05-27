# NTLM vs. Kerberos
- Like NTLM, Kerberos is an authentication protocol. 
- It replaced NTLM as the default/standard authentication tool on Windows 2000 and later releases.
- The main difference between NTLM and Kerberos is in how the two protocols manage authentication. 
- NTLM relies on a three-way handshake between the client and server to authenticate a user. 
- Kerberos uses a two-part process that leverages a ticket granting service or key distribution center.
- Another main difference is whether passwords are hashed or encrypted. 
  - NTLM relies on password hashing, which is a one-way function that produces a string of text based on an input file.
  - Kerberos leverages encryption, which is a two-way function that scrambles and unlocks information using an encryption key and decryption key respectively.


- Even though the Kerberos protocol is Microsoft's default authentication method today, NTLM serves as a backup. 
- If Kerberos fails to authenticate the user, the system will attempt to use NTLM instead.



## Why was NTLM Replaced by Kerberos?
- NTLM was subject to several known security vulnerabilities related to password hashing and salting.

- In NTLM, passwords stored on the server and domain controller are not "salted" meaning that a random string of characters is not added to the hashed password to further protect it from cracking techniques.
- This means that adversaries who possess a password hash do not need the underlying password to authenticate a session. 
- As a result, systems were vulnerable to brute force attacks, which is when an attacker attempts to crack a password through multiple log-in attempts.
- If the user selects a weak or common password, they are especially susceptible to such tactics.
- NTLM's cryptography also fails to take advantage of new advances in algorithms and encryption that significantly enchance security capabilities.

