MVC - Model View Controller.
1. View - First point of user interaction.
2. Controller - Intermediate layer between the view and the model. Their purpose is to communicate the request from the view to the model  and back . Controller should not contain and business logic and should be thin.
3. Model layer - This layer contains all the Business logic therefore can be fat in nature. Models also interact with the databases.

Now controllers  can further be broken down into two parts- 
1. **Middleware** - Middleware is function which has access to request, response object and the next function in the application request-response cycle. Basically this next function points to the next middleware in the layers as multiple middleware can be chained. 
        Middleware are the first point of interaction from the client hence request validation etc.
2. **Controller** - The last middleware is called a controller as it finally sets the request to the model layer. It also prepares the response structure and sends it back to the middleware which in turn sent it back to the client.
3. **Routes** - It registers the middleware's and the controller.In routes we write our routes and write the logic of which middleware and controller needs to be called for a specific routes. Middleware and controller can imported using modules.

**Breaking Up the Model layer** - 
1. **Services** - It contains all the business logic. It depends on the Repository layer.
2. **Repository layer** - It does all the database interaction and sets the result to the service layer. Repository layer only has the raw databases query.
3. Seed folder - It contains all the seeders i.e for testing purpose all the sample data.
4. Migration - It represents the changes in the schema at various points.Every schema update is stored inside the Migration.
5. **Schema** - The logic of how the  database query sent by the repository layer should interact with the databases is in the Schema folder.
6. Extra folders - 
    1. configs
    2. utils - Like error handlers etc.

**All the above layers/folders are stored inside the src(source) folder**
Apart from the src folder there is also a test folder containing the unit tests.

While setting up the MVC architecture there are two types of implementation -
1. Component Based  - In this all the services like payments, booking, auth goes to the Model, services, controllers etc folder.
2. Feature Based - In this services like payments, booking maintain there folders and inside them have their models, controllers, services implemented individually for each service.
