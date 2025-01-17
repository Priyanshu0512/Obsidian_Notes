

WebRTC (Web Real-Time Communication) is an open-source technology standard that enables real-time audio, video, and data communication between web browsers and mobile applications without requiring intermediary servers. It powers applications like video conferencing, live streaming, file sharing, and online gaming by allowing peer-to-peer (P2P) connections.

> Note - In scenario's like streaming matches and events  implementing WebRtc does not make a lot of sense and video can be upload from the source to the server for transcoding and then forwarded to clients requesting them. A delay of 10-15sec is admissible. Usually a WebTC servers are used for p2p connection where sub second data transmissions are required (very low-latency) without the need of a server in between.

---

## Signalling Server 

Signaling is the process of exchanging necessary metadata and connection information between two peers before they can establish a direct WebRTC connection.
- Exchange of Session Description Protocol (SDP)
- Exchange of ICE Candidates


WebRTC does not define a signaling protocol. Instead, developers can use any communication method to handle signaling, such as:
- **WebSockets**
- **HTTP/HTTPS**
- **Socket.IO**

---
### STUN Servers

A **STUN (Session Traversal Utilities for NAT)** server helps WebRTC clients discover their public IP address and port when they are behind a NAT (Network Address Translation) device.
#### Key Roles of STUN

1. **NAT Traversal**:
    - NAT devices often translate a private local IP address into a public IP address to allow communication with external networks.
    - Peers need their public IP and port to connect directly when behind NAT.
    
2. **Public Address Discovery**:
    - A STUN server allows a peer to query its public-facing IP address and port.

#### How STUN Works

1. A WebRTC client sends a request to the STUN server over UDP.
2. The STUN server responds with the client’s public IP address and port.
3. The WebRTC client uses this information to generate ICE candidates, which are shared with the other peer during signaling.

#### Types of NATs and STUN’s Role

- **Full-Cone NAT**:
    - Easily handles direct peer-to-peer communication.
- **Symmetric NAT**:
    - Challenging for direct communication, often requires TURN servers

---
### What Are Symmetric NATs?

**Symmetric NAT** is a type of Network Address Translation (NAT) that is more restrictive in how it handles network traffic. It assigns a unique public IP address and port for each specific destination a device inside the private network communicates with.

---
### How Symmetric NAT Works

1. When a device inside a private network (e.g., 192.168.1.10:12345) sends traffic to an external destination (e.g., 8.8.8.8:53), the NAT device:
    - Translates the private source IP and port into a public-facing IP and port (e.g., 203.0.113.10:54321).
    - This mapping is stored in the NAT table.

2. If the same internal device sends traffic to a different external destination (e.g., 1.1.1.1:80), the NAT device:
    - Assigns a new, different public IP and port pair (e.g., 203.0.113.10:54322).
    
3. The NAT device only allows responses from the specific external IP and port pairs that match the entries in its NAT table. Any other incoming traffic is dropped.

---
### Turn server

A lot of times, your network doesn’t allow media to come in from `browser 2` . This depends on how restrictive your network is.Since the `ice candidate` is discovered by the `stun server`, your network `might` block incoming data from `browser 2` and only allow it from the `stun server`. Basically when using a TURN server it also acts as a STUN server to get the ICE candidates.

---
### What Are ICE Candidates?

ICE (Interactive Connectivity Establishment) candidates are pieces of information used in WebRTC (and other peer-to-peer communication technologies) to describe potential connection endpoints that a device can use to establish a connection with a remote peer.

These candidates are part of the ICE framework, which helps devices discover the best network path for communication, even if they are behind NATs (Network Address Translators) or firewalls.

>  All possible ways the peers can connect** (direct or relayed). The most efficient route** for data transfer (e.g., avoiding relay servers like TURN if possible).

### Types of ICE Candidates

1. **Host Candidates**:
    - Represent the device's local IP address and port.
    - Example: `192.168.1.100:5050`.
    - Generated for every network interface the device has (Wi-Fi, Ethernet, etc.).
    - Limited to direct connections within the same network.
    
2. **Server-Reflexive Candidates**:
    - Represent the public IP and port as seen by an external server (e.g., a STUN server).
    - Used when the device is behind a NAT to understand how its local address translates to a public address.
    - Example: `203.0.113.10:54876`.
    
3. **Relayed Candidates**:
    - Represent the IP and port of a TURN server that will relay traffic between the peers.
    - Used as a fallback when direct communication fails (e.g., due to symmetric NATs).
    - Example: `198.51.100.5:3478`.

---

> Each peer collects its available candidates (host, server-reflexive, and relayed) from its local interfaces and STUN/TURN serversUsing the ICE framework, both peers test the connectivity of the gathered candidates by sending `ping-like `messages (STUN Binding Requests). These checks help identify which candidates can successfully establish a connection.Each peer combines its candidates with the remote peer's candidates, creating "candidate pairs."

 Candidate pairs are prioritized based on factors like:
 - Candidate type (host > server-reflexive > relayed).
-  Network performance (latency, bandwidth).

---
### ICE Candidate Example

```ICE Candidate
candidate:842163049 1 udp 2122260223 192.168.1.100 5050 typ host

```

- `842163049`: Foundation (unique identifier for the candidate).
- `1`: Component ID (1 = RTP, 2 = RTCP).
- `udp`: Transport protocol (UDP in this case).
- `2122260223`: Priority (higher values indicate higher priority).
- `192.168.1.100`: IP address.
- `5050`: Port number.
- `typ host`: Candidate type (host in this case).

---
##### ICE Candidate Gathering Process
1. Local Gathering
2. STUN Query
3. TURN Allocation

---
### Optimizations in ICE

1. **Trickle ICE**:
    - ICE candidates are sent to the remote peer as they are discovered, rather than waiting to gather all candidates.
    - Speeds up the connection process.
2. **ICE Lite**:
    - Used in server-side WebRTC implementations that only generate host candidates (e.g., for media streaming servers).

---

### Terminologies 

- `Offer` - The process of the first browser (the one initiating connection) sending their `ice candidates` to the other side.
- `Answer`- The other side returning their `ice candidates` is called the answer.
- `SDP` - Session description protocol. A single file that contains all your
	1. ice candidates
	2. what media you want to send, what protocols you’ve used to encode the media

```SDP

v=0
o=- 423904492236154649 2 IN IP4 127.0.0.1
s=-
t=0 0
m=audio 49170 RTP/AVP 0
c=IN IP4 192.168.1.101
a=rtpmap:0 PCMU/8000
a=ice-options:trickle
a=candidate:1 1 UDP 2122260223 192.168.1.101 49170 typ host
a=candidate:2 1 UDP 2122194687 10.0.1.1 49171 typ host
a=candidate:3 1 UDP 1685987071 93.184.216.34 49172 typ srflx raddr 10.0.1.1 rport 49171
a=candidate:4 1 UDP 41819902 10.1.1.1 3478 typ relay raddr 93.184.216.34 rport 49172

```

---

# Connecting the two sides

The steps to create a WebRTC connection between 2 sides includes -

1. Browser 1 creates an `RTCPeerConnection`
2. Browser 1 creates an `offer`
3. Browser 1 sets the `local description` to the offer
4. Browser 1 sends the offer to the other side through the `signaling server`
5. Browser 2 receives the `offer` from the `signaling server`
6. Browser 2 sets the `remote description` to the `offer`
7. Browser 2 creates an `answer`
8. Browser 2 sets the `local description` to be the `answer`
9. Browser 2 sends the `answer` to the other side through the `signaling server`
10. Browser 1 receives the `answer` and sets the `remote description`

This is just to `establish` the `p2p` connection b/w the two parties

To actually send media, we have to
1. Ask for camera /mic permissions
2. Get the `audio` and `video` streams
3. Call `addTrack` on the `pc`
4. This would trigger a `onTrack` callback on the other side

---
## Implementation

 Backend -  
```typescript

import { WebSocketServer, WebSocket } from "ws";

const wss = new WebSocket.Server({ port: 8081, clientTracking: true });

let senderSocket: WebSocket | null = null;
let receiverSocket: WebSocket | null = null;

wss.on("connection", function connection(ws) {
  ws.on("error", console.error);
  ws.on("message", function message(data: any) {
    const msg = JSON.parse(data);
    if (msg.type === "sender") {
      senderSocket = ws;
    } else if (msg.type === "receiver") {
      receiverSocket = ws;
    } else if (msg.type === "createOffer") {
      if (ws != senderSocket) {
        return;
      }
      receiverSocket?.send(
        JSON.stringify({ type: "createOffer", sdp: msg.sdp })
      );
    } else if (msg.type === "createAnswer") {
      if (ws != receiverSocket) {
        return;
      }
      senderSocket?.send(
        JSON.stringify({ type: "createAnswer", sdp: msg.sdp })
      );
    } else if (msg.type == "iceCandidate") {
      if (ws === senderSocket) {
        receiverSocket?.send(
          JSON.stringify({ type: "iceCandidate", candidate: msg.candidate })
        );
      } else if (ws == receiverSocket) {
        senderSocket?.send(
          JSON.stringify({ type: "iceCandidate", candidate: msg.candidate })
        );
      }
    }
  });
});


```




>Note - You can look at a bunch of stats/sdps in `about:webrtc-internals`

Sender side - 

```typescript

import { useEffect, useState } from "react";

export const Sender = () => {
  const [socket, setSocket] = useState<WebSocket | null>(null);

  useEffect(() => {
    const socket = new WebSocket("ws://localhost:8081");
    setSocket(socket);
    socket.onopen = () => {
      socket.send(JSON.stringify({ type: "sender" }));
    };
  }, []);

  const initialConnection = async () => {
    if (!socket) {
      alert("Socket Not Found");
      return;
    }

    const pcConnection = new RTCPeerConnection();

    pcConnection.onnegotiationneeded = async () => {
      pcConnection.onicecandidate = (event) => {
        if (event.candidate) {
          socket?.send(
            JSON.stringify({ type: "iceCandidate", candidate: event.candidate })
          );
        }
      };
      const offer = await pcConnection.createOffer();
      await pcConnection.setLocalDescription(offer);
      socket?.send(
        JSON.stringify({
          type: "createOffer",
          sdp: pcConnection.localDescription,
        })
      );
    };

    socket.onmessage = (event) => {
      const message = JSON.parse(event.data);
      if (message.type === "createAnswer") {
        pcConnection.setRemoteDescription(message.sdp);
      } else if (message.type == "iceCandidate") {
        console.log(message.candidate);
        pcConnection.addIceCandidate(message.candidate);
      }
    };
    getCameraStreamAndSend(pcConnection);
  };

  const getCameraStreamAndSend = (pcConnection: RTCPeerConnection) => {
    navigator.mediaDevices
      .getUserMedia({ video: true, audio: false })
      .then((stream) => {
        const video = document.createElement("video");
        video.srcObject = stream;
        video.play();
        document.body.appendChild(video);
        stream.getTracks().forEach((track) => {
          pcConnection?.addTrack(track);
        });
      });
  };
  return (
    <div>
      Sender
      <button onClick={initialConnection}> Send data </button>
    </div>
  );
};


```


Receiver side - 

```typescript 
import { useEffect } from "react";

export const Receiver = () => {
  useEffect(() => {
    const socket = new WebSocket("ws://localhost:8081");

    socket.onopen = () => {
      socket.send(JSON.stringify({ type: "receiver" }));
    };
    startStreaming(socket);
  }, []);

  function startStreaming(socket: WebSocket) {
    const pc = new RTCPeerConnection();
    socket.onmessage = async (event) => {
      const message = JSON.parse(event.data);
      if (message.type === "createOffer") {
        await pc.setRemoteDescription(message.sdp);
        const answer = await pc.createAnswer();
        await pc.setLocalDescription(answer);
        socket.send(
          JSON.stringify({
            type: "createAnswer",
            sdp: answer,
          })
        );
      } else if (message.type === "iceCandidate") {
        pc.addIceCandidate(message.candidate);
      }

      pc.ontrack = (event) => {
        const video = document.createElement("video");
        video.srcObject = new MediaStream([event.track]);
        video.controls = true;
        video.autoplay = true;
        video.muted = true;
        document.body.appendChild(video);

        video.play().catch((error) => {
          console.error("Error while playing video:", error);
        });
      };
    };
  }
  return <div>Receiveing videos ....</div>;
};
```


---
### Trickle ICE in WebRTC

**Trickle ICE (Interactive Connectivity Establishment)** is a mechanism used in WebRTC to gather and exchange network candidates (IP addresses and ports) incrementally between peers to establish a connection as quickly as possible. This method optimizes connection setup by allowing ICE candidates to be sent and processed as they are discovered, instead of waiting for all candidates to be gathered before sending them.

### How Trickle ICE Works

1. **Candidate Gathering**:
    - The WebRTC client begins gathering ICE candidates from various sources:
        - Host candidates (local network interfaces).
        - Reflexive candidates (public-facing IPs via STUN servers).
        - Relay candidates (via TURN servers for NAT traversal).
2. **Trickling Candidates**:
    - As each candidate is discovered, it is sent to the remote peer immediately, instead of waiting for all candidates to be gathered.
    - The remote peer processes and tests connectivity with each candidate as it arrives.
3. **Connection Establishment**:
    - The peers test different combinations of candidates (candidate pairs) to determine the best path for communication (based on criteria like latency and packet loss).
    - Once a valid pair is found, the connection is established, even if more candidates are still being gathered.

---
## Other architectures

There are two other popular architectures for doing WebRTC
1. SFU
2. MCU

Problem with P2P architecture is that is does not scale well beyond 3-4 people. 

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2Feecbe4a3-2b10-421a-8e42-1de3f10173ba%2FScreenshot_2024-05-04_at_7.55.05_PM.png?table=block&id=80cbf71c-099d-4d03-ba10-33f1c24d1e55&cache=v2)

### SFU's 

A **Selective Forwarding Unit (SFU)** is a media server architecture used in real-time communication systems like video conferencing, live streaming, and online gaming. It acts as a middle layer between the sender and receiver(s) to efficiently manage and route media streams.


### How SFU Works

1. **Media Streams**:
    - Each participant in a session sends their audio/video streams to the SFU.
2. **Forwarding Logic**:
    - The SFU selectively forwards the streams to other participants based on specific criteria (e.g., network conditions, participant priorities).
3. **No Media Processing**:
    - SFUs do not transcode or process media streams. They simply forward them as-is, often based on participant subscriptions.
4. **Optimization**:
    - SFUs handle dynamic changes in the network by adapting the quality and number of streams forwarded to each participant.

---

## MCU (Multipoint Control Unit )

A **Multipoint Control Unit (MCU)** is a media server architecture used in real-time communication systems, such as video conferencing and telepresence. Unlike the **Selective Forwarding Unit (SFU)**, the MCU processes and mixes media streams before forwarding them to participants. This centralized processing approach simplifies the client-side requirements but increases the server's workload.

---
### How MCU Works

1. **Stream Reception**:
    - Each participant sends their audio and video streams to the MCU.
2. **Media Processing**:
    - The MCU processes incoming streams, which can include decoding, mixing, and encoding them into a single composite stream.
3. **Stream Distribution**:
    - The processed stream is then sent to all participants. This reduces bandwidth requirements for participants, as they receive only one mixed stream.

---

### MCU vs SFU: Which to Choose?

| Feature              | MCU                             | SFU                                |
| -------------------- | ------------------------------- | ---------------------------------- |
| **Media Processing** | Decodes, mixes, and encodes     | Forwards streams as-is             |
| **Server Load**      | High                            | Low                                |
| **Client Bandwidth** | Low                             | Higher (receives multiple streams) |
| **Latency**          | Higher                          | Lower                              |
| **Scalability**      | Limited                         | Highly scalable                    |
| **Best Use Case**    | Small groups, consistent layout | Large groups, adaptive quality     |

---
