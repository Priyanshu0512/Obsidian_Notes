**Client**  - Any end system that initiates or generates a request or the end-systems which want to perform a operation by requesting for something.
Note - It is not necessary that a client always have some UI.
**Server** - Any end-system or a process running on a system which can receive a request, process it and sends back some data as a response to the client.

**API** - Application Programming Interface. They are like contracts which expect a certain input format and the return the data in specify manner depending upon the API being used. 
     API calls can be over internet using HTTP request where data is fetched to the local machine or it can be  function call to some already installed library on to the system to get some data.Both are API calls.

**Difference Between Framework and Library**
**Library** - It is some specific piece code which provides some functionality to the user. Ex - React.js is an library as it has a specific functionality.
**Framework** - It is a collection of various libraries clubbed together to provide the facility of performing a variety of task just by using the in-built functions only. Ex - Angular.js 

**REST** -Rest is Representational State Transfer.Rest is basically a set of guidelines to drive the architecture of the web.It is not a compulsion to write according to these guidelines as it is just a set of guidelines and not a protocol. API written following the rest guidelines are called RESTful APIs.
Other set of guidelines are SOAP,gRPC and GraphQL.

# REST Guidelines 

1. It prefers that client server interaction to occur of HTTP.(Though a specific version of HTTP has not being specified.)
2. It prefers that JSON as the mode of data transfer over the network.(JSON - Javascript Object Notation)
3. It also gives the guidelines about how the URL's should look like.
    In Rest the main source of info is called as Resource(Example - Liking a tweet,) whereas as commenting on a tweet is considered an action.
    Resources - NOUN
    Actions - Verb
    Now the URL's should always end with a NOUN not VERB.
    In addition to that the NOUNs are expected to be plural.
    Note - In order to now differentiate between URL's pointing to the same page(NOUN) but doing different actions like commenting or liking, REST recommends that every network call should be defined with a HTTP method like (Put , Fetch, Patch) to signify about the action being done.
    GET - retrieve data
    POST - Sending data or Creating a resources
    PATCH - Partial changes to the resources.
    PUT - update a resource
    DELETE - deleting a resource
    Info about these tasks are sent in the request body of the HTTP request.
    Also more than three level of nesting the URL's is not suggested.
4. It expects the response to have HTTP codes.
5. Statelessness- It expects the request from the client to the server must contain all the information request to process and complete the request.
6. Layered System - It expects the systems to have a hierarchical order of layers of components wherein one layer should not be able to look beyond one layer which which it is interacting.
More Info of [restfulapi.net].

Sending data can be done in three ways - 
1. **Request Body**
2. **URL Params** - Ex - /blogs/2/comments/3 Here the data is being sent through the means of the URL only .Like here in a GET request you want the 3 comment of 2nd page of a blog.
3. **Query params** - Ex - /products ? category = electronics & company=apple. This a query param in form of key value pairs assigned with = sign and keys separated by a & symbol.

**CRUD APIs** - CRUD stands for create, read, update and delete.
An api which supports all these function along more are called CRUD APIs.
