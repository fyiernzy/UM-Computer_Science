# Application Layer

## Peer-to-Peer Network

1. Client/server model involves a client device requesting information from a server device
2. Both client and server processes are in the application layer
3. P2P network involves multiple devices connected via a network and can share resources without a dedicated server
4. Each connected device (peer) in a P2P network can function as both a server and a client
5. Some P2P networks use a hybrid system where resource sharing is decentralized, but indexes are stored in a centralized directory
6. Examples of P2P networks include BitTorrent, Direct Connect, eDonkey, and Freenet
7. Gnutella protocol-based P2P applications involve sharing whole files with other users
8. Clients in BitTorrent use a torrent file to locate other users who have pieces of the file they need. This file also contains information about tracker computers that keep track of which users have specific pieces of certain files.
9. Clients in BitTorrent ask for pieces from multiple users simultaneously, known as a swarm.

## HTTP and HTTPS

Three common message types

- GET - This is a client request for data. A client (web browser) sends the GET message to the web server to request HTML pages.
- POST - This uploads data files to the web server, such as form data.
- PUT - This uploads resources or content to the web server, such as an image.

1. The browser interprets the URL's three parts: protocol/scheme, server name, and filename
2. The browser checks with a name server to convert the server name into an IP address using DNS (Domain Name System)
3. HTTP is a request/response protocol where clients send GET messages to request data from web servers
4. HTTP is not secure because data is transmitted in plaintext and can be intercepted and read
5. HTTPS is a secure protocol that uses authentication and encryption to protect data transmitted between clients and servers
6. HTTPS uses TLS (Transport Layer Security) or SSL (Secure Socket Layer) to encrypt data before transmission

## Email protocols

### Introduction

1. An ISP provides email hosting services, which requires several applications and services.
2. Email uses store-and-forward method and messages are stored in databases on mail servers.
3. Email clients communicate with mail servers to send and receive email.
4. An email client does not communicate directly with another email client when sending email. Instead, they rely on the mail server to transport messages.

### SMTP

1. SMTP is a protocol used for sending email messages. 
2. When a client sends an email, it connects with a server on port 25 and attempts to send the message to the server. 
3. The server either stores the message in a local account or forwards it to another server for delivery.
4. The message header must contain the sender and recipient email addresses.
5. If the destination server is unavailable, the message is spooled and sent later.
6. Periodically, the server checks the queue for messages and attempts to send them again. If the message is still not delivered after a predetermined expiration time, it is returned to the sender as undeliverable.

### POP (Post Office Protocol)

- POP is a protocol to retrieve email messages from a mail server.
- With POP, email messages are downloaded from the server to the client and deleted from the server.
- There is no centralized location for email messages with POP.
- POP is not recommended for small businesses needing a centralized backup solution.

#### How POP work

1. POP service starts by listening on TCP port 110 for client connection requests.
2. A client initiates the connection by sending a request to the server to establish a TCP connection.
3. Once the connection is established, the POP server sends a greeting to the client.
4. The client and server then exchange commands and responses until the connection is closed or aborted.

### IMAP (Internet Message Access Protocol)

1. IMAP is a protocol used to retrieve email messages
2. Unlike POP, IMAP downloads copies of messages to the client application while keeping the original messages on the server
3. Users can view copies of messages in their email client software
4. Users can create a file hierarchy on the server to organize and store mail, which is duplicated on the email client
5. When a user deletes a message, the server synchronizes that action and deletes the message from the server.

## DNS (Domain Name System)

- Devices in data networks are identified with numeric IP addresses
- Domain names were created to convert IP addresses into simple, recognizable names
- Fully-qualified domain names (FQDNs) are easier for people to remember than numeric addresses
- Changing the numeric address of a server is transparent to the user if the domain name remains the same. The new address is simply linked to the existing domain name and connectivity is maintained.
- Domain names allow for easier network configuration and maintenance.

### DNS Message Format

- DNS server stores different types of resource records that contain name, address, and type of record
Resource record types include:
  - A (IPv4 address)
  - NS (authoritative name server)
  - AAAA (IPv6 address)
  - MX (mail exchange record)
- When a client makes a query, the server first looks at its own records to resolve the name
- If unable to resolve, the server contacts other servers
- Once a match is found and returned, the server temporarily stores the numbered address for future requests.

### DNS Hierarchy

- DNS protocol uses a hierarchical system to create a database for name resolution.
- DNS uses domain names to form the hierarchy.
- Naming structure is broken down into small, manageable zones.
- Each DNS server maintains a specific database file and is responsible for managing name-to-IP mappings for that portion of the entire DNS structure.
- DNS server forwards the request to another DNS server within the proper zone for translation when it receives a request for a name translation that is not within its DNS zone.
- DNS is scalable because hostname resolution is spread across multiple servers.

### CNAME

A Canonical Name (CNAME) record is a type of DNS record that maps an alias name to a true or canonical domain name. In other words, it's an alternate name that points to a canonical name, which is the true or official name of a domain. When a client looks up a CNAME record, it will be directed to the canonical name and then to the IP address associated with that canonical name. This allows administrators to set up aliases for their domain names without having to change the IP address associated with each one.

## DHCP (Dynamic Host Configuration Protocol)

- DHCP performs dynamic addressing by automating the assignment of IPv4 addresses, subnet masks, gateways, and other networking parameters.
- When using static addressing, the network administrator manually enters IP address information on hosts.
- DHCP assign (leases) addresses from a pool of configured addresses to hosts that request an address.
- DHCP is preferred for address assignment on larger networks or where user population changes frequently.
- DHCP can allocate IP addresses for a configurable period of time, called a lease period.
- The lease period is an important DHCP setting and the address is returned to the DHCP pool for reuse when the lease period expires or the DHCP server gets a DHCPRELEASE message.
- Users can freely move from location to location and easily re-establish network connections through DHCP.

### DHCP messages

- IPv4, DHCP-configured device broadcasts a DHCP discover (DHCPDISCOVER) message to find available DHCP servers on the network
- DHCP server replies with a DHCP offer (DHCPOFFER) message, which offers a lease to the client including IPv4 address, subnet mask, DNS server, and default gateway
- The client may receive multiple DHCPOFFER messages if there is more than one DHCP server on the local network. Therefore, it must choose between them.
- Client sends DHCP request (DHCPREQUEST) message to accept the lease offer from a specific DHCP server
- DHCP server sends DHCP acknowledgment (DHCPACK) message to confirm the lease has been finalized or DHCP negative acknowledgment (DHCPNAK) message if offer is no longer valid
- If a DHCPNAK message is returned, then the selection process must begin again with a new DHCPDISCOVER message being transmitted
- Client must renew the lease prior to the lease expiration through another DHCPREQUEST message
- DHCPv6 messages are SOLICIT, ADVERTISE, INFORMATION REQUEST, and REPLY.

| DHCPv4 Message | Function |
| --- | --- |
| DHCPDISCOVER | Broadcast message sent by a client to request IP configuration parameters from DHCP servers |
| DHCPOFFER | Unicast message sent by a DHCP server to offer IP configuration parameters to a client |
| DHCPREQUEST | Broadcast or unicast message sent by a client to accept an offered IP configuration parameter from a DHCP server |
| DHCPACK | Unicast message sent by a DHCP server to confirm the allocation of IP configuration parameters to a client |
| DHCPNAK | Unicast message sent by a DHCP server to inform a client that its requested configuration is not available |
| DHCPRELEASE | Unicast message sent by a client to inform the DHCP server that it no longer requires its assigned IP address and that the address can be released back into the pool of available addresses |

