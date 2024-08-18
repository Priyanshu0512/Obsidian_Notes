

```html 
<body>
     <button onclick="data()">click me</button>
</body>
<script>
     async function data() {
       const info = await fetch("https://fakerapi.it/api/v1/persons");
       const finalData = await info.json();
       console.log(finalData);
     }
   </script>
```

Note- info.json() is also an asynchronous function call.
