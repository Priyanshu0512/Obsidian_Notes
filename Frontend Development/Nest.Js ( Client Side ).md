
`Next.Js` was introduced due to minor inconveniences in React which are as follows - 

- In React projects  a separate backend directory needs to be maintained.
- React does not provide out of the box routing.
- React is not `SEO` optimized.
- Water-falling Problem.

---

## SEO Optimization

Google/Bing has a bunch of `crawlers` that hit websites and figure out what the website does.
It ranks it on `Google` based on the HTML it gets back.The crawlers `DONT` usually run your JS and render your page to see the final output.

>  While Google-bot can run JavaScript, `dynamically generated` content is harder for the scraper to index

When the website loads initially its HTML markup is almost empty and hence crawlers are not able to detect the website content.

---

## Water-falling Problem

The "waterfalling problem" in React, and more broadly in web development, refers to a scenario where data fetching operations are chained or dependent on each other in a way that leads to inefficient loading behavior.

![[Pasted image 20241228185646.png]]

1. Fetching the index.html from the CDN
2. Fetching script.js from CDN
3. Checking if user is logged in (if not, redirect them to /login page)
4. Fetching the actual blogs
There are 4 round trips that happen one after the other (sequentially). 

#### How Next.Js tackles this problem!!

![[Pasted image 20241228185815.png]]

#### 1. Concurrent Data Fetching

- In Next.js, functions like `getServerSideProps`, `getStaticProps`, and `getInitialProps` can be used to fetch data **before rendering the page**.
- Data fetching in these functions is performed **concurrently**, not sequentially, ensuring multiple requests are resolved simultaneously, reducing latency.

#### 2. Parallel and Streaming Rendering (React 18 Features)

- Next.js supports **React Server Components** and **streaming** features introduced in React 18.
- These features allow parts of a page to render and stream incrementally as data becomes available, rather than waiting for all data to be fetched.

**How It Helps:**
- Water-falling delays are minimized because rendering starts as soon as the required data for some parts of the page is ready.

#### 3. Static Site Generation (SSG) with `getStaticProps`

- For static pages, Next.js fetches data at **build time** using `getStaticProps`. This avoids any runtime delays because the data is already baked into the HTML during the build process.

**Benefit:**
- This approach completely bypasses runtime waterfalls, as no additional data-fetching calls are required on the client or server.

#### 4. Data Fetching at Component Level

- In Next.js apps, components can fetch their own data using hooks like `useSWR` (from the `swr` library) or custom React hooks.
- SWR (Stale-While-Revalidate) allows concurrent fetching and caching of data, so multiple components fetching data don’t block each other.
---

# Next.js offerings

Next.js provides you the following `upsides` over React

1. `Server side rendering` - Get’s rid of SEO problems
2. `API routes` - Single codebase with frontend and backend
3. File based routing (no need for react-router-dom)
4. Bundle size optimizations, Static site generation
5. Maintained by the Vercel team

### Downsides -
1. Can’t be distributed via a CDN, always needs a server running that does `server side rendering` and hence is expensive
2. Very opinionated, very hard to move out of it

---

**Creating a Next.Js project** - 

```bash 
npx create-next-app@latest
```

---
## Routing 

Lets take a step backward and explore the file structure in a NEXT.Js app

- `app.tsx` - This file is the main file where all the functions required for the rendering the page is written or is exported to.
- `layout.tsx` - Layouts let you `wrap` all child `pages` inside some logic. This file contains all the layouts for the page which remains same across different pages.
- `loading.tsx` - This is file which contains the loading logic which data is being rendered on to the page from the server (fetch from the server and hydrated on to the HTML page).


Next.js uses **file-system based routing**, meaning you can use folders and files to define routes.What this means is that folder are nested in and they become the routes.

A nested route is a route composed of multiple URL segments. For example, the `/blog/[slug]` route is composed of three segments:
- `/` (Root Segment)
- `blog` (Segment)
- `[slug]` (Leaf Segment)

> Merging Routes - In order to merge routes enclose the routes to merged inside the folder wrapped inside `()`. This route which be ignored but will be used to merge further nested routes to go through it.

More about various routing at- [Routing](https://nextjs.org/docs/app/building-your-application/routing/route-groups)

---

### Client and Server side components - 

NextJS expects you to identify all your components as either `client` or `server`

As the name suggests
1. Server components are rendered on the server
2. Client components are `pre-rendered` and are pushed to the client to be rendered again

By default, all components are `server` components.
If you wan’t to mark a component as a `client` component, you need to add the following to the top of the component -

```javascript
"use client"
```

##### Client side components 

Client-side components are rendered and hydrated in the browser. They enable dynamic interactivity and are essential for features that require client-side state management or access to browser APIs.

#### Key Features:
1. **Dynamic Interactivity:**
    - React on the client handles interactions like button clicks, animations, and other UI updates without requiring a page reload.
2. **Browser-Specific APIs:**
    - Client-side components can access APIs like `window`, `document`, `localStorage`, and `navigator`.
3. **State Management:**
    - These components can use hooks like `useState`, `useEffect`, and `useContext` for managing state and side effects.
4. **Hydration:**
    - After the server sends the HTML to the browser, the React library attaches event listeners and rehydrates the component to make it interactive.
#### Use Cases:
- **Interactive Components:**
    - Modals, dropdowns, carousels, and client-driven forms.
- **Browser-Specific Logic:**
    - Components that depend on `window` or `document` (e.g., geolocation, localStorage access).
- **Real-Time Updates:**
    - Components with live updates, such as chat applications or stock tickers.


### Server-Side Components

Server-side components are rendered on the server, and the resulting HTML is sent to the browser. These components are static by default but can be hydrated on the client if needed.
#### Key Features:

1. **Pre-Rendering:**
    - Content is rendered on the server, improving initial page load speed and SEO performance.
    - Two types of pre-rendering:
        - **Static Rendering (SSG):** Generated at build time.
        - **Dynamic Rendering (SSR):** Generated on every request.
2. **No Browser-Specific Logic:**
    - Server-side components do not run in the browser, so they cannot access browser-specific APIs (`window`, `document`).
3. **Better Performance:**
    - Rendering on the server offloads computation from the client, reducing the work required in the browser.
4. **Data Fetching:**
    - These components can use `getServerSideProps`, `getStaticProps`, or `getInitialProps` to fetch data at the server level.

#### Use Cases:
- **SEO-Optimized Pages:**
    - Blog posts, product pages, or landing pages where metadata and content must be crawlable.
- **Content with External Data:**
    - Fetching and displaying data from APIs, databases, or CMSs.
- **Reducing Client Load:**
    - Offloading rendering for better performance on slower devices.

>Rule of thumb is to defer the client as much as possible

---

