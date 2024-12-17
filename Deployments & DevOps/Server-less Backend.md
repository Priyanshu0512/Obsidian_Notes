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

### Isolates 

V8 orchestrates `isolates`. It is a lightweight contexts which provides your code with the variables it can access and a safe environment to be executed within. Instead of creating a virtual machine for each function, an isolate is created within an existing environment.

A single runtime can handle thousands of isolates, seamlessly switching between them.Each isolates memory is completely isolated from the other.Isolates are designed to start very quickly hence eliminating the cold start problem.


### Isolates vs Containers 

> Unlike other service provides which use a containerized processes of each running an instance of a language runtime, Workers pay the overhead of a javascript runtime once on a start of the container.
> Worker processes are able to run essentially limitless scripts with almost no individual overhead creating an individual isolate for each worker function call. An isolate can spin up very quickly in comparison to containers and require an order of magnitude less than them.


```typescript
export default {
	async fetch(request, env, ctx): Promise<Response> {
		if (request.method == 'GET') {
			return Response.json({
				msg: 'Get request',
			});
		} else {
			return Response.json({
				msg: ' Not a get requst.',
			});
		}
	},
} satisfies ExportedHandler<Env>;
```

In order to use the query params from the request refer to the following link. 
[[https://community.cloudflare.com/t/parse-url-query-strings-with-cloudflare-workers/90286]]

### Deployments

![[Pasted image 20241214170922.png]]

## Using Hono as a replacement for Express 

> 
> `npx create hono@latest --myapp
> 

```typescript
import { Hono } from "hono";

const app = new Hono();

app.post("/", async (c) => {
  const body = await c.req.json();
  console.log(body);
  console.log(c.req.header("Authorization"));
  console.log(c.req.query("params"));
  return c.text("Hello Hono!");
});

export default app;
```

##### Middleware Implementation
```typescript
import { Hono, Next } from 'hono'
import { Context } from 'hono/jsx';

const app = new Hono()

app.use(async (c, next) => {
  if (c.req.header("Authorization")) {
    // Do validation
    await next() // await is used if after next some computation is needed.
  } else {
    return c.text("You dont have acces");
  }
})

app.get('/', async (c) => {
  const body = await c.req.parseBody()
  console.log(body);
  console.log(c.req.header("Authorization"));
  console.log(c.req.query("param"));

  return c.json({msg: "as"})
})

export default app
```



### Some wrangler(cli for cloudflare workers ) commands 

  - `wrangler init [name]`                           📥 Initialize a basic Worker
  - `wrangler dev [script]`                        👂 Start a local server for developing your Worker
  - `wrangler deploy [script]`                   🆙 Deploy a Worker to Cloudflare  [aliases: publish]
  - `wrangler deployments`                           🚢 List and view the current and past deployments                                                                        for your Worker
  - `wrangler rollback [version-id]`       🔙 Rollback a deployment for a Worker
  - `wrangler versions`                                 🫧  List, view, upload and deploy Versions of your                                                                           Worker to Cloudflare
  - `wrangler triggers`                                  🎯 Updates the triggers of your current deployment
  - `wrangler delete [script]`                   🗑  Delete a Worker from Cloudflare
  - `wrangler tail [worker]`                       🦚 Start a log tailing session for a Worker
  - `wrangler secret`                                      🤫 Generate a secret that can be referenced in a                                                                            Worker
  - `wrangler types [path]`                          📝 Generate types from bindings and module rules                                                                        in configuration
  - `wrangler kv`                                              🗂️  Manage Workers KV Namespaces
  - `wrangler queues`                                      🇶  Manage Workers Queues
  - `wrangler r2`                                              📦 Manage R2 buckets & objects
  - `wrangler d1`                                              🗄  Manage Workers D1 databases
  - `wrangler vectorize`                                🧮 Manage Vectorize indexes [open beta]
  - `wrangler hyperdrive`                              🚀 Manage Hyperdrive databases
  - `wrangler pages`                                       ⚡️ Configure Cloudflare Pages
  - `wrangler mtls-certificate`                 🪪  Manage certificates used for mTLS connections
  - `wrangler pubsub`                                     📮 Manage Pub/Sub brokers [private beta]
  - `wrangler dispatch-namespace`             🏗️  Manage dispatch namespaces
   - `wrangler ai`                                            🤖 Manage AI models
  - `wrangler workflows`                               🔁 Manage Workflows [open-beta]
  - `wrangler login`                                       🔓 Login to Cloudflare
  - `wrangler logout`                                     🚪 Logout from Cloudflare
  - `wrangler whoami`                                     🕵️  Retrieve your user information