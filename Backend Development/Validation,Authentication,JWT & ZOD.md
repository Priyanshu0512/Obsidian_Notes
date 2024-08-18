
# ZOD 

ZOD is  a TypeScript-first schema validation with static type inference.

```js
const zod=require("zod");

const schema= zod.array(zod.number()); //Defining the markup of schema.

const app = express();
app.use(express.json());

app.get('/health', function (req, res) {
  const kidneys=req.body.kidneys;
  const len=kidneys.length;
  const response= schema.safeParse(kidneys) // Schema validation
  res.status(200).json({
    msg: "Request Successful",
    len: len,
    res: response
  });
  
});
```

Difference between parse and safeParse - 

 - `safeParse `- It does not throw an error upon schema invalidation but gives the details about the error in the response object only.
 - `parse` - It throws an error object upon schema invalidation and returns back the error object which can further be used to display relevant error message.

```js
const schema= zod.object({
  user: zod.string(),
  kidneys: zod.array(zod.number()),
  country: zod.literal("US").or(zod.literal("IND"))
}); // A basic validation schema template.
```


##### Difference between Authentication & Authorisation

- `Authentication` - It is process of validating a user and its credentials.
- `Authorisation` - It is referred to as giving user access to certain functionalities within the system upon Authentication.

### Encryption & Hashing 
- `Encryption` - Encrypted data can be decrypted by using an encryption key.A string is encrypted by a password and can be decrypted provided it has the password.
- `Hashing` - It is a one way process wherein the Hashed data cannot be used to recover that original data. Though hashing of the same data will result in same hashed data every-time.


###  JWT (Json Web Tokens)
- It is neither hashing nor encryption but a digital signature.
- Anyone can see the original data given the digital signature but the signature can only be verified using the JWT password.
Note- Data can be viewed by anyone if they have access to the JWT token but it can only be verified by the platform which has the specific password which was used to create the JWT token in the first place.

### Authentication

- Authentication can be implemented by **JWT** ( JSON Web Tokens) etc.
- **Steps involving User Authentication**

  1.  In the process of authenticating a user, user sends its credentials to the server wherein firstly the request in validated in the middleware's for valid user and password.
  2.  If the request is reject then a response object is send back to the client.
  3.  Upon Successful validation of the request a JWT token is generated and send back to the user where it needs to be stored in form of **cookies Headers** etc.
  4.  Now when the user tries to sign-in again it sends its credentials along with the JWT token in request headers. (**x-access-token** etc).This token is also known as a `Bearer Token`.
  5.  Now the controllers/middleware's firstly check for the presence of JWT token in the request. If present they check for its validity. If found valid the request is forwarded to the service layer else the request is rejected and Error response object is send back the client.

  (Note - JWT token validation can be done either in middleware or in service layer.)

Also depending upon the use case JWT can be made to expire.Example - a Banking system would expire a token every 5 minutes but a Shopping application might expire a token every 2 days etc.

```js
const { ALL } = require("dns");
const express = require("express");
const jwt = require("jsonwebtoken");
const jwtPassword = "123456";

const app = express();
app.use(express.json());

const ALL_USERS = [
  {
    username: "harkirat@gmail.com",
    password: "123",
    name: "harkirat singh",
  },
  {
    username: "raman@gmail.com",
    password: "123321",
    name: "Raman singh",
  },
  {
    username: "priya@gmail.com",
    password: "123321",
    name: "Priya kumari",
  },
];

function userExists(username, password) {
  return (
    ALL_USERS.find(function (obj) {
      return obj.username === username && obj.password === password;
    }) != undefined
  );
}

app.post("/signin", function (req, res) {
  const username = req.body.username;
  const password = req.body.password;

  if (!userExists(username, password)) {
    return res.status(403).json({
      msg: "User doesnt exist in our in memory db",
    });
  }

  var token = jwt.sign({ username: username }, jwtPassword);
  return res.json({
    token,
  });
});

app.get("/users", function (req, res) {
  const token = req.headers.authorization;
  let list = [];
  try {
    const decoded = jwt.verify(token, jwtPassword);
    const username = decoded.username;
    ALL_USERS.forEach(function(obj){
      if(obj.username!=username){
        list.push(obj);
      }
    });
    res.status(200).json({
      list: list
    });
  } catch (err) {
    return res.status(403).json({
      msg: "Invalid token",
    });
  }
});

app.listen(3000);

```