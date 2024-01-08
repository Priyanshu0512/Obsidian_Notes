- In order to create a table use the following command. It create the databases with name mentioned in the config.json file of the config folder
```iterm2
npx sequelize db:create
```

- In order to create the tables in the database the following command is used 
```iterm2
npx sequelize model:generate --name Airplane --attributes modelName:string capacity:integer
```
Note - The above command creates a Airplane.js file in the models folders. Sequelize by default does not create the tables mentioned in the command but it works on the line of git that it the changes which are being made need to be committed in order for them to show up in the database and sequelize also maintains a version history of the all the changes being made.

- Changes in the properties of the attributes can be made in the files created in the models and migrations folders.Now changes can also be made in the files being created by sequelize in the models and migrations folder. Sequelize provides the user two levels of changes 
    - `JS level`-> If changes are made to only the files in the models folder them it becomes a js level constraint wherein it will prompt error when conditions are not met when data is being entered through js 
    - `Database Level`-> If changes are made to the migration file then a database level constraint is being added wherein errors will be prompts if data being entered in the database does not meet the required conditions.

- To commit changes to the database use the following command
```iterm2
npx sequelize db:migrate

// To undo the migration
npx sequelize db:migrate:undo
```
Apart from the user defined tables it also creates a **SequelizeMeta** table which stores all the migrations being done(sort of the like a commit history).
