
**Connection pooling** refers to the practice of maintaining a cache of database connection objects that can be reused by multiple clients. Instead of opening and closing a new connection for each user request, a connection pool allows a set of connections to be shared among requesting threads or processes. When a new request comes in, it can borrow a connection from the pool, use it for the database operation, and then return it to the pool for future use.

>Serverless environments, such as Cloudflare Workers, present unique challenges for database connectivity. Since serverless functions can scale up rapidly and run in multiple regions, they can potentially open a large number of connections to the database. This can quickly exhaust the database's connection limit and degrade performance.


![[Pasted image 20241228175515.png]]

---

## Connection Pooling in Prisma 

- Prisma Accelerate is a service that enhances Prisma's capabilities in serverless deployments, such as those on Cloudflare Workers.

#### Steps to setup connection pooling with Prisma Accelerate 


```bash
npm install prisma 
npx prisma init 
```

1. Create a basic schema.
2. Migrate the Schema 

```bash 

npx primsa migrate --name <name-of-migration>

```

3. Sign-up to prisma accelerate to generate the API key for pooling database address.
4. Replace the `DATABASE_URL` in the `.env` file with the API key.
5. Add the Accelerate Dependency and and generate the prisma client `without engine`.

```bash 

npm install @prisma/extension-accelerate
npx prisma generate --no-engine

```

---

## The `Wrangler.toml` file

Here's how the `wrangler.toml` file relates to the setup:

- **Project Configuration**: The `wrangler.toml` file contains various configuration options for your Cloudflare Workers project, such as the account ID, project name, and environment variables.
- **Environment Variables**: You can define environment variables in the `wrangler.toml` file, which might include the `DATABASE_URL` for Prisma. This URL would be the connection string provided by Prisma Accelerate, which includes the API key and other necessary parameters for connection pooling.
- **Workers Script Settings**: The file also includes settings related to the Workers script itself, such as the entry point for the application code and any build commands that need to be run before deployment.
- **Dependencies**: If your Worker uses npm packages, such as `@prisma/client` and `@prisma/extension-accelerate`, you may need to specify how these dependencies are bundled with your Worker script.
- **Routes and Triggers**: The `wrangler.toml` file can also define routes and triggers that determine when your Worker is executed in response to HTTP requests.

--- 
## `.env` vs `wrangler.toml` files 

> In a server-less deployment using cloudflare workers the all the environment variables are loaded from the `wrangler.toml`  file hence it becomes important to know which where to load which environment variable.


- In the `schema.prisma` file the env variable should be loaded from the `.env` file which contains the `DATABASE_URL` of the actual database hence when schema are generated that connection is needed to the actual database.

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```


- While in the backend when request are received from the frontend to perform operations on the user data there the `DATABASE_URL` should be loaded from the `wrangler.toml` as here actual request are coming from the user which need to pooled through the pooling database.

```ts

const app = new Hono<{
  Bindings: {
    DATABASE_URL: string;
    JWT_SECRET: string;
  };
}>();

const prisma = new PrismaClient({
      datasourceUrl: DATABASE_URL,
  }).$extends(withAccelerate())
  
```

> Note - In Hono, it does not know the type of environment variables being loaded hence their types need to be  specified as shown above.

---
