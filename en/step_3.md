## Changing the page with JavaScript

Ultimately, you're going to create a collection of 'cards' that contain information about all the coutries in the world (don't worry, you won't have to type it in!), but you're going to start off with something a bit simpler: making one card. This is often how programmers approach a project —  break it down into small pieces and solve those, then put the pieces together to solve the problem as a whole. You'll see that approach a few times in this project.

To begin with, you need to create a `div` inside the `card-container` `div` that already exists on the page. 

--- task ---
In `script.js` create a function called `makeCard` to create a `div` and return it, like this:

```javascript
function makeCard() {
    var card = document.createElement("div");
    
    return card;
}
```
--- /task ---

--- task ---
Now create a `displayCountries` function that calls `makeCard` and appends the result to `card-container`:

```javascript
function displayCountries() {
    var cardContainer = document.getElementById("card-container");

    cardContainer.appendChild(makeCard());
}
```
--- /task --- 

--- collapse ---
---
title: Parents and children in HTML
---
You might have wondered about the `appendChild` function we used a moment ago — specifically where children come into all of this. It's just a way of discussing the relationship between different HTML elements. Elements inside another element are its children, and it is their parent. For example:

```html
<p>
    Hello everyone and welcome to my website! My name is <strong>Alex</strong> and you can find all of <a href="dev.html">my web developement projects</a> on the site. 
</p>
```

The paragraph (`<p>`) tag is the **parent** of the strong (`<strong>`) and anchor/link (`<a>`) tags and they are its **children**.

--- /collapse ---

--- task ---
Finally, at the bottom of `script.js`, add a line that calls `displayCountries` when `script.js` is loaded by the webpage:
```javascript
displayCountries();
```
--- /task ---

When your page reloads, you may notice that nothing has visibly happened. That's because your new div is completely invisible: there's nothing in it and it has no styling.

--- task ---
Create some basic styling for your card by creating a class in `style.css` with a few properties, like this:

```css
.item-card {
    background-color: lightblue;
    border-radius: 25%;
    margin-top: 10px;
    padding: 30px;
    text-align: center;
    width: 300px;
}
```
--- /task ---

--- task ---
Now attach your new class to the card by adding one more line to the 'makeCard' function in `script.js` to modify the `classList` (the list of all the classes an element has) for `card` to include the item `item-card` class you just created:

```javascript
function makeCard() {
    var card = document.createElement("div");
    card.classList.add("item-card");
    return card;
}
```
--- /task ---

Now when the page reloads you should see your card! It doesn't look like much yet, but you'll start adding content soon!