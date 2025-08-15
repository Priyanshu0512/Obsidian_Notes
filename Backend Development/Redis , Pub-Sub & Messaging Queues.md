
## Redis 

Redis (Remote Dictionary Server) is an **in-memory, key-value data store** widely used as a **database**, **cache**, and **message broker**. Redis is commonly employed in systems requiring low-latency data access and efficient data manipulation.

### **Key Features of Redis**

1. **In-Memory Storage**:
    - Stores data in memory, ensuring extremely low latency.
    - Optionally persists data to disk for recovery.
2. **Data Structures**:
    - Supports rich data types beyond simple key-value pairs:
        - **Strings**: Basic text or binary data.
        - **Lists**: Ordered collections.
        - **Sets**: Unordered collections with unique elements.
        - **Sorted Sets**: Sets with a score for ordering.
        - **Hashes**: Key-value pairs within a single key.
        - **Streams**: Log-like data structure for event-driven architectures.
        - **Bitmaps** and **HyperLogLogs**: Special-purpose data types.
3. **Performance**:
    - Handles millions of read/write operations per second.
    - Ideal for real-time applications like gaming, finance, or chat systems.
4. **Persistence**:
    - Offers two persistence mechanisms:
        - **RDB (Redis Database Backup)**: Periodic snapshots of data.
        - **AOF (Append-Only File)**: Logs every write operation.
5. **Pub/Sub Messaging**:
    - Allows publish/subscribe messaging for real-time notifications.

---

### In memory data structure store

Very similar to a DB, only it is in memory. That doesn’t mean it doesn’t have persistence

#### RDB (Redis Database File ) - 
RDB is a binary snapshot of the Redis dataset stored at a specific point in time. It is created using the `SAVE` or `BGSAVE` commands. Redis creates a point-in-time snapshot of all the data and writes it to a binary `.rdb` file.

- **`SAVE`**: Creates the snapshot synchronously (blocks Redis while saving).
- **`BGSAVE`**: Creates the snapshot asynchronously (forks a child process to save the data).
##### Advantages of RDB
- **Compact and Efficient**: The `.rdb` file is highly optimized and compact, consuming less disk space.
- **Faster Restarts**: RDB files are quicker to load during startup compared to AOF.
- **Resilience Against Corruption**: RDB files are static and less prone to corruption.

##### Disadvantages of RDB
- **Data Loss Risk**: Data added or modified after the last snapshot will be lost if Redis crashes.
- **Time-Consuming**: Creating snapshots can be resource-intensive for large datasets.

```redis 

save 900 1       # Save the dataset every 900 seconds if at least 1 key changed
save 300 10      # Save the dataset every 300 seconds if at least 10 keys changed
save 60 10000    # Save the dataset every 60 seconds if at least 10000 keys changed

```

---
#### **AOF (Append Only File)

AOF logs every write operation received by Redis. Unlike RDB, it is not a snapshot but a complete history of commands that can be replayed to reconstruct the dataset.

- **`BGREWRITEAOF`**: Optimizes the AOF file by rewriting it with the minimal set of commands required to recreate the current dataset.

##### Configuration for AOF

In `redis.conf`, you can enable and configure AOF:

```text 

appendonly yes           # Enable AOF persistence.
appendfilename "appendonly.aof" # AOF file name.
appendfsync everysec     # Sync AOF file to disk every second.
# Other options:
# appendfsync always     # Sync after every write operation (slow but safest).
# appendfsync no         # Rely on OS for syncing (fastest but risky).

```

#####  AOF Rewrite
- Over time, AOF files grow as commands accumulate. The `BGREWRITEAOF` command compacts the AOF file by consolidating commands into a minimal set to reproduce the current dataset.
---
### **General Commands**

|Command|Description|Example|
|---|---|---|
|`PING`|Tests the connection. Returns `PONG`.|`PING` → `PONG`|
|`ECHO`|Echoes a message back.|`ECHO "Hello, Redis!"`|
|`SELECT`|Switches to a different database (0–15 by default).|`SELECT 1`|
|`DBSIZE`|Returns the number of keys in the selected database.|`DBSIZE`|
|`FLUSHDB`|Deletes all keys in the current database.|`FLUSHDB`|
|`FLUSHALL`|Deletes all keys in all databases.|`FLUSHALL`|

---
### **String Commands**

| Command    | Description                           | Example                |
| ---------- | ------------------------------------- | ---------------------- |
| `SET`      | Sets a key to a string value.         | `SET name "Alice"`     |
| `GET`      | Gets the value of a key.              | `GET name` → `"Alice"` |
| `INCR`     | Increments a numeric value by 1.      | `INCR counter`         |
| `DECR`     | Decrements a numeric value by 1.      | `DECR counter`         |
| `APPEND`   | Appends a value to a string.          | `APPEND name " Smith"` |
| `GETRANGE` | Gets a substring of a string.         | `GETRANGE key 0 4`     |
| `SETEX`    | Sets a key with a time-to-live (TTL). | `SETEX key 60 "value"` |

---
### **List Commands**

| Command  | Description                                      | Example               |
| -------- | ------------------------------------------------ | --------------------- |
| `LPUSH`  | Adds an element to the start of a list.          | `LPUSH mylist "item"` |
| `RPUSH`  | Adds an element to the end of a list.            | `RPUSH mylist "item"` |
| `LPOP`   | Removes and returns the first element of a list. | `LPOP mylist`         |
| `RPOP`   | Removes and returns the last element of a list.  | `RPOP mylist`         |
| `LRANGE` | Gets elements from a list.                       | `LRANGE mylist 0 -1`  |
| `LLEN`   | Returns the length of a list.                    | `LLEN mylist`         |
|          |                                                  |                       |
The `BRPOP` command in Redis is a blocking list operation. It is used to remove and return the last element from a list. If the list is empty, it blocks the connection until an element is added or a timeout is reached.
##### Behavior
- If the list is not empty, `BRPOP` immediately removes and returns the last element of the list.
- If the list is empty, it waits for an element to be pushed into the list or until the timeout expires.
- If multiple keys are provided, `BRPOP` checks them in order and returns the first non-empty list's last element.
- If the timeout expires and no elements are available, it returns `nil`.

---

### **Set Commands**

|Command|Description|Example|
|---|---|---|
|`SADD`|Adds a member to a set.|`SADD myset "value"`|
|`SREM`|Removes a member from a set.|`SREM myset "value"`|
|`SMEMBERS`|Returns all members of a set.|`SMEMBERS myset`|
|`SISMEMBER`|Checks if a value is a member of a set.|`SISMEMBER myset "value"`|
|`SCARD`|Gets the number of members in a set.|`SCARD myset`|
|`SUNION`|Returns the union of multiple sets.|`SUNION set1 set2`|

---
### **Hash Commands**

A **Hash** in Redis is a data structure that maps fields to values, similar to a dictionary or hashmap. Hashes are ideal for representing objects or storing related information in one key.

|Command|Description|Example|
|---|---|---|
|`HSET`|Sets a field in a hash.|`HSET user name "Alice"`|
|`HGET`|Gets the value of a field in a hash.|`HGET user name`|
|`HDEL`|Deletes one or more fields in a hash.|`HDEL user name age`|
|`HGETALL`|Gets all fields and values in a hash.|`HGETALL user`|
|`HLEN`|Gets the number of fields in a hash.|`HLEN user`|
|`HMSET`|Sets multiple fields in a hash.|`HMSET user name "Alice"`|

```redis 

HSET user:1001 name "Alice" age 30
HGET user:1001 name
HGETALL user:1001
HINCRBY user:1001 age 1 // increases age by 1

```

---
### **Sorted Set Commands**

A **Sorted Set** in Redis is a collection of unique strings, each associated with a score (a floating-point number). The elements in the sorted set are ordered by their scores. This makes it ideal for scenarios where ordering is required, like leaderboards or rankings.

|Command|Description|Example|
|---|---|---|
|`ZADD`|Adds a member with a score to a sorted set.|`ZADD leaderboard 100 "Bob"`|
|`ZRANGE`|Gets members by rank (inclusive).|`ZRANGE leaderboard 0 -1`|
|`ZREM`|Removes a member from a sorted set.|`ZREM leaderboard "Bob"`|
|`ZRANK`|Gets the rank of a member in a sorted set.|`ZRANK leaderboard "Bob"`|
|`ZCOUNT`|Counts members with scores in a range.|`ZCOUNT leaderboard 0 100`|
|`ZSCORE`|Gets the score of a member.|`ZSCORE leaderboard "Bob"`|

---
### **Pub/Sub Commands**

|Command|Description|Example|
|---|---|---|
|`PUBLISH`|Publishes a message to a channel.|`PUBLISH channel "message"`|
|`SUBSCRIBE`|Subscribes to a channel.|`SUBSCRIBE channel`|
|`UNSUBSCRIBE`|Unsubscribes from a channel.|`UNSUBSCRIBE channel`|

---
### **Key Management Commands**

|Command|Description|Example|
|---|---|---|
|`EXPIRE`|Sets a TTL for a key in seconds.|`EXPIRE key 60`|
|`TTL`|Gets the remaining TTL for a key.|`TTL key`|
|`DEL`|Deletes a key.|`DEL key`|
|`EXISTS`|Checks if a key exists.|`EXISTS key`|
|`RENAME`|Renames a key.|`RENAME oldkey newkey`|
|`TYPE`|Returns the data type of a key.|`TYPE key`|
 **Command Syntax**  - `TTL key`
 
  **Return Values**
- **Positive Number**: The remaining time-to-live in seconds for the key.
- **-1**: The key exists but does not have an associated expiration time.
- **-2**: The key does not exist.


---
### **Transaction Commands**

|Command|Description|Example|
|---|---|---|
|`MULTI`|Starts a transaction.|`MULTI`|
|`EXEC`|Executes a transaction.|`EXEC`|
|`DISCARD`|Discards a transaction.|`DISCARD`|
|`WATCH`|Watches a key for changes.|`WATCH key`|
|`UNWATCH`|Unwatches all keys.|`UNWATCH`|
**Using `WATCH`**- ```
``` text
WATCH mykey 
MULTI 
SET mykey "newvalue"
EXEC
``` 

- If `mykey` is modified by another client between `WATCH` and `EXEC`, the transaction is aborted.

---
### **Server Management Commands**

|Command|Description|Example|
|---|---|---|
|`INFO`|Returns server statistics.|`INFO`|
|`CONFIG GET`|Gets server configuration.|`CONFIG GET maxmemory`|
|`CONFIG SET`|Sets server configuration.|`CONFIG SET maxmemory 100mb`|
|`SAVE`|Saves data to disk.|`SAVE`|
|`SHUTDOWN`|Stops the Redis server.|`SHUTDOWN`|

---

## Implementation

### Using Express 

Backend 
```typescript 

const app = express();
app.use(express.json());
const client = createClient();

app.post("/submit", async (req, res) => {
  const { name, address, id } = req.body;

  try {
    await client.lPush("details", JSON.stringify({ name, address, id }));
    res.status(200).json({ message: "Data added successfully" });
  } catch (error) {
    res.status(500).json({ message: "Failed to add data" });
    console.log(error);
  }
});

async function createServer() {
  try {
    await client.connect();
    app.listen(3000, () => {
      console.log("Server is running on port 3000");
    });
  } catch (error) {
    console.log("Failed to connect to redis server.");
  }
}

```

Worker 

```typescript 

async function submit(submission: string) {
  const { name, address, id } = JSON.parse(submission);
  console.log(name);
  console.log(address);
  console.log(id);

  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log("Finished processing data");
}

async function startWorker() {
  try {
    await client.connect();
    console.log("Connected to redis server");
    try {
      while (true) {
        const submission = await client.brPop("details", 0);
        if (submission) {
          await submit(submission.element);
        }
        console.log("Done");
      }
    } catch (error) {
      console.log("Failed to pop data." + error);
    }
  } catch (error) {
    console.log("Failed to connect to redis server.");
  }
}

startWorker();

```

---

# Pub subs

Publish-subscribe (pub-sub) is a messaging pattern where messages are published to a topic without the knowledge of what or if any subscribers there might be. Similarly, subscribers listen for messages on topics of interest without knowing which publishers are sending them. This decoupling of publishers and subscribers allows for highly scalable and flexible communication systems.

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2F7f446917-e063-4a1c-8d16-632cc6fca0a2%2FScreenshot_2024-04-07_at_5.26.51_PM.png?table=block&id=e81e64d8-32c3-40a8-b791-450a5465629b&cache=v2)

---

## Implementation of Pub-Sub using Singleton Pattern


```typescript

import { connect } from "mongoose";
import { createClient, RedisClientType } from "redis";

export class PubSubManager {
  private static instance: PubSubManager;
  private client: RedisClientType;
  private subscriptions: Map<string, string[]>;
  private constructor() {
    this.client = createClient();
    this.client.connect();
    this.subscriptions = new Map();
  }

  public static getInstance() {
    if (this.instance) {
      return this.instance;
    }
    return (this.instance = new PubSubManager());
  }

  public subscribe(userId: string, stock: string) {
    if (!this.subscriptions.has(stock)) {
      this.subscriptions.set(stock, []);
    }
    this.subscriptions.get(stock)?.push(userId);

    if (this.subscriptions.get(stock)?.length == 1) {
      this.client.subscribe(stock, (message) => {
        this.handleMessages(stock, message);
      });
    }
    console.log(`Subcribed to redis channel ${stock}`);
  }

  public unsubscribe(userId: string, stock: string) {
    this.subscriptions.set(
      stock,
      this.subscriptions.get(stock)?.filter((id) => id !== userId) || []
    );
    if (this.subscriptions.get(stock)?.length === 0) {
      this.client.unsubscribe(stock);
    }
    console.log(`Unsubscribed from redis channel ${stock}`);
  }

  private handleMessages(stock: string, message: string) {
    console.log(`message received on channel ${stock}: ${message}`);
    this.subscriptions.get(stock)?.forEach((userId) => {
      console.log(`Sending message to user ${userId}`);
    });
  }

  public async disconnnect() {
    await this.client.quit();
  }
}

```

index.ts 
```typescript

setInterval(() => {
  PubSubManager.getInstance().subscribe(Math.random().toString(), "APPL");
}, 5000);

```

---


