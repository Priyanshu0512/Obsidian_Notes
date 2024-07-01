- It stand for **HyperText Markup Language**.
- It defines the structure of a webpage or acts as a skeleton for it.
- `Markup language` -> It is a text-encoding system consisting of a set of symbols inserted in a document to control its structure, formatting and relationship between its parts.
- `Hyper Text` -> It is a special type of text document in which you can add **hyperlinks** of other documents.

# Tags

 Tags are the basic building block of a HTML document.
 - `<tagname>` -> opening tag
 - `</tagname>` -> closing tag
 - `<tagname/>` -> self closing tag. Here opening and closing is managed by the same tag.
##### Types of Tags
- `inline` -> This tag only takes up the space of its contents. It two inline tags are together they are displayed in the same line.
- `block` -> This tag takes up the entire space of the line. It two block level tags are together then they are displayed in separate lines.
#### Some basic tags are as follows 

 -  `<h1>` -> This is the heading tag. 1 represents the largest heading and as the heading number keeps on increasing the heading gets smaller and smaller. HTML provides heading from 1 to 6.
 - `<p>`-> This is a paragraph tag. Anything inside the paragraph tag is displayed as plain text.
 - Lists in HTML 
    - `<ul>` -> This creates an Unordered List without any sequencing typically rendering a bulleted list.
    - `<ol` -> This creates an ordered list with proper sequencing.
    (Note -> To add items inside the list use the `<li>` tag.)
- `<img/>` -> Image tag is used to add an image to an HTML document.
    - `src` -> In this attribute the path or the link to the image is written.
    - `alt` -> Alt attribute is used to describe the image content to the screen readers.
- `<div>` -> Div is generic container tag which can contain any data.
- `<span>` -> Span tag is also a generic container tag usually used to store smaller amount of data.
Note-> The difference between span and div tag is that span is an inline tag which div is a block tag.
- `<marquee>` -> This tag is used to create the moving text animation of the text on the sites these days.Although this tag has be deprecated.
- `<input>` -> Used to enter data from the user.
    - `type` -> This attributes tell the type of data going to be entered.
    - `value` -> The value entered in the value attributes in shown in the input tag usually a button.
    - `placeholder` -> Data inside the placeholder tag is shown till the user enters the data.It gives a hint about the sample input.
- `<select>` -> This tag is used to given option to the user to select from a bunch of values using the `<option>` tag inside the `<select>` tag.
-  `<textarea>` -> This tag gives an expandable area for writing text. Its dimensions can be predefined at start using the `rows` and `cols` attributes. Though the size of the area can be resized in the document by the user. 
- `<table>` -> This tag creates a table in the HTML document. Also various attributes can be given `<table>` tag like the `border` and `padding` properties etc. Inside the table tag various tags are used which are as following - 
    - `<thead>` -> This tag is used to define the table heading which is displayed in bold. Inside the tag `<tr>` tag needs to be defined to write the contents.
    - `<tbody>` -> This tag defined the main body of the table.
    - `<tr>` -> This tag is used to add rows to the table.
    - `<td>` -> The table data tag adds columns to the rows and hence used inside the `<tr>` tag.
    - `<label>` -> This tag programmatically associates the Text with its corresponding input which can be done by mentioning the id of the input in the  `for` attribute.
    - `<th>` ->  Defines the header cell in HTML table. It is expand to multiple columns using the `colspan` attribute.

- `<form>` -> Form tag is used to take input from the user using the `<input>` tag and submit the content over a network. The `<input>` has a `type` attribute which defines the input data. Other attributes include `placeholder`, `value` etc.
	- `action` -> The IP address or the URL of the server is mentioned to which the request is to be made.
	- `method` -> The request type is mentioned whether it is a `GET`,`POST` etc.
     - `value` -> This attribute places the actual text in the document.
    - `disabled`-> This attribute makes the element non-mutable, focusable or even submittable in a form. It only takes its value as disabled but its presence it sufficient enough to disable the element without the need of entering value.
  ( Note- A input tag with type `submit` or a button inside the form tag will submit the data collected within the form once pressed by the user.)
     - `name` -> This attribute is used to identity which values are coming from what fields. It creates a Key-value pair for the field and the value to uniquely identify the data on form submission.
     - `autofocus` -> When the page is reload the element is highlighted.
     - `size` -> Used to define the visible width in the element.

#### HTML level validation
- `min`,`max` -> These are used to set the minimum and maximum limit in the input tag with type `number`.
- `maxlength`,`minlength`-> Used to set the max and min length in the input tag with type `text`.


##### Other Tags & Attributes
- `<hr>` -> This tag is used to give horizontal line break in the document.
- `<a>` -> The anchor tag is used to link other hypertext document. The address of these hypertext docs is provided inside the `href` attribute.
(Note :- For opening the link in a new tab using the attribute `target='_blank`)
- `id` -> Id attribute is used to uniquely identify a HTML element.
- `class`-> Class attribute is used to uniquely identify a group of HTML elements. An element can belong to multiple classes.It is case sensitive.




### Document Object Model(DOM)
- It is an N-ary tree data structure i.e a parent can have N Childs.
- The attributes of the tag are the properties on  the nodes in the DOM.



#### How Browsers Render the Websites??

**Browser** -> It is a software that can load files from a local machine or some remote server. It also decides how the content should be displayed. 
- Browsers have an engine which algorithmically decide what to display.(Ex- Gecko engine is used be mozilla, Webkit for safari, blink for chromium)

- **HTML File Rendering** ->
     - Firstly the browser reads the HTML file in form of Bytes and are converted into characters.
     - The characters are tokenised by the process of tokenisation with the help of the parser.
     - Now parse tree is generated where these tokens acts as nodes with each node having distinct properties. This is called the `DOM Tree`.
- **CSS File Rendering** ->
     - The contents of the CSS file is read in the same way as the HTML file and `CSSOM` (CSS Object Model) is created.

After successful rendering of the DOM and CSSOM a `Render Tree` is Generated. Before the Render Tree is drawn on to the browser viewport one more step is involved called as `layout` or `Reflow` which is responsible for calculating the various position, sizes and other metrics for each element.
Now the `painting` process takes place the the Webpage is rendered on to the browser viewport.

### Loading of script tag
- Whenever a Script tag is encountered the DOM creation is halted
- Whereas in most engines the JS is halted if CSSOM construction is in place.

### Painting in Browsers
- Painting is the process of rendering pixels for each element based on the calculations, style & other info.
- It is responsible for rendering content, background and other visual effects.
- In painting process the render tree is traversed and renders `paint()` method is called to display  content on to the screen.
- `Invalidation` -> It is the process by which the browser determines which parts of the pages needs to repainted and invalidates them for the repainting process. The invalidated parts are seen as `dirty region` by the OS and triggers an `paint()` method which repaints the invalidated region.
- Painting order ->
   1. `background-color`
   2. `background-image`
   3. `border`
   4. children
   5. `outline`
- Types of painting
   - `Global` -> In global painting the entire tree is painted.
   - `Incremental` -> In incremental painting some parts of the tree are changed such that it does not effect the entire tree.

#### Difference between rendering and painting
- `Rendering` -> Rendering is the process which describes all the process of a HTML webpage such as DOM creation, reflow process and rendering of the DOM and CSSOM along with the render tree along with painting.
- `Painting` -> Painting is concerned with the HTML page after the rendering process is completed. It focus on the pixel by pixel changes to the webpage and changes the visual style depending upon the interaction.


