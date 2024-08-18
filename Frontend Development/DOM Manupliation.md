- It is a programming interface for web documents.
- It is a tree like representation of the web page that gets loaded into the browser.
- 


- **Selecting HTML element**
```js
document.querySelector('.message').textContent = "Something";
document.querySelector('.message').textContent // to get the text value.
```

- **Handling Events** 
```js
document.querySelector("element")
.addEventListener("Event", function () {
   // Callback function
});
```

- There are three types of Keyboard events present
    1. `KeyUp` -> When a pressed key is released.
    2. `KeyPress` -> When a key is pressed indefinitely.
    3. `KeyDown` -> When a key is pressed initially.

### Some common functions

- `.insertAdjacentHTML('afterbegin', str)` - It takes two argument's position of insertion and string to be inserted. Positions are `afterbegin` , `beforeend` , `beforebegin`, `afterend.
- `.innerHTML` - Returns all the HTML inside the mentioned tag.
- `createElement()` - Create a specified element and insert it into the DOM.
- `documentElement` - It returns the root element of the document. For non-empty HTML document it will always be the HTML element. For non-empty XML document it will be  the root of the document.
- `document.write()` - This function is used to write directly to the HTML output stream.
Note - Never use the `document.write()` after the document has loaded as it will overwrite the entire document. Also the location of the output depends upon the location of script tag.
- `setAttribute()` - This method is used to set new value to a attribute. If the attribute does not exists then it creates one. 
```js
//Create Element
const para=document.createElement("p");
para.innerText="Hello There";
document.body.appendChild(para); // insertion to DOM

// Finding elements
document.getElementById("first");
document.getElementBytagname("div");
document.getElementByClassName("intro"); // Returns list of all elements
document.querySelector('p');
document.querySelectorAll('p'); // Use .className for selecting classes.
// Accessing element by HTML Object Collections.
document.forms["formId"];

// documentElement
document.getElementById("demo").innerHTML = document.documentElement.innerHTML

// setAttribute
document.getElementById("intro").setAttribute('type',"button");

// Adding & Removing elements
document.createElement(element); // Create HTML element
element.remove(); // Remove element
parent.removeChild(element(child)); // Delete 
document.getElementById("intro").appendChild(element); // Add element
document.write(text);

// Replacing 
<ul id='mylist'>
    <li>coffee</li>
    <li>tea</li>
    <li>milk</li>
</ul>

function myfunc(){
const element= document.getElementById('mylist').children[1];
const newNOde = document.createTextNode('juice');
element.replaceChild(newNode,element.childNodes[0]);
}
```

### Difference between HTML-Collection & NodeList

| HTML Collection                                                                             | NodeList                                                                                                  |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 1. getElementByClassName(),getElementByTagname return a Live HTML collection.               | 1. querySelectorAll() returns a static NodeList.                                                          |
| 2. Items can be accessed by their name, id and index number.                                | 2. Items can only be accessed by their index number.                                                      |
| 3. It is live collection which means the list changes upon addition of elements to the DOM. | 3. Most Often it is a static list. This means if an element is added to DOM the NodeList will not change. |
## DOM Nodes 

In the DOM (Document Object Model), nodes represent different parts of an HTML or XML document, forming a tree structure. There are various types of nodes, each serving a specific purpose. Here are the common types of nodes in the DOM:

-  **Element Nodes**
    - **Description:** Represent HTML or XML elements.
    - **Access:** Accessed using methods like `getElementById`, `getElementsByTagName`, or `querySelector`.
    - **Example:** The `<div>` element is an example of an element node.

-  **Attribute Nodes:**
    - **Description:** Represent attributes of an HTML or XML element.
    - **Access:** Attributes can be accessed through the `attributes` property of an element node.
    - **Example:** In this example, `src` and `alt` are attribute nodes of the `<img>` element.

```js
<img src="example.jpg" alt="Example Image">
```

-  **Text Nodes:**
    - **Description:** Contain the text content within an HTML or XML element.
    - **Access:** Accessed through the `textContent` or `innerText` property of an element node.
    - **Example:** The text "This is a text node" is a text node within the `<p>` element.

-  **Comment Nodes:**
    - **Description:** Represent comments within the HTML or XML document.
    - **Access:** Accessed through the `comment` property of a comment node.
    - **Example:** The content within `<!--` and `-->` is a comment node.

-  **Document Node:**
    - **Description:** Represents the entire document.
    - **Access:** The document node is the entry point for accessing the DOM tree.
    - **Example:** The `<html>` element serves as the document node in this example.

- **Document Type Node:**
    - **Description:** Represents the document type declaration.
    - **Access:** Accessed through the `doctype` property of the document node.
    - **Example:** The `<!DOCTYPE html>` declaration is a document type node.

### Node Method

- `node.childNodes` - accesses the child Nodes of the selected parent.
- `node.firstChild` - accesses the first child of the selected parent.
- `node.lastChild` - accesses the last child of the selected parent.
- `node.parentNode` - accesses the parent of the selected child node.
- `node.nextSibling` - accesses the next consecutive element(sibling) of selected element.
- `node.previousSibling` - access the previous element(sibling) of the selected element.

```js
<title id="intro"> Hello there </title>

// Multiple ways of selected data

document.getElementById('intro').innerHTML
document.getElementById('intro').firstChild.nodeValue;
document.getElementById('intro').childNodes[0].nodeValue;
```
\

## On-load  & On-unload functions 

- **On-load functions** - The On-load functions are triggered when the webpage has completed loading that is it all the resources have be download and display.
- **On-unload functions** - The Un-load functions are triggered when the webpage is about to unloaded i.e. the user changes the browser tab or tries to change the page.This event is usually used to perform the cleanup task or prompt the user for confirmation before leaving the page.

## DOM Event Listeners

DOM Event Listeners provide a more flexible and powerful way to handle events compared to traditional event attributes (e.g., `onclick`). Event Listeners allow you to attach multiple event handlers to a single event, making your code more modular and easier to maintain.


### `addEventListener`

The `addEventListener` method is used to attach an event listener to an HTML element. It takes three parameters: the event type, the function to be executed when the event occurs, and an optional third parameter indicating whether the event should be captured during the event propagation phase.

```js
element.addEventListener(eventType, eventHandler, useCapture);
```

- `eventType`: A string representing the type of event (e.g., "click", "keydown", "change").
- `eventHandler`: A function that will be called when the event occurs.
- `useCapture`: (Optional) A boolean value indicating whether to use the capturing phase (`true`) or the bubbling phase (`false`, default).

## Event Bubbling & Capturing

Event bubbling and event capturing are two types of event propagation in the HTML DOM.
They are ways to handle the order of events attached to child as well as the parent.
### Event Capturing (Capture Phase)

- In this phase, the event travels from the root of the DOM tree to the target element.
- Event handlers attached with `useCapture` set to `true` are triggered during this phase.
### Event Bubbling (Bubbling Phase)

- In this phase, the event travels from the target element back up to the root of the DOM tree.
- Event handlers attached without specifying `useCapture` or with `useCapture` set to `false` are triggered during this phase.

