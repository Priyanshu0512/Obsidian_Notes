
### **Strong Coupling vs. Weak Coupling in Backend Communication**

In backend communication, **coupling** refers to the degree of dependency between different components or services. Understanding the difference between **strong (tight) coupling** and **weak (loose) coupling** is critical when designing scalable, maintainable, and robust backend systems.

---
### **Strong Coupling**

#### Definition
Strong coupling occurs when two components or services are highly dependent on each other. Changes in one component often require changes in the other, and the components typically communicate directly and in a tightly integrated manner.

#### **Characteristics**

1. **Direct Communication**:
    - Components or services invoke each other’s APIs directly (e.g., via HTTP or RPC).
    - Example: A service directly calls another service and expects a specific response format.
2. **Synchronous Communication**:
    - Strongly coupled systems often rely on synchronous communication, where the caller waits for a response before proceeding.
3. **Shared Data Structures**:
    - Components may share data schemas or use a common database, leading to dependencies.
4. **Limited Autonomy**:
    - Changes in one component can have cascading effects on other components.

---

### **Weak Coupling**

#### **Definition**
Weak coupling occurs when components or services are designed to be minimally dependent on each other. They communicate in a way that allows them to operate independently, often using intermediaries or asynchronous methods.

#### **Characteristics**

1. **Intermediaries**:
    - Services communicate through message queues, event streams, or brokers (e.g., RabbitMQ, Kafka).
    - Example: Service A publishes an event to a queue; Service B processes it.
2. **Asynchronous Communication**:
    - Services do not wait for immediate responses. Instead, they work on separate timelines.
3. **Independent Data Stores**:
    - Each service manages its own database, avoiding schema dependencies.
4. **High Autonomy**:
    - Changes in one service have minimal or no impact on others.

---

# WebSockets 

**WebSockets** are a communication protocol that provides full-duplex (two-way) communication channels over a single TCP connection. Unlike traditional HTTP requests, which are stateless and unidirectional, WebSockets allow for real-time, persistent communication between a client and a server.


> Good example - [https://www.binance.com/en/trade/SOL_USDT?type=spot](https://www.binance.com/en/trade/SOL_USDT?type=spot)

#### Why not use HTTP/REST? Why do you need ws?

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2F337fdfd4-982f-4476-b225-c9b705344a54%2FScreenshot_2024-04-06_at_4.43.39_PM.png?table=block&id=c1b393de-60bc-4c09-8143-ae3d34e240ad&cache=v2)

1. **Network Handshake happens for every request**
2. No way to push server side events (You can use polling but not the best approach)

---

> Note - Socket.io is not a complete implementation of WebSockets. Hence a WebSocket server will not be able to communicate with a Socket.io server.


### Implementation 

```typescript

import express from 'express'
import { WebSocketServer } from 'ws'

const app = express()
const httpServer = app.listen(8080)

const wss = new WebSocketServer({ server: httpServer });

wss.on('connection', function connection(ws) {
  ws.on('error', console.error);

  ws.on('message', function message(data, isBinary) {
    wss.clients.forEach(function each(client) {
      if (client.readyState === WebSocket.OPEN) {
        client.send(data, { binary: isBinary });
      }
    });
  });

  ws.send('Hello! Message From Server!!');
});

```

> Note - A HTTP server is required initially to connect sender and receiver. Then the server object is passed to the `WebSocketServer`

For a Next.js code remember to use `use client`  while using `websocket` connection on the client.

---

## Scaling WS Servers 

In the real world, you’d want more than one websocket servers (Especially as your website gets more traffic). The way to scale websocket servers usually happens by creating a `ws fleet`.
There is usually a central layer behind it that `orchestrates` messages

ws servers are kept `stateless`

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2Fb44488cf-22da-4480-ad1c-402d93799e62%2FScreenshot_2024-04-06_at_6.06.53_PM.png?table=block&id=4f0ed422-3897-4b48-8eea-925ab9118f18&cache=v2)

What happens here is whichever websocket servers need to connect to each other subscribes to the same in the pub-sub server and hence whenever a message is published the respective server subscribes the message hence maintaining a persistent connection.

---

