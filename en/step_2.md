## Setting up your project

Normally, when you create a webpage, you write all your HTML in a HTML file, such as `index.html`. However, when creating a more advanced, JavaScript-based, web application, it's very common to use only a small amount of HTML directly in HTML files and to create the other HTML elements using JavaScript code. That's what we're going to do in this project.

The first thing you're going to need to do is create the files that will make up your application:

--- task ---
[Open a new HTML project on Trinket](https://trinket.io/library/trinkets/create?lang=html). You will need to create an account if you don't already have one.
--- /task ---

You should have an `index.html` file now, but you'll need a couple of other files too:

--- task ---
Create a `style.css` file.
--- /task ---

--- task ---
Create a `script.js` file.
--- /task ---

--- task ---
Add the following code to your `index.html` file.

```html
<html>

<head>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div id="card-container"> </div>
    
    <script src="script.js"></script>
</body>

</html>
```
--- /task ---

That's all the code you'll be typing into your HTML file in this whole project! As you can see, all it does is include the `style.css` and `script.js` files, and create a `div` called `card-container`. If you wanted to build this application into a larger webpage, you'd decide where on the page it appeared by moving `card-container` around.