
The benefits of using NextJS for backend includes -

1. Code in a single repo
2. All standard things you get in a backend framework like express
3. Server components can directly talk to the backend

---

> All the backend logic resides under the `api`  folder.

``` ts

export async function GET() {
  return Response.json({ username: "harkirat", email: "harkirat@gmail.com" })
}

// backend call 
async function getUserDetails() {
  try {
    const response = await axios.get("http://localhost:3000/api/user")
	  return response.data;
  }  catch(e) {
    console.log(e);
}

Note - Not the best way to fetch data from the backend.

}```
 
`getUserDetails` runs on the server. This means you’re sending a request from a server back to the server

![[Pasted image 20250107180501.png]]

##### Better Solution 

```ts

import { PrismaClient } from "@prisma/client";

const client = new PrismaClient();

async function getUserDetails() {
  try {
    const user = await client.user.findFirst({});
	  return {
      name: user?.username,
      email: user?.username
    }
  }  catch(e) {
    console.log(e);
  }
}

export default async function Home() {
  const userData = await getUserDetails();

  return (
    <div className="flex flex-col justify-center h-screen">
        <div className="flex justify-center">
            <div className="border p-8 rounded">
                <div>
                    Name: {userData?.name}
                </div>
                
                {userData?.email}
            </div>
        </div>
    </div>
  );
}

```

> Note - Here the `Home` component is async. Next.js 14 supports async components wherein the water-falling problem is eliminated and the web-server pre-renders page before sending it to the user.

---

## Singleton Prisma Client

The **Prisma Singleton Pattern** is a commonly used design pattern for managing the lifecycle of a Prisma Client instance in a Node.js application. This pattern is crucial for avoiding issues like multiple database connections or performance bottlenecks in environments like **server-less functions** or **long-running processes**.

### Why Singleton Pattern for Prisma?

1. **Connection Pooling:**
    - Prisma manages a pool of database connections internally. Creating multiple Prisma Client instances can lead to **excessive connections** to the database, which may exceed the allowed limits, especially in production databases.
2. **Performance Optimization:**
    - Initializing the Prisma Client is an expensive operation. By reusing a single instance, you avoid the overhead of initializing a new client repeatedly.
3. **Serverless Environments:**
    - In server-less architectures (e.g., AWS Lambda, Vercel ), where the application may scale horizontally by creating multiple instances, ensuring a **single Prisma Client instance per request lifecycle** is essential to prevent overloading the database.
4. **Ease of Maintenance:**
    - A singleton pattern centralizes the Prisma Client management, making the codebase easier to maintain and debug.


#### Implementation

Create `db/index.ts`

```ts

import { PrismaClient } from '@prisma/client'

const prismaClientSingleton = () => {
  return new PrismaClient()
}

declare global {
  var prisma: undefined | ReturnType<typeof prismaClientSingleton>
}

const prisma = globalThis.prisma ?? prismaClientSingleton()

export default prisma

if (process.env.NODE_ENV !== 'production') globalThis.prisma = prisma

```


>Update import of prisma everywhere `import client from "@/db"`

--- 

## Server Actions 

Server Actions are a feature in Next.js that allow you to directly perform server-side logic within your React components. Server Actions are **functions defined in React components** that run exclusively on the server. They allow developers to:

- Handle data mutations (e.g., create, update, delete operations).
- Communicate with databases or APIs.
- Perform computationally expensive tasks securely on the server.

Unlike traditional API routes or client-side mutations, Server Actions eliminate the need for explicit HTTP requests to perform these tasks.

> 💡Under the hood, still an HTTP request would go out. But you would feel like you’re making a function call


A Server Action can be defined with the React [`"use server"`](https://react.dev/reference/react/use-server) directive. You can place the directive at the top of an `async` function to mark the function as a Server Action, or at the top of a separate file to mark all exports of that file as Server Actions.

- Server Components can use the inline function level or module level `"use server"` directive. To inline a Server Action, add `"use server"` to the top of the function body
- To call a Server Action in a Client Component, create a new file and add the `"use server"` directive at the top of it. All exported functions within the file will be marked as Server Actions that can be reused in both Client and Server Components:

#### Example - 

1. Create `actions/user.ts` file (you can create it in a different folder)

```ts
"use server"

import client from "@/db"

export async function signup(username: string, password: string) {
    // should add zod validation here
    const user = await client.user.create({
        data: {
            username: username,
            password: password
        }
    });

    console.log(user.id);

    return "Signed up!"
}
```


```ts
import { signup } from "@/actions/user";;

...

<button onClick={async () => {
    const response = await signup(username, password);
    localStorage.setItem("token", response);
    router.push("/")
}} type="button" className="mt-8 w-full text-white bg-gray-800 focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2">Sign in</button>


```


### Best Practices for Using Server Actions

1. **Encapsulate Business Logic:**
    - Keep your server-side logic modular and reusable.
2. **Handle Errors Gracefully:**
    - Use `try...catch` blocks to manage server-side errors and provide meaningful feedback to users.
3. **Avoid Overloading Components:**
    - Keep components clean by moving heavy server-side logic to dedicated action files.

---

