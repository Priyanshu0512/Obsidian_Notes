
---
### **Stateless Backends**

A **stateless backend** does not retain any information about client interactions between requests. Each request from the client contains all the information needed to process it, and the server treats every request as independent and unrelated to previous ones.

#### Characteristics:

1. **No Session Memory**:
    - The server does not remember the state of the client between requests.
2. **Idempotency**:
    - Each request produces the same result, regardless of when or how many times it is made (e.g., retrieving the same resource).
3. **Simplified Scalability**:
    - Stateless servers can handle requests independently, making it easy to scale horizontally (adding more servers).
4. **Fault Tolerance**:
    - A failure of one server does not affect others since no session information is stored locally.

---

### Stateless and Stateful Backends

In software architecture, **stateless** and **stateful** describe how a backend server manages client interactions and maintains state (information about client sessions). Understanding the distinction is crucial for designing scalable, efficient, and resilient systems.

---
### **Stateful Backends**

A **stateful backend** retains information about the client and their interactions across multiple requests. The server maintains a session for each client, tracking state information like authentication, user preferences, or the progress of a transaction.

#### Characteristics:

1. **Session Management**:
    - The server uses mechanisms like cookies, tokens, or server-side session storage to maintain client state.
2. **Dependency on State**:
    - Some operations depend on previously stored information, such as shopping cart contents in an e-commerce application.
3. **Complex Scalability**:
    - Scaling requires sharing session state across servers, often using databases, distributed caches (e.g., Redis), or sticky sessions.
4. **Session Recovery Challenges**:
    - If a server fails, the state must be recovered, which adds complexity.

---

## Stickiness

Making sure that the user who is interested in a `specific` room, gets connected to a `specific` server.

![notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F085e8ad8-528e-47d7-8922-a23dc4016453%2Feee8417d-18e0-4f07-ad52-59605fc5c182%2FScreenshot_2024-04-21_at_4.41.59_PM.png?table=block&id=9afa1fd2-29e8-45bd-8614-ec7a7e3268ef&cache=v2)

---
### Singleton Pattern: A Detailed Explanation

The **Singleton Pattern** is a design pattern used in software development to ensure that a class has only **one instance** throughout the application's lifecycle. It provides a global point of access to this instance while maintaining strict control over its instantiation.

### **Key Characteristics of the Singleton Pattern**

1. **Single Instance**:
    - Only one instance of the class is created, and it is shared across the application.
2. **Global Access**:
    - Provides a single point of access to the instance.
3. **Controlled Instantiation**:
    - The class controls the creation of its own instance, often using private constructors.
4. **Thread Safety**:
    - Ensures the Singleton works correctly in a multi-threaded environment, preventing multiple instances from being created.


> Note - In a multi-threaded environment, the Singleton pattern faces challenges in ensuring that only **one instance** of the Singleton class is created, even when multiple threads attempt to create an instance simultaneously.
	1. **Thread-Safety**:
	2. **Performance Overheads**:
	3. **Race-condition**: 


---

## Static Keyword 

In JavaScript, the `static` keyword is used to define methods or properties on a class that are associated with the **class itself** rather than any instance of the class. These are called **static methods** or **static properties**, and they cannot be accessed through instances of the class—only directly via the class. 
##### 1. Static Methods
- Static methods are defined with the `static` keyword and are typically used to perform operations that don't depend on instance properties.
##### 2. Static Properties
- Static properties are used to define class-level variables. These are also accessed directly through the class.

##### Limitations of `static`

1. **No Access to Instance Data**:
    - Static methods cannot access `this` referring to instance properties or methods since they are not tied to an instance.
2. **Instance Methods and Properties**:
	- Instances of the class cannot directly use static methods or properties.

###### Inheritance with `static`

Static methods and properties are inherited by subclasses and can be overridden.

```js
class Parent {
    static greet() {
        return "Hello from Parent!";
    }
}

class Child extends Parent {
    static greet() {
        return "Hello from Child!";
    }
}

console.log(Parent.greet()); // Output: "Hello from Parent!"
console.log(Child.greet());  // Output: "Hello from Child!"

```

---

## Implementation of Singleton Pattern

Game-Manager Class - 

```typescript

interface Game {
  id: string;
  whitePlayerName: string;
  blackPlayerName: string;
  moves: string[];
}

export class GameManager {
  private static instance: GameManager;
  private games: Game[];

  private constructor() {
    this.games = [];
  }

  public static getInstance(): GameManager {
    if (this.instance) {
      return this.instance;
    }
    return (this.instance = new GameManager());
  }
  public addGame(game: Game) {
    this.games.push(game);
  }
  public getGame(gameId: string) {
    return this.games.find((game) => game.id === gameId);
  }
  public getGames() {
    return this.games;
  }

  public addMove(gameId: string, move: string) {
    this.games.find((game) => game.id === gameId)?.moves.push(move);
  }

  public logstate() {
    console.log(this.games);
  }
}
```

Logger function 

```typescript 

import { GameManager } from "./store";
export function Logger() {
  setInterval(() => {
    console.log(GameManager.getInstance().logstate());
  }, 5000);
}

```


Index.ts

```typescript

import { GameManager } from "./store";
import { Logger } from "./logger";
import { PubSubManager } from "./pubsubManager";

Logger();

setInterval(() => {
  const gameManeger = GameManager.getInstance();
  gameManeger.addGame({
    id: Math.random().toString(),
    whitePlayerName: "Alice",
    blackPlayerName: "Bob",
    moves: [],
  });
}, 5000);

```


---
