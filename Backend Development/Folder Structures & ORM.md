

- `src` -> Inside the source folder all the actual source code of the project resides.(Does not include a tests folder.)

  Segregation inside the `src` folder

    - `config` -> config folder contains all the configurations related to the setup of the library and modules.
      Ex - logging library can be implemented in the config folder to prepare meaningful logs.It is implemented in the `logger-config.js` file.

    - `routes` -> In the routes folder we register a routes and bind with it its corresponding middleware's and controllers.

    - `middleware's` -> The middleware's intercept the incoming requests where validators and authenticators etc. are implemented.

    - `controllers` ->They are the last middleware's as post them they call the business layer to execute the business logic. In controllers we just receive the incoming request and data and then pass it to the business layer. Once the business layer returns an output, we structure the API response in controllers and send the output.

    - `repositories` -> This folder contains all the logic using which we interact with the databases by writing queries, all the raw database queries and ORM will go in here.

    - `services` -> Contains all the business logic and interacts with the repositories to get the data from the databases.

    -  `utils` -> Utils contains all the helper methods, errors and classes etc. 

**Setup the Project**

- Download the template from Github and open in a text editor.

- In the root directory create a `.env` file and the following  env variables
```
   PORT = <Port Number>
```

- Go inside the src folder and execute the following command 
```
     npx sequelize init
```
- By executing the above command seeder, migrations folders and config.json file will be created.

- If you are setting up the development environment, then write the username, password of your database and mention the name of the database in the dialect.
- If setting up the test environment or production environment , make sure to change the host to hosted database URL.


**ORM** - Object Relational Mapping. **It is a technique used to create a bridge between object-oriented programs and in most cases relational databases.**
Famous ORM's are  sequelize, mongoose etc.

We will be using sequelize for our project.

