# Microsoft Sql Server Security
Securing Sql server, like many things, can be looked at like an Onion.
![Layers Image](./assets/layers.gif)

Four to be exact. Those areas include **the Platform**, **authentication**, **objects (including data)** , and **Applications that access the system**.

## Platform and Network Security
The "Platform" includes the physical hardware and networking systems connecting clients to the database servers, and the binary files that are used to process database requests.

### Physical Security
- Best practices for physical security can include a variety of things. However to make a long story short, "Lock that shit up". Make sure that whoever is accessing the physical hardware (where ever it is located) is authorized to access it.

### Operating System Security
- Make sure to consistently update your OS system service packs and upgrades which will include security enhancements. 
- **Firewalls** also provide effective defenses against attackers. Firewalls block or restrict network traffic, make sure that your firewalls are configured to adhere to your organizations security policy. 