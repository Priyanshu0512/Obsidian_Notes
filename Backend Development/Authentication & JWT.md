##### Difference between Authentication & Authorisation

- `Authentication` - It is process of validating a user and its credentials.
- `Authorisation` - It is referred to as giving user access to certain functionalities within the system upon Authentication.

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
