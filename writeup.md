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
