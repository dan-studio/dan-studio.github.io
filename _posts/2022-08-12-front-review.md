--- 
layout: single 

title:  "Reviewing Basic Knowledge of FrontEnd"
categories: FrontEnd
tags: react
toc: true
sidebar: 
    nav: "docs"
---

Before moving on to React, I just wanted to review the Basic frontend Knowledge.

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/ac1baa8a-654b-4524-9eaa-7216396aad33/image.jpeg)

![img](https://c.tenor.com/pPKOYQpTO8AAAAAd/monkey-developer.gif)

## HTML
> HTML(HyperText Markup Language) is the standard markup language for documents designed to be displayed in a web browser. It can be assisted by technologies such as Cascading Style Sheets (CSS) and scripting languages such as JavaScript.

Example of HTML file:
```html
<!DOCTYPE html> <!-- Version of HTML being used -->
<html> <!-- Start of the HTML document -->
  <head> <!-- The head section of a document.
    Usually contains CSS, JavaScript
    scripts, metadata
    -->
    <title>Document Title</title>
  </head>
  <body> 
    <!--
    The content of the document goes
    into the body section
    -->
   <h1>First Heading</h1>
    <!-- Rest of page goes here -->
  </body>
</html> <!-- End of the HTML document -->
```
take a look at [w3school HTML Tags](https://www.w3schools.com/tags/default.asp) for more information about the HTML tags

## CSS
> CSS(Cascading Style Sheets) is the language for describing the presentation of Web pages, including colors, layout, and fonts.

~~~css
body {
  background-color: lightblue;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 20px;
}
~~~
take a look at [w3school CSS Reference](https://www.w3schools.com/cssref/default.asp) for more information about the CSS Reference

## Javascript
> Javascript is the world's most popular programming language that enables you to create dynamically updating content, control multimedia, animate images, and pretty much everything else.

~~~js
  <button id="button"> Click Me! </button>
</body>
<script>
  document.getElementById("button").onclick = function(){
    alert("Hello World"); // displays an alert box
  };  
</script>
~~~
take a look at w3school [JS Tutorial](https://www.w3schools.com/js/default.asp) for more information about JavaScript
