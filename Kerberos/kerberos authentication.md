# Kerberos
- Kerberos lets you connect to an application over an insecure network

- Protocol designed to provide secure authentication to services over an insecure network

- Passwords are never sent across the network

- Encryption keys are never exchanged directly

- Application and client mutually authenthicate each other

- Kerberos is a protocoll implementing all the points mentioned above

## Kerberos realm
- Kerberos realm is the domain
- domain is the group of systems over which Kerberos has the authority to authenticate a user to a service
- There can be mulitple realms and you can interconnect them.
- Within a realm there are principals
- Principal is a uniqe identity of an user or service(application)

- Client / User is a process wich accesses a service  

- Service is a resource (application, file server) provided to a client 

## KDC
- The Key Distribution Center provides tickets and generates temporary session keys which allow an user to securely authenticate to a service
- KDC stores all the secrety symmetric keys for users and services
- Within KDC ther are two servers, namely the authentication server and the ticket granting server

- The authentication server confirms that a known user is making an access request  and issues ticket granting ticket

- The ticket granting server confirms that a user is making an access request to a known service and issues service tickets

## kerberos realm
![](kerberos%20realm.png)

- Tons of messages are sent back and forth between users and authentication server

There are two types of messages: 
- Authenticators
- Tickets

Authenticators are a record containing information that can be shown to have been recently generated using the session key known only to the client and the server.

Authenticators allow the user to authenticate to the service and the service to the user (mutual authentication).

Tickets contain most of the information that needs to be passed containing the clients identity, service ID, session keys, time stamps, time to live etc.

All this is encrypted using a servers secret key

![](kerberos%20authentication%20overview.png)








