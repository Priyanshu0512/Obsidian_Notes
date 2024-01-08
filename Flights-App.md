
### Chain of Flow - 
- src/index.js -> Routes -> Controllers -> Services -> Repositories -> Models -> Migrations 

- Error.captureStackTrace(err) -  option can be used to get info about the stack of functions where errors are happening. 
 - Reverse Proxy - It acts like the web server and takes request from the client and forwards its to the required service for completion.It is positioned in front of the web servers whereas as the forward proxy is positioned in-front of the client.
 ```js 
const { Airport,City } = require('./models');
const city = await City.findByPk(12);
console.log(city);
const airports = await city.createAirport({name: 'International',code: 'LKO'});
const lko = await city.getAirports();
console.log(lko);
await City.destroy({
   where: {
      id: 12
   }
});
```

npx sequelize model:create --name:Flights --attributes --source:string,--destination:string,--departureTime:integer,--arrival:integer, --class:alphanumeric, --price:integer, capacitiy:integer


when adding constraint using after creating of the model in references we use - table and field property for table name and key respectively whereas while adding constraints on table creation in references model and key  keys are used. 