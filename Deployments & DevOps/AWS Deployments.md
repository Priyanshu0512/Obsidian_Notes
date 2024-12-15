VMs on AWS are called EC2 Servers

>  EC2 stands for Elastic compute Version 2.
	`Elastic` - Can increase/decrease the size of the machine
	`Compute` - It is a machine

You can spin up a new EC2 instance from the aws dashboard

---
### Creating an EC2 instance

### Step Involved
1. Go to EC2 instance page and click on launch instance.
2. Give the instance name and select the OS.
3. Select the size of the instance depending upon the needs.
4. Create a new key-value pair.( It downloads a `.pem` files)
5. Select the compute size within the instance.
6. Toggle the Network settings to allow HTTP/HTTPS traffic as per need.
7. Now launch the instance.

---

### **TLS (Transport Layer Security)**

#### Purpose:  
TLS is primarily used to secure communication over a network. It ensures that data transmitted between two parties (e.g., a client and a server) is encrypted, authenticated, and tamper-proof.

**Key Features**:

1. **Encryption**: Prevents eavesdropping.
2. **Authentication**: Verifies the identity of the communicating parties, often using certificates (e.g., HTTPS uses TLS for web traffic).
3. **Data Integrity**: Ensures that the transmitted data hasn’t been altered.

**Common Use Cases**:

- Securing web traffic (HTTPS).
- Email protocols (SMTP, IMAP, POP3).
- VPNs and other network communications.

**Protocols Involved**:

- Works at the **application layer** of the OSI model.
- Uses digital certificates (e.g., X.509) for authentication.

**Example**: When you visit a website starting with `https://`, TLS encrypts the communication between your browser and the website's server.

---
### **SSH (Secure Shell)**

**Purpose**:  
SSH is a protocol for securely accessing and managing systems remotely. It’s mainly used to establish a secure terminal session and transfer files between computers.

**Key Features**:

1. **Encryption**: Protects data transmitted during the session.
2. **Authentication**: Uses public-private key pairs or passwords to verify the user.
3. **Command Execution**: Allows users to execute commands on a remote system securely.
4. **Port Forwarding**: Can tunnel other protocols through SSH.

**Common Use Cases**:

- Remote system login and administration (e.g., accessing a Linux server).
- Secure file transfers (SCP, SFTP).
- Secure tunneling and port forwarding.

**Protocols Involved**:

- Operates at the **application layer** but facilitates command execution at lower layers.

**Example**: Using `ssh user@hostname` to access a remote server securely.


### SSH into the Instance

```bash
chmod 700 first-instance.pem
```

Since the connection to the remote needs to be very secure hence the connection key has to be give the complete permission to ssh into the server. ( Here 700 means complete permissions is give to the current user only other user have no permission to perform any operation onto this key.)

```shell
ssh -i First-instance.pem ubuntu@16.171.176.153
```

> Instead of the I.P address domain name can also be given provided in the AWS dashboard.

---
### Security groups 

In AWS, **Security Groups** are a key feature used to control inbound and outbound traffic to your EC2 instances and other resources. They act as virtual firewalls at the instance level, allowing you to define rules that determine which types of traffic are permitted or denied.

### **Key Features of Security Groups**

1. **Stateful**:
    - If you allow inbound traffic, the corresponding outbound response is automatically allowed (and vice versa). No explicit outbound rule is needed for responses.
    
2. **Rule-Based**:
    - Security groups operate based on rules that define traffic permissions.
    - Rules can specify:
        - **Protocol** (e.g., TCP, UDP, ICMP).
        - **Port Range** (e.g., port 22 for SSH , port 80 for HTTP ).
        - **Source/Destination**: IP address ranges (CIDR blocks), other security groups, or specific instances.
    
3. **Default Deny**:
    - By default, all inbound and outbound traffic is **denied** unless explicitly allowed by rules.


> Common Ports 
> HTTP(IPv4)- 80
> HTTPS(IPv6)- 443
> SSH - 22 

Note - If the port is specified with `:<port-number` in the URL then the request goes to the process running on that port else it goes to 443,80 or 22 depending upon http version used or trying to SSH into the server.

--- 
### NGINX

**NGINX** is a high-performance, open-source software used for **web serving**, reverse proxying, caching, load balancing, and more. It is widely known for its speed, reliability, and scalability, making it a popular choice for modern web applications.

#### Architecture of NGINX:

NGINX uses an **event-driven, asynchronous architecture**, which allows it to handle many requests simultaneously using minimal resources. This contrasts with traditional thread-based servers (like Apache), which may spawn a thread for each request.

```bash
sudo apt update
sudo apt install nginx
```
