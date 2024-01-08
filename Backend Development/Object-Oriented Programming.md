Oops is way of creating a mental model of real life entities.

**Class** - Class is blueprint of the real life entities having a common behaviour.
**Objects** - Objects are the real life entities having different properties but with a common behaviour.
Ex- For a product having name price etc these are called its data members(properties) while the action to buy or wish-list  the product is its behaviour.
Boilerplate code for a class and creating an object in js is given below.
```js
class Product{
    name;
    price;
    description;
    // let or var are not complusory

    buy(){

    }
    // function keyword is also not necessary.
    wishlist(){

    }
}

const obj = new Product();
//syntax to create an object.
```

**this** keyword - this always refers to the calling site **except in one**.
```js
let phone ={
    name: "Redmi note 9 Pro max",
    price: 15000,
    rating: 4.2,
    display(){
        console.log("first display", this);
    }
}

phone.display();

Output - 
first display {
  name: 'Redmi note 9 Pro max',
  price: 15000,
  rating: 4.2,
  display: [Function: display]
}
```

Here first display is printed then the display function is called in the context of the phone object hence the phone object is printed.

Note - this keyword always refers to the calling site except in one case which is when used inside the an arrow function.Here it is resolved lexically.
```js
const iphone ={
    name: "iphone",
    Price: 100000,
    display: function iphoneRed(){
        let iphonered ={
            name: iphoneRed,
            price: 110000,
            print: () => {
                console.log(this);
            }
        }
        iphonered.print();
    }
}

iphone.display();

Output- 
{ name: 'iphone', Price: 100000, display: [Function: iphoneRed] }
```

Here it prints the iphone object and the this keyword is being lexicographcally resolved.
Also it the iphoneRed function would have being an arrow function then it would had gone to the global scope and would have printed an empty object as in the global scope this is defined as an empty object.

**new** - The sole purpose of the new keyword is to create a new instance of a class or an object of an class. Syntax
```js
const p = new product();
```

Note - In the above line the calling context is the new object therefore this refers to the new created object.
Constructor - Constructors are used to initialise an the values of an object at the time of object creation.The purpose of the constructor is to return an object an assignment. Therefore returning an primitive has no effect of the output of the program whereas if an object is being returned then the object is passed to the calling site.If nothing is being returned then if is equivalent to **return this.**
Note- Constructor overloading is not present in javascript.
```js
class product{
    constructor(n,p,d)
    {
        this.name=n;
        this.price=p;
        this.description=d;
    }
}

const p = new product("Iphone",120000,"slick");
console.log(p);```

In the above snippet  name, price need not to be defined as the above code is just assigning a new key value pair to an object which is allowed.

As classes were introduced very late early the function of an class was mimicked using an function constructor.
```js
    function product(n,p,d)
    {
        this.name=n;
        this.price=p;
        this.description=d;
    }

const p = new product("Iphone",120000,"slick");
console.log(p); 
```
If new keyword is not used then it is now not a function constructor hence it returns undefined and values gets assigned by resolving this in the gobal context (i.e empty object). In the snippet as there is not return in function hence it is treated as return this.

**Data Abstraction** - It is the process of hidden unnecessary details and from the user and only showing the requited details.

```js
class product{
    #name;
    constructor(n,p,d)
    {
        this.#name=n;
        this.price=p;
        this.description=d;
    }

    set name(n){
        if (typeof(n)!='string') {
            console.log("invalid name");
            return ;
        }
        return n;
    }
    display(){
        console.log(this.#name, this.price,this.description);
    }
}

const p = new product("Iphone",120000,"slick");
p.name=10;
console.log(p);
p.display();

Output-
invalid name
product { price: 120000, description: 'slick' }
Iphone 120000 slick
```

In order to make a property(variable private) # is used. Now whenever the variable is used # has to be used.Also the variable cannot be used outside the scope of the class.
In the above code snippet p.name creates a new key value pair with name key while the # name remains unchanged as it is private.When p is printed then new name key is added to the object and not the original name key.

**The use of access specifiers restricts the accessibility of the variable out the scope.** It is essential to prevent invalid inputs being done in wrong variable. To combat this issue the concept of getters and setters is brought into the picture.
They are essentially  used to get the input to the key value pairs with some logic being implemented to prevent invalid inputs.

