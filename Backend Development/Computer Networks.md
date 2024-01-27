**Network** ->
  - It is a group of interconnected people or items.
  - Computers connected with each other wired or wireless means is called a computer network.
**Internet** -> 
- It is the network of computer networks.
- Complex web of interconnected computer networks.
#### History of Internet 
- During 1957 Soviet Union launch their first satellite called Sputnik. In order to make advancement in the field of telecommunication and counter the innovation made by the Soviet union US government launched **ARPA**(Advanced Research Project Agency). 
- In 1960's-1970's due to the large scale of the ARPA facility different department were having trouble communicating with each other effectively to solve the issue at hand **ARPANET** was introduced which at that time used the **Transmission Control Protocol** which was later shifted to **TCP/IP**. During this time ARPANET was expanded to connect various sources of information like schools libraries and universities and it started being called **INTERNET**.
- In 1990's Tim Berner Lee invented the **World Wide Web**. After its introduction web browsers like **MOSAIC** and **NETSCAPE** came into the picture.

### Terminologies 

- `Network Protocols` -> are a set of rules and regulations setup to communicate and share information over a network. Ex - HTTP, UDP, SMTP, TCP etc.
- `Packets` -> We can't send big chunks of data over a network. For this reason data is divided into small chunks called **Packets** which are send over the network.
- `Address` -> Sending data over a network require destination details. These details which uniquely identify the end-system is called a Address.
- `Ports` -> In order to uniquely identify the specific process (application) running of the end-system for which data is being received over the network **PORTS**  are used.
    - Every process has a 16 bit port number. That ranges fro 0 to 6553.
    - `0-1023` -> These are called Well known Ports. These ports are reserved for specific application by default.
    - `1024-49512` -> These are called Registered Ports. These are used by specific, potentially proprietary apps/processes which are known but are not System Registered.
    - `49512-65536` -> These are called Dynamic Ports. These are currently not being used by any proprietary app or open-source software as their defaults and present for future purposes or to be used by the User.
 Note -> ( IP-Address + Port together are called a socket. )

- `Access Networks` -> These are the media using which an end-system connects to the Internet.
- `Network Interface Adapter` -> It enables a computer to connect to a network. As there are different  types of network it acts as single suite to connect over any network.
- `Digital Subscriber Line (DSL)` -> It uses the existing telephone groundwork to connect to a network. Generally DSL is provided by the same company which provides the telephone service
- `Internet Service Provider (ISP)` -> It is simply a company which provides end-users Internet. Ex - Jio, AT&T

### Network Protocols 
 - There are two types of Network Protocols stacks
     - `OSI Model` -> OSI stands for **Open System Interconnections**. It is a 7 layer stack. These are Application, Presentation,Session,Transport,Network,Data Link,Physical.
     - `TCP/IP` ->TCP/IP  stands for **Transmission Control Protocol/Internet Protocol**. It is a 5 layer stack. It bundles all the first three layers of the OSI model into the Application layer only hence making it a  5 layer  stack.

 - `Application Layer` -> It is this layer where the request originates. Ex- Email service, chat service etc
 - `Presentation Layer` -> It is this layer which is responsible for data presentation to rest of the layer , compression and encryption.
 - `Session Layer` -> This layer is responsible for User session management. Ex Login session on a website etc. 
 - `Transport Layer` -> This layer is responsible for division and management of big chunks of data into the smaller chunks or blobs which will be transferred over the network.
 - `Network Layer` -> It handles how routing of the packets is to be done over the network.
 - `Data Link Layer` -> It handles the Errors, flow control along with multiplexing and demultiplexing and handles addressing.

**Application Layer in Detail** 
 - Roles 
      1. Writing/providing data to network.
      2. Reading data from the user.
      3. Contains application that helps user to interact on the network.
      4. Error handling and recovery can be done.

 - It exists only on the End-systems only.
 - Also a lot of protocols of the Application layer depend upon the lower protocols of the transport layer.

##### Client Server Architecture
- It is a 2 level architecture containing a server-side and client-side.
- `Servers` -> It is basically a process that controls access to the centralised resource or a service such as a website or a web-app. 

##### P2P Architecture (Peer to Peer)
- It is sort of decentralised architecture where every machine is connected to one another.  Torrent is based on P2P architecture.

## HTTP 
- It stand for HyperText Transfer Protocol.
- `Objects` -> Web pages are main objects that contain other objects.Some other objects can be mp3 file, png, jpg file etc. Every object has a URL.
- It defines the whole procedure on how the client  and server will interact.
- HTTP is a stateless protocol i.e. the server does not stores any data about the client.
- HTTP depends on the TCP protocols of the transport layer. Firstly a TCP connection is setup over which a HTTP connection is setup and request/responses are sent over. 
- There are two types of HTTP connection.
     1. `Persistent HTTP` -> In this type of connection the multiple request-response cycles can exist without breaking the HTTP connection. Ex- **Web Sockets**
     2. `Non-Persistant HTTP` -> In this type of connection the HTTP connection over the TCP connection breaks after **ONE** request-response cycle.
- `HTTP Request Message`-> A HTTP request message is a plain text message. It consist of method , URL, HTTP version, status code etc.
- `User-Agent` -> It is contained inside the HTTP request message only. It consists information about the client.It is useful if the server has different webpages for different devices.
- `Accept-lang` -> Specifies the preferred language.

(Note -> Extra piece of information regarding the request are sent in the request headers.)

#### HTTP Methods 
- `GET` -> Request representation of specified resource from the server.
- `HEAD` ->  It asks for a response identical to GET but without a response body.
- `POST` -> It submits a entity to a specified resource on the server often causing a change in state of the server.
- `PUT` -> It replaces all the current representation of the targeted resource with the request payload.
- `PATCH` -> It does partial modification to a resource.
- `DELETE` -> Delete an object at the given URL.
- `OPTIONS` -> It describes the communication options for the target resource.
- `TRACE` -> It performs a message loop-back test along the path the target resource.
- `CONNECT` -> It establishes a tunnel to the server identified by the target resource.
 (Note -> The above mentioned uses of the methods is only a recommendation and not a compulsion to follow.)
#### URL 
- It stands for Uniform Resource Locator.
- It consists of the following 
     1. Protocol being used.
     2. Hostname
     3. Location of File/object.
     4. Arguments

### Cookies
- They are mainly concerned towards privacy.
- Cookies are unique identifier strings. These are set by the server through HTTP headers.
- As soon as a cookie is stored it can be sent along a subsequent HTTP request to the same server. This allows the server to know the identity of the client and hence serve the request accordingly.
- `Set-Cookie header` -> When a server wants to set up a cookie it includes `set-cookie: value` and sends it in the http response. This value is stored in the cookie file of the browser.

### SMTP 
- It stands for **Simple Mail Transfer Protocol**.It is Push protocol to send the mail. Pull Protocols like POP3/IMAP are used to access the Email.
- SMTP also used the below layer protocol TCP.
- For executing the functionality of Email **SMTP** along with **POP3** is used. SMTP is used to sent mails to the client which are stored in users inbox while POP3 is used to retrieve emails sent to the user.
- Connection of SMTP is done on PORT 25.
- When a Email is sent firstly it is sent to the senders SMTP server using the SMTP Protocol. Now the senders SMTP server places the email in a message queue. Now the SMTP server initiates a connections with receiver's SMTP server through a SMTP handshake. Now the Email is sent to the receiver's SMTP server from where it is downloaded on the receiver's machine.
- If receiver's SMTP server is offline then sender's SMTP server tries again and again after some delta time. There is a set threshold after which it stops trying and marks it **not delivered**.

### POP3
- It stands for Post office Protocol.(version3 hence a 3 in name)
- It downloads an email in 4 phases
     1. Connect
     2. Authorise
     3. Transaction
     4. Update
- There are two modes of POP3 protocol
    1. `Download & Keep`
    2. `Download & Delete`

### IMAP
- It stands for Internet Message access protocol.
- In this the Email are kept on the server and not deleted. Local copies of the email is cached and kept on the local device. If the Email is deleted manually by the user then only it gets deleted from the server.

### Bit Torrent
- Torrent is a peer to peer (P2P) file sharing protocol. A Bit Torrent client is the application that uses this protocols.
- Bit torrent follows a hybrid architecture instead of P2P.
- Data is downloaded and uploaded directly to and by the peers.
- A Bit Torrent client request for a file from multiple client in parallel.
- Small chunks of data are called **Pieces**.
- If a piece of data is downloaded successfully then the Bit Torrent client sends a message to other clients that this client has successfully downloaded piece and they can download it from it.
- These collaborating clients are collectively called `Swarms`

##### What does Bit-torrent do exactly?
- It breaks up the file into pieces
     1. For throughput pieces are large usually between 256KB to 1MB.
     2. For lesser latency these are further broken into sub-pieces.
     3. This breakup is done to ensure that the TCP stream transferring the file is lived long enough  that it's congestion windows can grown to a reasonable size.
- Pieces also ensure integrity
     1. A torrent contains a `SHA-1` hash of every piece so that data can be encrypted.
- UnderHood Mechanism
    1. Peers exchanges the pieces they have.
    2. Peers download the rarest piece among the peers available first. If any piece is unavailable in all the clients then no one can down it. This is called the `Rarest first policy`.
    3. If very few peers have the piece then it becomes a bottleneck to the download.
- `TFT Policy` - Tit for Tat policy
    1. In this policy you send data to peers, who send you the data.Therefore peers who contribute can download faster.
    2. This is achieved using a process called `Choking`. When happens in this process is following 
         1. Initially all the peers act as a choke.
         2. Now suppose a peer X checks the download rate of all the peers connected to it then it exacts the Top P peers which highest upload-download rate and un-chokes them and divides all the uplink capacity bandwidth to each of these P peers equally. 
         3. Now the problem arises that each of the peer might not require the same bandwidth being allocated to them.
    3. To solve the problems in `Choking` `BIT-TYRANT` was introduced.
        1. In this you preferentially gain access to the download.
        2. It increases the **throughput** by 70%.
        3. It ensures that each peer uses the uplink capacity exactly equal to what they need so that new peers can be added to top P peers.
#### Torrent file
- Clients join a swarm by downloading a `.torrent` file. It consists of the following data
   1. Gives info about the file to be downloaded, size and number of pieces  along with the information on how to start interacting with other clients in the swarm.
   2. Also gives information about the `Trackers`.(A server which tracker who all are participating in the swarm)
- When a client joins a swarm it request the information about the already present clients from the tracker and starts to communicate with them over TCP initially as a `Leecher`.
- When the size of Swarms increase then `Tracker Less` torrent are used which use the Distributed Hash table(DHT) which is a distributed co-ordination mechanism wherein information about the swarms are stored in many nodes.


### Transport Layer
- The key responsibility of this layer is to extend the Network to the Applications.
- Transport layers and its protocols reside on the end-system.
##### Responsibility of Transport Layer
- `Segments Data` -> It divides the data into manageable pieces which are called `SEGEMENTS` if TCP Protocol is used or `DATAGRAMS` if UDP Protocol is used.
- `Allow Multiple Conversations` -> It tracks each application to application connection or conversation separately and hence allows multiple conversations to occur.
- `Multiplexing Data` ->  It gathers data from multiple application processes of the sender, envelops that data into headers and sends it as a whole to the intended receiver. It also allows messages to be send to more than one destination host via single medium.
- `Demultiplexing Data` -> Delivering received segments at receivers side to the correct application layer processes is called data demultiplexing.
- `Reliable Data Transfer` -> There are a lot of network layer imperfections that transport layer is supposed to deal with 
    1. Segments can be corrupted.
    2. Segments can be lost.
    3. Segments can reordered or duplicated.

###### Workarounds for Reliable Data Transfer 
- `Checksums` -> The first imperfection for the network layer is that Segments can corrupted by transmission errors. **Checksums** is an error detection mechanism. Checksums( Arithmetic sum of the bits ) is attached to the Segment and is validated by the receiver.
- `Retransmission Timers` -> The second imperfection of the network layer was data can be lost. To solve this retransmission timers are used wherein the value of retransmission timers must be greater than the round-trip time of the request along with some added delta. Using this method if the acknowledgement is not received at the sender's end after sending the segment then if can be concluded that there was some issue in the data transmission. After the expiration of timer if acknowledgement is not received then the Segment is send again.
(Note -> If the Receiver successfully received the segment but for some reason the acknowledgement was not received at the sender then their might be a case that the Segment is send again and this is not handled by Retransmission timers. )
- `Sequence Numbers` -> To tackle the limitation of the Retransmission timers Sequence Numbers are send along with the Segments. Now if a Segment is received the receiver end with the same Sequence Number then is will not be downloaded. This also solves the problem of reordering of Segments as the Sequence Numbers are consecutive. 
- `Sliding Window` -> It is used to avoid overload on the receiver's end.These are a set of consecutive numbers that the sender uses in transmitting  to ensure the waitlisted data transfer. At the beginning of the session, sender & receiver agree on a window size. 


## TCP 
- It stand for transmission control protocol.It is a protocol of the transport layer.
- What does TCP does?
    1. Send data at appropriate transmission rate.
    2. Segment data 
    3. Congestion Control
    4. Identify and Retransmit message
- Application of TCP 
    1. `FTP` -> File transfer Protocol. Runs on Ports 20 and 21.
    2. `SSH` -> Secure Shell Protocol.It is used to provide a secure connection to a remote Host over a unsecured network.
    3. `Email`
    4. `Web Browsing` -> HTTP connection happens over TCP.
- Key Features of TCP
    1. `Connection Oriented` -> It creates a long-term connection between the send and the host. It is terminated only when either one of them terminates the connection.
    2. `Full Duplex Connectino` -> It means that both sender and host can be send request/responses to each other simultaneously.
    3. `Point to Point Transmission` -> It has exactly two endpoints and hence does not support broadcasting.
    4. `Error Control`
    5. `Congestion Control`
##### Segment Header 
It consists of the following information.
- `Source Port Number` -> 2 bytes
- `Destination Port Number` -> 2 bytes
- `Sequence Number` -> 4 bytes
- `Acknowledgement Number` -> 4 bytes
- `Header Length`-> 4 bits
- `Reserved Bits` -> 4 bits
- `8 flags` -> 8 bits 
    1. `ACK` -> Acknowledgement flag
    2. `RST` -> Reset flag
    3. `SIN` -> Synchronisation flag
    4. `FIN` -> Finish flag
    5. `CWR`-> Congestion window reduced. On receiving the ECN flag the host reduces the congestion by turning on the CWR flag.
    6. `ECN`-> Explicit congestion notification.It is send by the receiver and send to the host.
    7. `PSH` -> Push flag
    8. `URG` -> Urgent Flag. If this flag is send the its message value is read immediately for the Urgent Pointer.
- `Window Size` -> 2 bytes
- `Checksum`-> 2 bytes
- `Urgent Pointer` -> 2 bytes
- `Option and Padding` -> 40 bytes

### 3 Way Handshake
1. Firstly the client sends a connection request with a Sequence Number (x) and `SYN` flag and no `ACK` flag.
2. Now the server sends a response back to the client with a Sequence Number (y) and **Acknowledgement Number** equal to `x+1` along with the `SYN` and `ACK` flag.
3. Now the client again sends a connection request with a Sequence Number equal to `x+1` and acknowledgement number equal to Sequence Number plus one received from the server `y+1` along with the `ACK` flag and not the `SYN` flag this time.
4. After this a connection is established.

### UDP Protocol
- It stands for User Datagram Protocol.
- It is used by apps that do not require the guaranteed delivery service of the TCP either because the application handles it on its own or the reliable delivery service is not required.
- It gets the data converts it to UDP datagram and sends it over the network.
- It is used in Name translation of DNS and XBOX uses the UDP Protocol.
##### UDP Header
- Its max possible size it 65536 bytes.
- Header size is maximum 8 bytes and rest is data.
- Header consist of the following 
    1. `Source Port Number`-> 2 bytes
    2. `Destination Port Number`-> 2 bytes
    3. `Checksum`-> 2 bytes
    4. `Length`-> 2 bytes

### Internet Protocol (IPV4)
- It is a network layer protocol.
-  It was designed by keeping mind the following assumptions
    1. It should provide unreliable connectionless servers. This is so that packets can be transmitted through different routes instead of following a set route for source to destination.
    2. It should have  fixed 32 bit size address.
    3. IP should be able to exchange variable length packets.
- `Address Assignment` -> 
    1. A naive solution will be to assign IP addresses on first come first serve basis but this would have scalability issues.
    2. `Subnetting`-> In this approach routers only maintain routes towards **blocks of addresses** and these blocks are assigned to various ISP which mount the **sub-blocks** to these addresses in individual manner.These sub-blocks are called `Subnets`.
    3. A typical subnet groups all the hosts that are part of the same enterprise. A enterprise network is usually composed of several LAN's interconnected by routers. A small block of IP addresses from the enterprise block is usually assigned to a LAN.
- IP address has two parts
    1. `Subnetwork Id` -> Higher order bits.
    2. `Host Id`-> Lower order bits.
- `Address Classes` 
     1. When a router need to send a packet it must know the **Subnet**  of the destination address to be able to construct its routing table for forwarding the packet. To achieve this it was proposed to use the higher order bits of the address to encode the length of `Subnet:identifer`
     2. We have first classes - A,B,C,D,E
        1. `Class A`
            - In class A first bit is always zero therefore we have 2^31 addresses only as 1 bit is always fixed.
            - First 8 bits represent network Id and rest of the bits represent the Host Id.
            - Number of Network Id is class A is 2^7 and host id are 2^24 Host id's
            - Default mask for class A is `255.0.0.0`. These mask are used to detect the network Id of Class A by doing `bitwise and` with the given network address.
            - ID's `X.0.0.0`(network Id) and `X.255.255.255`(broadcast Id) are reserved within class A. Hence 2^24-2 unique host are present in class A.
        2. `Class B`
            - In class B the first two bits are set 1,0 respectively.
            - Range of first octet is 128-191.
            - Total number of IP address are 2^30.
            - First two octets tell us about the network Id so therefore there are 2^14 network Id in class B.
            - Number of Host are 2^16.
            - ID's `X.Y.0.0`(network Id) and `X.Y.255.255`(broadcast address) are reserved in class B. Hence 2^16-2 unique host are present in class B.
            - Default mask for class B is `255.255.0.0`
        3. `Class C`
            - In class C first three bits are set 1,1,0 respectively.
            - Range of first octet is 192-223.
            - Total number of IP address are 2^29.
            - Total number of Hosts is 2^8.
            - First three octets tell us about the network Id so there are 2^21 network Id in class C.
            - Default mask for class C is `255.255.255.0` with ID's `X.Y.Z.0`( network Id) and `X.Y.Z.255`( broadcast Id) are reserved in class C therefore 2^8-2 unique host are present in class C.
        4. `Class D`
            - In class D first four bits are 1,1,1,0 respectively.
            - Range of first octet is 224-239.
            - Total number of IP address are 2^28.
            - Default mask for class D is `255.255.0.0`
            - There is no host or network Id here as these are reserved for special purposes.
        5. `Class E`
            - In class E first four bits are 1,1,1,1.
            - Range of first octet is 240-255.
            - These are reserved for special military purpose.
    3. Disadvantages of Classful Addressing
        1. Wastage of IP addresses.
        2. Maintenance and time consuming.
        3. More prone to errors.
    4. `Subnetting in Classful Addressing`
        - In affect in done on the network Id.
        - First for subnetting the address into the respective classes default mask of each class in operated with the address using bitwise or.
        - Then for dividing the subnet in further  say X subnets first **X bits of the Host Id** are fixed with all possible combination available. Example For X =1 we have 2 combination 0,1 and hence all host will host id starting with 0 will be part of one subnet and host with Id starting with 1 will be part of the other subnet.
        - Now for identifying the correct subnet for request redirection we create a Host mask will first X bits of the host Id be set and bitwise or Operation in done to filter the request.
- `Classless Addressing
    1. In classless Address there are no classes only blocks are present with the general notation being `X.Y.Z.W/N` where N is mask or the number of bits to represent the block.
    2. The value of N  can be maximum 32.So if the value of the N is 28 then it would signify that the first 28 bits in the mask are set and rest are 0's. Therefore total network Id present will be 2^N and total Host present will be 2^(32-N) out of which 2 will be reserved for Network Id and broadcast Id so unique host present will be 2^(32-N)-2
    3. Rules in classless Addressing
        - Address should be continuous.
        - No. of address in a block should be of power of 2.
        - Network address should be divisible by the size of the block.
    4. `Subnetting in Classless Addressing`
        - No affect is done on the Network Id.
        - Same process is done as in Classful Addressing but the only difference is that instead of Default mask being alter know they are creating using the `/N` part of the address.


### IPV6 Protocol
- It is a 128 bit Address.
- Address is divided into 2 parts `Subnet Prefix` and `Host Suffix`.
- Uses 8 octets and can be represented by using Hexadecimal values as 8 blocks of 16 bit each.
- Can omit single runs of Zeroes by using ::
- Uses brackets in URL.
- Address assignment in done similar to IPV4 addressing with the same `/N` notation.

We can auto generate a IPV6 address from a `subnet/64` and ethernet address. Ethernet has a 48 bit address with initial 24 bits being allocated to the manufacturer and last 24 bits are for the devices.
Convert the 48 bit ethernet address to 64 bit Host Id by sticking `Oxfffe` in the middle of manufacturer address and device address.