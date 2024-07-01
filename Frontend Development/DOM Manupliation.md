

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


