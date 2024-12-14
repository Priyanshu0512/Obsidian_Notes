`Server-less`  is a backend deployment in which the `cloud provider` dynamically manages the allocation and provisioning of the servers. The term `server-less` does not mean that there are no servers but that the developers and operators do not need to worry about the servers.

## Problems with this approach 

- Tend to get very expensive at scale
-  Cold start problem- As the cloud providers charge you on per request basis therefore if no request are been made and suddenly request are generated the `cloud provider` will need to spin up some servers which would initially take time and hence give a huge initial latency.

> To tackle this `warm pool` of some servers may be kept always online and then they can auto-scaled as per the request generated.

### Famous Server-less Providers

- AWS Lamda
- Google Cloud Functions
- Cloudflare Workers

### When to use a Server-less Architecture?

- It the service has a very low traffic and you want to optimize for costs.
- When you can't anticipate the traffic and don't want to worry about auto-scaling.

### How Cloudflare Workers work??

The Cloudflare Workers works similarly on the browser as well as in the Node.js environment. 
Under the hood the workers runtime uses the V8 engine.  The difference happens on the runtime. Rather than running on the individual machine, Cloudflare worker functions on  Cloudflare Edge network which is essentially a distributed system of thousands of machine globally.