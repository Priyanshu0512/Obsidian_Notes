HTML Tags
1. <head> Contains all the meta data like the charset , descreption of the document, links to files linked to that HTML pags examples - like the stylesheet, head icon , javascripts(.js) etc.
	1. <meta> This tag is where the meta data is defined inside the head tags.  Its only has a opening tag. Example-     <meta name="author" content="Name of the author">
	2.<link> This tag is used to link an external file to the HTML 
          page. Syntax for the same is as follows:
	          <link rel="icon" href="styles.css" type="image/x-icon"> 
	          Note- Declaring the type reference gives a schematic meaning to the link here is should be specified for all types of links added to the HTML.
	3. <title> this tag displays its content in  browser tab of the page.
2.  <body> It contains the body of the HTML page. It is here where all the content of a HTML page is written.Almost all the tags which are used within the body tags have an opening and closing tag.
3. Various tags within the body tag
	1. Schematic Tags- These tags does not affect the appearance of an HTML page but gives meaning to the various elements. It also helps the screen reader to identify the elements nature.
	2. <header>A schematic tag which is used to define the heading section of the page just like a text document.
	3. <h1>This defines the Primary heading of the page.There is no such restriction on the number of h1 tags to be used in a HTML document but according to World Wide Web validation service there should be only one per HTML page.
	4. <nav> nav tag is used to create a navigation section in a document which will be used to either navigate through the different sections of the same page or provide links to different pages.
	5. <ul> This represents an unordered list. An unordered list is basically a list with no numbering on it . Instead of the numbers it only has bullets points infront of each element of the list.
	6. <li> Li in layman's terms stands for list item i.e. it is used to represent the various items in the list.
	7. <figure> This is used to represent a self contained element usually with a optional caption using the figcaption tag.
	8. <figcaption>This tag is used to give a caption to  the element of the figure tab.It is an optional tag.
	9. <article> Article tag is used to represent a standalone differentiable reuseable element of an document.An article must be provided with a "id" in its opening tag if it has to be used in different section of the same document or if it is to be to someother webpage.It must contain a heading.
	10. <section> This is tag unlike the article tag is given to that part of the document which does not have a much scematic meaning.
	11.<img> This tag is used to link an image file from the local machine or directly from  the Web.
	Its syntax is as follows.
	<img src="Path to directory or a weblink" title="The name given image(It will not be display in the webpage but will provide a description of the image to the web browser and will only to displayed in place of the image if the image fails to load in.)" 
	alt="It will be read by the screen reader(This functionality is implemented to provide support to differently abled people who use a screen reader to go through the content of the webpage)"
	width="Mention the width of the image provided"
	height="Mention the height of the image provided">
	12.<aside> It is used to display  the summary of the content mentioned within the summary tag.It is provide a drop down arrow upon clicking which the details of the content mention inside the summary tag is revealed.All the details, summary tag are also enclosed inside the details tag which contains all the content of the aside tag.
	13.<table> A table tag is used to create a table in a document. A table provides a better way to convey information to the end user in an organized manner.
		1. <caption>Inside the caption tag the heading of the table is mentioned.The contents of the caption tag in displayed at the top of the table.
		2. <thead>This tag represent the header of the table.It works same as the header tag.
		3. <tbody> tbody tag is where all the content resided inside the table. It is here where all the data values are displayed under the catergoried head as mentioned in the thead tag of the table.
		4. <tr> & <tc> These tag are used to define the rows and columns of a table respectively. 
		5. <th>This tag is used to differentiate the contents of the row or a columns from the row heading.Anything mention inside the th tag will be made "Bold".Although this couold be done with the help of strong tag inside the td tag but th is recommended as it not only provides a schematic meaning but also gives a structure to the html code.
		6. <td>This is where all the content is written . It the parent tag of <td> is <tr> then the content will be filled row-wise will each  new <td> tag and vice-versa automatically.
		7. Scope - Scope is defined in the opening tag of <th> tag. It bascially provides a schematic meaning i.e. whether that particular tag  contains row elements or the columns elements. It is done by defining the value of scope to either row or to column.
	    8.rowspan & colspan - These are defined in the<td> tag. They take up positive numeric values. There value define how much that particular cell of that row or column will span through. For example- if the value of colspan is 2 then it will span horizontally taking up the space of 2 columns of double the width of the orginal column but same height.
	    Similarily if the value of  rowspan is 3 then it will span veritcally taking up the space of 3 rows of triple the width of the original but of the same width.
   14.<br> br tag is used to given a line break in a document.
   15.<hr> hr works similarily as the br tag but instead of giving a blank line spae it instead draws a line to seperate the content.
   16.datetime- Datetime tag is used where a sepcific value of time is mention in the document. It is an schematic tag wherein in translate's to the web browser the value of time mentioned.
   16.<address> The address tag is used to enclose a address within it. It givens the contents mentioned inside it a sort of an italics font which differentiates it from the other contents of the page.
   17.<form>  Form tag is used to represent the section of the document with interactive controls.It is here where the user can enter his//her data.
      1.<fieldset> This tag is used to differentiate various section of the document or a form having interactive controls. It is provides with a <legend> tag which is used to given a caption to the section.There can be multiple fieldset inside the same tag (for-example form tag.)
      2.<legend> Legend tag is used to give caption to the fieldset tag.
     In order to take various types of input form the user <label> and <input> tag are used with with various attributes to change the input method.
     3.<label> Label tag is used to display the type of value a user needs to enter in the respective section.It's syntax is as following. 
     <label for="name of the field to entered">Name of field to be displayed </label>
     Note- It could be anything inside the for attribute but it is adviced to have something related to the field.
     4.<input> This is the tag where the type of input is specified and the user enter's the value of the specified field in this tag.
     It does not have any ending tag. The syntax for the same is as follows.
     <input type="the type of input to be taken" name="a name is given to the field to be entered." id=" value should be same as that of FOR attribute mentioned inside the particular input's label.">
     Note- name attribute does not having any effect on the document visually or internally but is gives the reader of the code a hint about the value going to be entered.
     There are also some optional attributes that could be mentioned inside the input tag as per the requirement of the user. These attributes are as follows-
     1. placeholder- This attribute as the name suggests is used to give a placeholder to the input box for giving a better clarity about the format of input to the user.
     2. required- If this attribute is present inside the input tag then it makes it mandatory for the user to enter a value.
     3. autocomplete- This tag comes in handy if the page is being visited a number of times to enter the same details. This tag saves the user information automatically and can fill in the data whenever the value being entered inside the field is partially same as the stored value.
     The input tag can take a variety of inputs.The link to the description  of these types is url-https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input  
   
   