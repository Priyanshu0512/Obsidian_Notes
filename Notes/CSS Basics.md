
css 1 was first introduced in 1996.
version 2 in 1998
version 3 introduced development in modules hence not more future version
usign the style command inside the html tag is called the inline styling.
(not recommanded)
using the style tag in the head section increases the load time of the page depending upon the content inside the tag.
also using an external stylesheet caches the files and hence if it is used by many pages then it would increase their loading time as well.
if use the world sans-serif in the font family then it changes the font to the default font specifed under the sans serif catergory of the browser.
sans-serif - It means a font with less extending features. Example - A font not having  extending features then the sans serif version of the font will not have those extending features.
attribute selectors- [disabled]
css is case insensitve
In css the parsing is done top to bottom.
Inline style has the highest specificity.
Sepecificity order
body selectors<<universal selectors(*)<< tag, psuedo element selectors<< classes,psuedo classes, attribute selectors<< #ID selectors<< inline selectors
use of combinators increases the specificity
there are four types of combinatores
1.  adjacent combinators ( h1+p) - In this type of combinators styles mentioned will be applied to second tag who are a direct sibling(immediately after it) of the first tag.Here are the p tags who are direct sibling of h1 tag gets the styles.The first tag should be the parent of the second tag.
2. general combinators(h1~p)In this type of combinators the second has to be only a general sibling of the first tag(parent tag).
3.  child combinators (h1>p) - In this type of combinators the second tag must be a direct child of the first tag(parent tag). 
4. descendant combinators (h1 p)- In thsi type of combinators the second tag should be only a descendent of the first tag. i.e ( it should be some how related to parent tag either a child or a sibling)
margin-collapsing- when two or more box elements are together side by side or top and bottom then the elements margin overlap each other on adjacents side and the bigger margin in taken in consideration.
In shortand property the order of values does not matter until the units of the value are same.
If values are same then 
for Margin 
1. for all different value- margin: 5px 10px 15px 20px(top right bottom left)
2. for top&bottom and right&left values same - 
  margin: 5px 10px(top&bottom and right&left)
3. for all same values - margin: 5px( all same )
margin are not included in the width calcution.
display- inline block - this is used to display the element in inline form while giving the flexiblility to add padding ,margin and border.
Adding class to the element and styling is faster than use of combinators but the difference in neglible.
pseudo classes are used to define the specific state of an element (:class name)
pseudo element are used to define the specific part of an element(:: element name)
css class selectors - They are reuseable and are only used to mark and style things in css (they don't have any meaning in css document )
css Id selectors - They are one used on per html page.they as well don't have any meaning in css document.
It is not recommended to use id selectors for styling usually as id can be linked in the anchor tag to navigate certain sections of the page here could lead upto some wierd behaviour.
!important - it overwrites all the specificity of all the selectors.(don't use it )
syntax- div{
      color: red !important;
}
maring: auto automatically assigns equal margin to the left and the right of the avaliable space.
with float you overwrite the default postioning of the element  and can positon it right or left of the page.It takes out the element out of the flow of the document.
clear - it tells the document to not consider the float on both the left and right.
default value of position : static
viewport is the visible part of the web page.
fixed-Takes he element out of the document flow and chagnes it's behaviour to inline-block element and the position now depends upon the viewport (as per value of the top.bottom,right,left).can be applied to both block and inline elements.
top,bottom,right,left value only work if the position value is anything but static(default value)
z-index does not impact the elements who positon property is set to default (static).
if more then one element have the same z- index then the order in which there are present in the html document will dictate which element will be displayed above the other wherein the latter element in the html gets displayed above the first element.
for absolute position property the postioning context is the nearest ancestors will the position property other that static. If it is static then  it's context is  as an html element.
in relative positioning the element itself is the positioning context and it is not taken out of the document flow.
if only the body element has overflow set to auto then it is passed on to the html  element unless it already has overflow value of hidden or auto.
sticky property- keeps the element fixed or relative depending upon the viewport.
stacking content - children of the parent cannot go above another parent unless and until there parents z-index is above the parent above it.
background-size
1. cover- automatically determine the whethere the container should be filled lengthwise or widthwise.if the image is in portrait mode then the image will occupy the entire height of the container and landscape will be scaled accordingly.
2. contain- if ensures that that the entire image  is displayed on the screen rather than the entire container being fille with the image(unlike cover.)
background-position-giving percentage values in the input results in a different behaviour.
suppose the first value is 50% then it will ensure that the parts of the image which are not inside the container  50% of those will be cropped and and the remaining part will be adjusted inside the container.

while adding multiple background only one background color can be added.
svg- scalable vector graphic
when a position  fixed is applied and size is defined with the percentage unit then the contaning block is the viewport.
when position absolute is applied and size is defined with the percentage then the containing block is the nearest ancestor(content+padding) which does not have it's position static(default).
if no other ancestor is present having a value other than static then it takes it value form the viewport  and behaves somewhat like the fixed position type.
when position static or relative is applied and size is defined in percentage then the containing block is nearest ancestor which is a block level element whose only content is taken is consideration.
rem no matter to which property to which it is applied it always refers to root font-size.
default setting of the browser for font-size is 16px.
 units to use
	 property                                                     recommended
1. font-size(root element)	                       percentage(%)or nothing
2. font-size                                                     rem,em(chidren only)
3. padding, margin                                       rem
4. border                                                         pixels
5. width,height                                              percentage(%),vw,vh
6. top,bottom,left,right                               percentage(%)
7. max,min width,height                            px(usually)

margin auto only works for block level element with and explicitly defined width.

all the styles listed in the dom variable are inline style.
to select all the class with the mentioned name used .querySelectorAll
variable and elements are invalid in javascript if they containi a dash.

viewport meta tag in the html  configures the browser to take in account the software pixels instead of the hardware pixels of the device. It's syntax is as follow-
<meta name="viewport" content="width=device-width, initial-scale=1.0,user-scalable=yes ,maximum-scale=2.0"> with viewport meta tag there are no design changes.
content="width=device-width"- allows to set the width of the document to the width of the device.
initial-scale - sets the zoom level
user-scalable- allows or restricts the user  from zooming in or out on the website.(default is set to yes).
maximum and minimum scale- restricts the maximum and minimum zooming in and out respectively.

media queries allow us to change the size according to the design
logical operator
1. and - and 
2. or -,

all the input labels and button despite being set to display block does not take up the full width of the page . In order to occupy the complete width it has to be done implicitily.

Advanced attribute selectores
1.   [type]{color: red;}
2. [type="email"]{color: red; }
3.    [type~="lang-us"]{color: red;}
         this means the input should have the lang-us attribute. It can also have more attribute  but should have lang-us as one of them.
4.  [type| ="en"]{color: red;}
          this means the element should have the specific value or should have it as an prefix.
5.  [href^="#"]{color: red;} 
         this  selects all thr element which have the attribute href and its value has a prefix of #.
6. [href$=".de"]{color: red;}
        this selects all the element which have the attribute href and tis value has  a suffix of .de 
7. [src*="cdn"]{ color: red;}
        this selects all the element which have the attribute src and hava value wherein some some part of the value have the  cdn
8. [src*="cdn" i]{color: red;}
     this selects all the element which have the attribute src an have a value wherering some part of the value have the cdn irrespective of the case.

there are two types of font families - generic and font families
    generic- serif, sans-serif, cursive,monospace, fanstasy
    inside these generic families we have font families .
 font syntax-
        font: "font family name", "2nd font family name ", generic font family 
        font family name needs to be inside the double quotes if there name contain whitespaces.
        if none if select then the default browser font setting is applied.
in order to apply italic from the imported font use the property font-style:italic;
 In order to import your custom fonts us the following syntax
 @font-face {
font-family: "anonymousPro";
src: url(anonymousPro-Regular.ttf);
}
.ttf stands to truetype format
woff web open font format 
font-variant: small caps- this changes all the small caps letter to capital ones without increasing there height.
line-height - it helps to define the top and bottom space in the content box. by default it depends upon the font-family used but when you set the value it depends on the font size.
font shorthand-
 font: font-style font-variant font-weight font-size/line-height font-family;
font-display- only works with custom font in @font-face selectors
                             block period                                   swap period
    swap                   n/a                    fallback    infinite time-custon font       
    block                   short                fallback    infinite time-custom font
    fallback          very short           fallback   short-custom font fallback
    optional        very short           custom-font else fallback
    auto - browser decide the best option(usually block )
generic family are a fallback if the font-family fail to load.

Flexbox-Adding the display:flex to a element makes it a flex container and its children are called flex items.
Properties that can be applied to flex containers are justify content, align-items,align-content and flex-flow.
Properties that can be applied to flex-items are order,align-self and flex.
When we apply the display flex property then two property are automactically defined which are 
 1.  flex-direction: row (row being default)
 2. flex-wrap: nowrap(nowrap being default)

There two main axis when the display flex is defined
 1.  main-axis  -  It is direction is defined by the flex-direction property.If the flex direction is row then it goes from left to right and if flex direction is set to row-reverse then it goes from right to left. It direction can only be changes when flex-direction row or row-reverse if applied. In both the cases the direction of cross axis remains top to bottom.
 2. cross- axis  - It direction if also defined by the flex-direction when its values are set  to either column or column-reverse.For default value of flex direction(row) it goes for top to bottom. If flex-direction is set to column or column-reverse then it goes from top to bottom or  bottom to top respectively.In either of the situation the direction of the main axis remains same(left to right).

Justify-content- This property defines how the browser distributes the space around and between the flex container along the main-axis and inline-axis of the container. It has a lot values some of which are start, end , left, right, space-between , space-around,space-evenly.

Align-items- The CSS align-items property sets the align-self value on all direct children as a group. In Flexbox, it controls the alignment of items on the Cross Axis. In grid layout, it controls the aligment of items on the block axis within their grid area.

Order- This property is used to define the order in which the elements inside the flex container are arranged in the direction of the main-axis. Higher the value of order property more it will be displayed further from the starting point of the main-axis.

Differene between flex-start and start
 Flex-start align the items according to the direction of the main-axis
 start aligns the items according to the document flow.

Flex-shrink - It is used to set a shrink factor to the flex-items.
It default value is 1  wherein it shrinks the element till the point no spacing in left around the content.A value of 0 restricts it from shrinking. If different value of flex-shrink are applied to different flex-items within the same flex-containter then items shrink in the ratio of the value used.

Flex-grow - It is used to set a growth factor to the flex-items. It default value is zero wherein the flex items do not grow beyound  their specified dimensions. If it is  applied to a single items or to all the items with a common valuethen it takes up all the extra space irrespective of the value . In the case of different values the extra space is distributed in the ration of there values.
                        increased width=( flex-grow of .this item)/(Sum of the 
                                                          values of the flex-grow property )* extra space induced.
If flex-wrap is set to nowrap then if the elements specifed dimension will not decreae beyon there limit but the element will be transferred to a new row or columns depending upon the flex-direction and will take the entire width as a single is is only present hence 100% width due to flex-grow property.      

flex-basics, flex shortand - grow shrink basics
display grid, grid-template-columns- 200px  1fr 150 2fr;
grid-column -start/end:  repeat( no of times, pattern),span in grid,overlapping of elements and z-index.

for naming the lines specify the name in square brackets in front of the value syntax-
grid-template-rows: [row-1] 5 rem [row-2 row-end] minmax( 40px, 300px) 
mutiple names can be added separated by a whitespace.

Shorthand for grid-column/row-start/end-
grid-row/column: start value / end value;
instead of values line names can also be used.

For combining all the column and row start end values.
grid-area:  row-start / column-start / row-end / column-end;

grid-row-gap and grid-column-gap are used to specify gap between the row and column without distrubting the positon of the elments inside the cells.However in-case of spaning elements across the row or columns the gaps are not visible but are present.
Shorthand - grip-gap: row-gap(separated by a whitespace) column-gap;

Grid-area-template  - It is way naming the cells in the CSS grid.
Using this elements in the CSS in grid can directly be position in the any cell using its address( name given to the cell).For using this  template firstly grid-area-template must be defined in the grid container. Syntax for the following is as follows:
grid-area-template: " header header  header header"
                                        " side .  main main"
                                        "footer footer footer footer";
If a new is not to be name the a full stop should be placed instead of a name.
Now in order to position and element in a particluar cell use the property grid-area: name of the cell; in the element selector.

Automatically Generated grid area- 
 grid-template-columns: [hd-start] repeat( 4 , [col-start] 25% [col-end]) [hd-end];
 grid-template-rows: [hd-start] 5rem [hd-end]  ........

By wrapping columns with [hd-start/end] CSS automactially creates an named grid template area with the name header.
Note- This would not work if wrapping rows have different start and name.
Now this header name can be used in element selectors to posting the element. Syntax- grid-area : hd;

fit-content(defalut size)- It scales the row or columns inorder to fit the content but if the content is smaller than the defalut size mentioned then the defalut size in applied.

justify-items - It aligns the elements along the horizontal axis. Default value is stretch.
align-items - It aligns the elemens along the vertical axis. Default valus is stretch.
justify/align-content - These properties are used to align the entire content of the inside the grid container itself horizontally and vertically respectively.
In order to position individually use the justify/align-self property in the elment selector.
grid-auto-rows is used to style the automatically generated rows in a grid.
grid-auto-flow is used to specify whether the row or columns should be added automactically.

auto-fill - This is used inside the repeat function when we explicitily define the rows or columns. It autmactically adds new columns to fit in the elements within the viewport or till the maximum widht/height defined.
auto-fit - unlike the auto-fill it bascially center the elements in row or column if not enough element are present to take the viewport or width defined. If it is defined in grid-template-columns then it center the elements horizontally and vice-versa.

transform: rotate(X/Y/Z)(degree); - This is used to rotate an element about an axis.
transform-origin - This property is used to define the axis of the rotation. By defalut it is set to center. Both absolute and relative units and percentages can be used to specify the axis of rotation.Values like top left, right, center can also be used.

translateX(distance to be translate)- This function is used to translate an element along the X-axis.
Note - The X-axis will be always along  the element passing through 
through the co-ordinate mentioned in the transform-orgin property(by default it is set to center).So if an element is rotated along the Z-axis with an angle of 75deg then both X and Y axis will be rotated by the same angle.

skewX(degree)- It is used to skew an element along the X axis.
Shorthand( x-axis degree  y-axis degree z-axis degree);

Scale( Scaling coeffecient) - It is used to scale an element along the x,y,z axis. If only one value is entered it scales it one both x and y axis  (also z but can not be noticed for 2D elements)

perspective(value in pixels) -It display the element giving it an 3-D view. Smaller the value  the closer you are to the element and  vice-versa. If perspective is to be used as a standalone property instead of mentioning it in the transform property then it needs to defined in the wraping container of the element on which the perspective property needs to be applied.
perspective-origin- It is used to adjust the camera pos. Right ,left,center etc. are all valid values.
When translating an element along Z axis despite the size of the value the element will always respecet the z-index values i.e. it cannot go behind  or infront of an element with different z index by a large value of translate.
While rotating a container by 90 deg along the Y-axis the container along with its content cannot by seen even if elements inside the container are rotated or translated by some value. This is becaus by default the transform-style value is set to flat which converts 3-D plain of the container into a 2-D space.  In order to change this behaviour use the value preserve-3d.
In order to hid the backend of the element while flipping or while transforming the element set the backface-visibility: hidden;
By default its value is set to visible.
Transition Property - Using the transiton selectors various animations can be introduced in the css. 
Syntac -  transiton: first property  time duration timing function(style of the transition) time delay(time after which the animation starts),  (same for second proprty);
If the display property is changed for the transitiong element then the animation would not kick-off.

What happens when a webpage is loaded??
Firstly the HTML is loaded and then parsed and the Document object model is formed. After the HTML is parsed the CSS is load and is parsed (resolving the conflicting CSS declaration and processing the final CSS units.)creating the CSS object model(CSSOM). After this both DOM and CSSOM are combined to form the render tree. This render tree is now is now formatted by visual formatting model and the then the final render is complete.

using the float property takes all the affected items out of the dom hence the all the property likes the heigt width all collapses. In order to fix this think a clearfix class is defined usually. 
 (name of the select in which the clearfix has to take effect):after{
       content:"";
       clear: both;
       display: table;
 }

Sass is CSS preprocessor.

Variable in sass are defined by writing a  $sign in front of the value follwed by there value.
Ex- $color-primary: #f9d3d5;

darken is predefined function whose syntax is as follows
background-color: darken(variable name or color  , darkness 
                                                                  percentage to increasesd)
same goes for the lighten function.

mixin is a reusable code that could be used anywhere again and again the code. Ex the synatax is as follows:-
@mixin name of the class or tag selector(variable to be passed){function};
In order to include the mixin in a function use the following syntax:-
@include name of the mixin(variable to be passed to the mixin);
Function can also be declared in the scss using the following syntax:-
@function add($num1, $num2)
{
    @return $num1+ $num2; 
}

%- Percentage sign is used to represent placeholders in scss.
extends is different from mixins as in the case of mixins the original code written is  copie to the funciton where the mixins is adedd while in the case of extends the selectors to which the extens property is added  gets copied to the placeholder text mentioned.

In Sass in the rgba function instead of specifying the code directly sass variable can be used.
Not psuedo class- This is usually used in the way wherein it it used to select all the elements except a single type of element. It syntax is as follows-
&:not(name or class of the element or an another pseudo selector){
    // property;
}

while using the calc function in sass if a variable is being used then it has  to be wrapped in the curly brackets and has to be preceeded by the hash(#).
[class^=col] - This selects all the classes which starts with col.

-webkit-background-clip: text; - This property will clip the background image at all the place except the textor the content.


