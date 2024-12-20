VMs on AWS are called EC2 Servers

  EC2 stands for Elastic compute Version 2.
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


 **Common Ports** 
- HTTP(IPv4)- 80
- HTTPS(IPv6)- 443
- SSH - 22 

Note - If the port is specified with `:<port-number>` in the URL then the request goes to the process running on that port else it goes to 443,80 or 22 depending upon http version used or trying to SSH into the server.

--- 
### NGINX

**NGINX** is a high-performance, open-source software used for **web serving**, reverse proxying, caching, load balancing, and more. It is widely known for its speed, reliability, and scalability, making it a popular choice for modern web applications.

#### Architecture of NGINX:

NGINX uses an **event-driven, asynchronous architecture**, which allows it to handle many requests simultaneously using minimal resources. This contrasts with traditional thread-based servers (like Apache), which may spawn a thread for each request.

```bash
sudo apt update
sudo apt install nginx
```

---

## Front-End Deployments on AWS


### Amazon S3 (Simple Storage Service) - Object Storage

Amazon S3 is a scalable **object storage service** for storing, managing, and retrieving unstructured data. It is designed for high durability, scalability, and availability.
##### Key Features:

1. `Data Storage`: Stores data as objects in buckets. Each object has a unique key and metadata.
2. `Durability`: Provides 99.999999999% (11 nines) durability for stored data.
3. `Scalability`: Handles petabytes of data.
4. `Access Control`:Supports fine-grained permissions and policies.
5. `Use Cases`: Backups, media storage, big data analytics, static website hosting.

---
### Amazon Cloudfront - CDN

Amazon Cloudfront is a content delivery network(CDN) which is used for caching data at edge-network globally for reduced latency thus accelerating the content delivery.

##### Key Features:

1. `Global Coverage`: Operates through a network of edge locations for low-latency content delivery.
2. `Dynamic and Static Content`: Serves both cached static files and dynamic content.
3. `Custom Rules`: Configures cache behaviors and delivery policies.
4. `Use Cases`: Accelerating websites, streaming video, and delivering APIs.

![[Pasted image 20241220191147.png]]

---

### Integration of S3 and CloudFront

When used together, S3 and CloudFront create a powerful setup:

1. `Store Origin Content in S3`: S3 acts as the origin server, hosting content like images, videos, or other assets.
2. `Deliver via CloudFront`: CloudFront caches the content stored in S3 at its edge locations, reducing latency and improving global access speed.
3. `Enhanced Performance and Security`:
    - **CloudFront reduces latency** by serving cached content from nearby edge locations.
    - S3 ensures high durability and provides a secure storage backend.

---

### Differences between S3 and CloudFront

| **Aspect**        | **Amazon S3**                          | **Amazon CloudFront**                |
| ----------------- | -------------------------------------- | ------------------------------------ |
| **Purpose**       | Long-term object storage               | Fast content delivery                |
| **Data Handling** | Stores unstructured data               | Caches and distributes data globally |
| **Access Point**  | Accessed via bucket URLs or APIs       | Accessed through distribution URLs   |
| **Performance**   | Focused on durability and availability | Focused on speed and low latency     |
| **Use Cases**     | Data storage, backup, hosting          | Website acceleration, streaming      |

---

1. For frontends, mp4 files, images, `Object stores` + `CDNs` are a better approach.
2. You can’t use the same for backends, since every request returns a different response. Caching doesn’t make any sense there.

>💡 You can use edge networks for backends (deploy your backend on various servers on the internet) but data can’t be cached in there.

---
### Step 1. 

#### Build you React project - 

```bash 

cd /link/to/your/react/project
npm run build
npm i -g serve
serve

```


> This approach will not work for frameworks that use Server side rendering (like Next.js) This will work for basic React apps, HTML/CSS/JS apps.

---
### Step 2. 

In AWS, S3 is their object store offering.
- You can create a `bucket` in there. A `bucket` represents a logical place where you store all the files of a certain project.
- Upload the files to the S3 bucket.

> Your S3 bucket should be blocked by default, and you should allow cloudfront (CDN) to access it.

---
### Step 3.

1. Create a cloudfront distribution.
2. Select your S3 bucket as a source.

>Origin Access Control (OAC) is a feature in Cloudfront, which allows you to restrict direct access to the content stored in your origin, such as an Amazon S3 bucket or a web server, ensuring that users can only access the content through the CDN distribution and not by directly accessing the origin URL.

---

### Step 4. 

##### Connect to your own domain -

1. Select edit on the root page.
2. Attach a domain name to the distribution.
3. Create a certificate. Since we want our website to be hosted on HTTPS, we should request a certificate for our domain

![[Pasted image 20241220192936.png]]

![[Pasted image 20241220192946.png]]

4. Add a CNAME record for the website to point to your cloudfront URL

---
### Error Pages 

You will notice a problem, whenever you try to access a route on your page that isn’t the index route (/user/1) , you reach an error page.This is because cloudfront is looking for a file `/user/1`in your S3, which doesn’t exist.

To make sure that all requests reach `index.html`, add an `error page` that points to `index.html`

![[Pasted image 20241220193201.png]]

> You might have to invalidate cache to see this in action.

---


