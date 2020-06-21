# Positioning Content

## 1.Positioning with inline-block

 We can make a layout using inline-block . Let's take an example :

 ```
 <!-- HTML -->
  <section>
    <article>.........</article><!--
    --><article>.........</article>
    <article>............</article>
  </section>
  <!-- CSS -->
  article {
    box-sizing: border-box;
    display: inline-block;
    margin: 32px 1.5%;
  }
 ```

 In this example, we want all the articles in a line so we give each article's width 30% and margin 1.5% . We should give every items 'box-sizing: border-box' so  that padding and border dose not affect the whole width of the elements. We can set some property to all the items this way (Universal Selector):

 ```
 *, *:before, *:after {
    box-sizing: border-box;
  }
 ```
 In any layout we should use "box-sizing: border*-box" so that we can calculate elements' width easily.

## 2.Positioning with floats

  We can make layout using floats too by floating the elements left, right, or we can use none to remove floats. If we want only two columns then we can use like this :

  ```
  <!-- HTML -->
  <img src="https://altcampus.io/images/student-image.svg" alt="">
  <p>
    Float property removes the element from the normal flow of the page and position it to the left or right of the parent element.
  </p>

  <!-- CSS -->

  img {
    float: left;
  }
  ```

![image](https://raw.githubusercontent.com/suraj122/AC-STYLE-images/master/positioning-content/float-image.png)

>## Floats May Changes the Display Property:
When we float any element then it is removed from the normal flow of the page which also alters the default display property of the element. A block elements may start covering the space according to the content it wraps. To fix this behavior we can apply some fixed width according to the need.
```
section {
   float: left;
   width: 600px;
 }
 aside {
  float: right;
   width: 300px;
 }
```
An inline-level element for example <span> ignores height and width property. However, it may accept height and width if floated.
```
span {
   float: left;
   width: 300px;
   height: 300px;
 }
```

  Still if we want to use multiple element in a line then we can float each element to one direction left or right . But when we use floats then we find a problem like some elements bleed bellow the floated elements which is solved by containing floats or clearing floats.

### Clearing float

  Clear property accept three values that is left,  right, and both . If we float the element the left then left, if float the element to the right then right and if we float the elements to the both side then we can use both value to the clear property in the immediately next element .

  ```
  <!-- HTML -->
  <header>..........</header>
  <aside>.........</aside>
  <section>.........</section>
  <footer>............</footer>

  <!-- CSS -->

  header, aside, section, footer {
    padding: 50px;
    background: green;
    box-sizing: border-box;
  }
  aside {
    float: left;
    width: 30%;
    margin: 32px 1.5%;
  }
  section {
    float: right;
    width: 63%;
    margin: 32px 1.5%;
  }
  footer {
    clear: both;
  }
  ```

### Containing the floats

Clearing floats won't return each floated elements to the normal flow so we should use containing floats technique. We have two containing floats technique :

1. Overflow technique

  Overflow technique has many values the popular values are auto, scroll, hidden etc. We can use 'overflow: auto' but it  may add a scrollbar to the element in internet explorer on an Apple Computer. Instead we can use 'overflow: hidden' .Still the problem with hidden is that few styles like box-shadow may cut off outside the parent. It's just that different browsers treat overflow property differently.

  ```
  <!-- HTML -->
 <header>..........</header>
 <div class="parent">
   <aside>.........</aside>
   <section>.........</section>
 </div>

 <footer>............</footer>

 <!-- CSS -->

 header, aside, section, footer {
   padding: 50px;
   background: green;
   box-sizing: border-box;
 }
 .parent {
   background-color: orange;
   overflow: auto;
 }
 aside {
   float: left;
   width: 30%;
   margin: 32px 1.5%;
 }
 section {
   float: right;
   width: 63%;
   margin: 32px 1.5%;
 }

  ```

2. Cleafix Technique

  This is the best and advanced technique to containing a floats. In this method, we define some sort rules in CSS to the parent element containing floated elements.

```
<!-- HTML -->
 <header>..........</header>
 <div class="parent">
   <aside>.........</aside>
   <section>.........</section>
 </div>
 <footer>............</footer>

 <!-- CSS -->

 header, aside, section, footer {
   padding: 50px;
   background: green;
   box-sizing: border-box;
 }
 .parent {
   background-color: orange;
 }
 aside {
   float: left;
   width: 30%;
   margin: 32px 1.5%;
 }
 section {
   float: right;
   width: 63%;
   margin: 32px 1.5%;
 }
 .parent:before,
 .parent:after {
 content: "";
   display: table;
 }
 .parent:after {
   clear: both;
 }

```

In this example :before and :after pseudo-element create empty an element before and after of the parent element respectively. Define a empty element we didn't assign any value t the content property and we give a "table" value to the display property to make sure that content take the whole width of the display . We gave a clear property to the :after element and assigned a value of both to clear the floats.  

Developers use cf or clearfix class for this technique so that it can be use in deferent elements where we want to use floats. That's why we call it clearfix technique.

```
<!-- HTML -->
  <header>......</header>
  <section class="parent clearfix">
    <div class="col">......</div>
    <div class="col">......</div>
    <div class="col">......</div>
  </section>
  <footer>.......</footer>

  <!-- CSS -->

  header, .parent, .col, footer {
    background: #bada55;
    padding: 50px;
    box-sizing: border-box;
  }
  .parent {
    margin: 32px 0;
  }
  .col {
    float: left;
    width: 30%;
    margin: 0 1.5%;
  }
  .clearfix:before, .clearfix:after {
    content: "";
    display: table;
  }
  .clearfix:after {
    clear: both;
  }
```

## Reusable and Flexible Layouts

  Whatever technique we use in our web pages but our page should be reusable and flexible.

### Reusable Layout

  Reusable layout stands for consisting modular class which can be reused again and again. Let's take an example:

  ```
  <!-- Html -->

  <!-- section one -->
  <section class="container cf">
    <article class="article">*****</article>
    <article class="article">*****</article>
    <article class="article">*****</article>
  </section>

  <!-- section two -->
  <section class="container cf">
    <article class="article">*****</article>
    <article class="article">*****</article>
    <article class="article">*****</article>
  </section>

  /* Css style */

  .container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .article {
    float: left;
    width: 30%;
    margin: 1.5%;
  }

  .cf:before,
  .cf:after {
    content: "";
    display: table;
  }

  .cf:after {
    clear: left;
  }
  ```

  In this example we use "article" class as a modular class and used for each article and also we use the whole css code for the each section. We didn't write css for each section separately. That's called reusable layout.

###  Flexible Layout

  Flexible means our page layout should be resized according to the screen size. To create a flexible layout we have to create flexible container as well as columns too.

#### Uses of relative units

  For make a flexible box or column or container we can use relative units like percentage(%), viewport width(vw), em etc.

  ```
  <section>
    <div class="column">......</div>
  </section>

  section {
    width: 1000px;
  }
  .column {
    width: 40%;
  }
  ```

  In the above example we assigned a width of 50% to the "column" class thus the column class take the width of 400px and when the screen size decreased the size of the column will be 40% of the container means it will also decrease according to the size of the container.

#### flexible container

  To create a flexible container we can use "max-width" instead of "width" so that when the screen size will decrease it will automatically fit to the screen. If we use only "width" , when the screen get smaller than it will give a horizontal scrollbar. So it is better to use "max-width" to create a flexible container.

```
.container {
    max-width: 990px;
    margin: 0 auto;
    padding: 0 30px;
  }
```

  For dive deep into these topics we can use the example which is given in the "reusable layout" topic.

  ```
  <!-- Html -->

  <!-- section one -->
  <section class="container cf">
    <article class="article">*****</article>
    <article class="article">*****</article>
    <article class="article">*****</article>
  </section>

  <!-- section two -->
  <section class="container cf">
    <article class="article">*****</article>
    <article class="article">*****</article>
    <article class="article">*****</article>
  </section>

  /* Css style */

  .container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .article {
    float: left;
    width: 30%;
    margin: 1.5%;
  }

  .cf:before,
  .cf:after {
    content: "";
    display: table;
  }

  .cf:after {
    clear: left;
  }
  ```

  In this example "container" class have a max-width property which made the container flexible and we have a "margin" property which will center the container . The "0" value is for top and bottom and "auto" value is for left and right which will divide the margin equally to the left and right. Then we have also a 'padding' property which will helps the user to see the content properly . Padding should be used because when a page render in a small screen the content goes from left edge to right edge. It can be difficult to read for the users. So we use padding to the left and right for a breathing space .



##   Uniquely Positioning Element

  When we want an element positioned in a exact place then the 'position' property comes handy. Position property have many values like static, relative, absolute, fixed etc.

  The position property have a connection with box-offset properties - top, right, left, and bottom. By using these we can positioned an element in any exact place .

### Position Static

  By default, every element in a document is a static element and does not accept any box-offset properties. It will be in the normal flow of the page, won't be repositioned.

  However, the default static value for position property can be overwritten with either relative or absolute or fixed.

### Position Relative

  The relative value accepts all the box-offset properties. We can precisely position the element by shifting it from its default position in any direction(top, right, bottom, or left) still it will be in the normal flow of the page. The relatively positioned element will be shifted from its original position, without disturbing another element on the page. The original place of a relatively positioned element won't be taken by any element, it will remain empty. However, the relatively positioned element can overlap or underlap other elements, without disturbing their original positions. It won't push or shifts other elements on the page. If for the relatively positioned element, suppose both top and bottom box-offset properties are declared. The top property will take priority. For the left and right offsets depends upon the language which will take priority. For example, if the page is English, the left offset will be having priority and for Arabic pages right offset will be given priority.

  ```
  <div class="box box-1">......</div>
  <div class="box box-2">......</div>
  <div class="box box-3">......</div>

  .box {
    width: 100px;
    height: 100px;
    background: green;
  }
  .box-2 {
    position: relative;
    top: 60px;
    left: 60px;
  }
  ```

  In the above example the second box will shift from the top towards the bottom and left towards the right by 60px. But it won't disturb the position of the other two boxes on the page. Also, the original position of the element will be maintained.


### Position Absolute

  The absolutely positioned elements accept all the box-offsets however they are removed from the normal flow of the page and lose its original position. And that lost position will be taken by the upcoming element. Generally it can position in relation to its parent element which is already relatively or absolutely positioned. If the parent element is not relatively or absolutely positioned then the element will be positioned in relation to the body of the page. The display property may also change if the element is absolutely positioned. A block-level elements will start taking space according to the content. At the same time, an inline-level element may start accepting the width and height. If no box-offset properties are specified for absolute elements, the element will remain absolutely positioned in its original position but on the Z-axis and  will be lost the X and Y plane. Therefore the next element will take the original position of the absolute element and the absolute element will be on top of it. The absolute element can be positioned in relation to its parent or the body of the page. To position an element absolutely in relation to its parent the parent element must be either relatively or absolutely positioned. As like the relative position absolute also give priority to the top (between top and bottom) and left right offset depends on the language. The element takes the whole specified width. Combining all the four box-offset the element takes the specified width and height.

  ```
  <div class="box box-1">......</div>
  <section class="parent-box">
    <div class="box box-2">......</div>
  </section>
  <div class="box box-3">......</div>


  box {
    width: 100px;
    height: 100px;
    background: green;
  }
  .parent-box {
    position: relative;
  }
  .box-2 {
    position: absolute;
    right: 0;
    bottom: 0;
  }
  ```


  In the above example the box-2 is absolutely positioned with relative to its parent, because the parent-box has been relatively positioned. Therefore the box-2 will sit at the right bottom corner of the parent-box. If the parent element would not have relatively positioned the element would be sitting right bottom corner of body of the page.


### Position Fixed

Position fixed is similar to absolute positioning. However, the fixed positioning will be always relative to the browser viewport. The fixed positioned elements do not scroll with the page. Its position will be fixed relative to the browser viewport no matter where you stand on the page. Similar to the absolute element, the display property for the fixed element may also change. Fixed block-level elements may take space according to the content it wraps. At the same time, an inline-level element may start accepting width and height.

```
.box {
    position: fixed;
    right: 60px;
    bottom: 60px;
  }
```


### Z-index Property

  Using z-index property you can decide the order of an element, which will be on top and which will be at the bottom. The z-index property only works with relative, absolute, and fixed elements. By default, every element has 0 value for the z-index property. The element with the highest z-index value will appear on top and with the lowest value will at the bottom.


```
<section class="parent-box">
  <div class="box box-1">1</div>
  <div class="box box-2">2</div>
  <div class="box box-3">3</div>
</section>

.parent-box {
  height: 200px;
  background: #bada55;
  position: relative
}
.box {
  width: 100px;
  height: 100px;
  position: absolute;
}
.box-1 {
  left: 10px;
  top: 10px;
  background: red;
  z-index: 1;
}
.box-2 {
  left: 30px;
  top: 30px;
  background: blue;
  z-index: 2;
}
.box-3 {
  left: 50px;
  top: 50px;
  background: green;
  z-index: 3
}
```

  Here, the box-3 is having the highest z-index value, therefore, it will be on top and box-1 is having the lowest z-index value so it will be at the bottom.


>I have search for the sticky position value also it's    very interesting . We see this type of positioned element in  some pages where some element stick to the window according to the scroll.
