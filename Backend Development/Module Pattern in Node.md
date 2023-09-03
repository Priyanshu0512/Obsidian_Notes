Module is the mechanism for splitting the contents of the program into small chunks called module which can be imported in the future whenever needed.
There are two mechanisms to prepare modules in node.
1. Common Javascript modules(CJS)
2. ESM Modules also called ES6 modules.

# Common Javascript Module  
In this moduleing structure the functions from a file can be exported using the module global along with the exports key.
    Ex -
    module.exports = {
        linearsearch: linearsearch,
        binarysearch:binarysearch
    } // This is called named export.
     Or
     module.exports.linearsearch = linearsearch;
     As module.exports in an object hence by doing this the key value pair gets allocated.
    Note - If the key and value are exactly the same then on the name of the key needs to written.

 In order to avoid a lot of key value pairs during the exports this syntax can also be used.
        module.exports = linearserach; // This is called default export.
        Now module.exports was an object but now the property has been updated to it being a function.

 In order to import these functions in an external function another global **require** is used.
 Ex- const searchFunctions = require('./filename or absolute path');
           OR 
  const {linearsearch , binarysearch } = require('.filename or absolute path');
   Or 
   If the module.exports was used as a function in exports then 
   const linearsearch = require('./filename or absolute path');
   Here a function is being imports hence linearsearch is function and can be used directly.

The advantage of the second syntax in that only functions that are needed in the current file will only be imported. In order to given an alias to a function then use the following way-
const {linearsearch :ls } = require('.filename.js or absolute path'); 
Here ls is the alias.
In case the first syntax is being used then the functions will be accessed using the object key syntax.
Note - **By default node.js considers everthing to be in cjs pattern.**


# ECMAscript or ES6 modulling pattern

One of the ways to make the module pattern ES6 is to rename the file to .mjs extension.If in the package.json file package key is set to module then it will treat it an ES6 module.

In order to import function from another file following syntax is used
Ex -
     import (name of the object ) from '.filename.js';
     **Note - Module will only be located it the fileame has the .js extension.**
       Or 
     If named import has be to done then 
     import { linearsearch} from './searching.mjs'
     This type of syntax only needs to be followed only when the file from which the exports are been done are in ES6 pattern i.e .mjs extension.

  Note - Files have cjs moduleing can be exported to the files with mjs moduleing by adding .js in the filename but if .mjs is being mentioned in the import statement then all the function from the which the function are being exported must have the ES6 moduleing in any form. One way to do this is to  add export keyword in the function definition of the function to be exported.
             But this adding of the export keyword is a named export therefore in the import statement all functions needs to be destructured in form of an object.
             Ex - import {linearsearch, bubblesort} from './searching.mjs'
             In order to give a alias use 'as' instead of : like in cjs moduleing.

Note - In order to bring all the named exports and give them a alias then 
use the following syntax - 
import *  as sorting from './searching.mjs'
This gives a object with the name sorting which contains all the named functions.

Note- __ dirname is not available for use in ES6 moduleing.

In named exports alias can be given but in default exports as the name suggest  a single thing is being exported which will act as a default therefore any name can be given when it is being imported to the file without using any syntax as in named exports.

**JSON** - It stands for Javascript object notation solely because it looks like a javascript object. It advantage of the .json file is that is stores the version history and dependencies of the node modules installed. Using the json file all the packages and their dependencies can be installed using the command  in terminal  ' npm i '

Note- Since node_modules folder contains all the required modules it is quite a heavy folder and thus is not pushed on to the github but the package.json file is to be used by the end user to download all the requied dependencies using the node package manager.

**Creating a json file** - It can be created by using the command ' npm init' in the terminal.
Now the user will be asked to mention the details of the json file.
Note - package.json file contains the list of all packages installed manually by the user whereas package-lock.json file contains dependencies of the packages manually installed by the user.

NPM - It stands for Node Package Manager.

