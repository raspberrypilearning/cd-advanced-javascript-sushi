## Display lots of information

Now that you've got a card working, it's time to add some more information from the API. Since the information is mostly going to be key: value pairs, like 'Region: Europe', a table is a good structure to use to display it. Ideally, you want to do this in a way that lets you write a very small amount of code to add new information, so you're going to use a function.

--- task ---
Start by creating a table in your card, by adding three lines to `makeCard` just before the `return` statement:

```javascript
function makeCard(country) {

    var card = document.createElement("div");
    card.classList.add("item-card");

    card.appendChild(textTag("h2", country.name));

    var flag = document.createElement("img");
    flag.src = country.flag;
    card.appendChild(flag);
    flag.classList.add("country-flag");

    var table = document.createElement("table");
    table.classList.add("info-table");
    card.appendChild(table);

    return card;
}
```
--- /task ---

Next, create a function called `infoRow` that will create and return a table row `tr` given a key and a value.

--- task ---
Add this `infoRow` function to `script.js`:

```javascript
function infoRow(key, value) {
    var row = document.createElement("tr");

    var keyCell = document.createElement("td");

    keyCell.classList.add("key");
    keyCell.appendChild(document.createTextNode(key));

    row.appendChild(keyCell);

    var valueCell = document.createElement("td");

    valueCell.classList.add("value");
    valueCell.appendChild(document.createTextNode(value));

    row.appendChild(valueCell);

    return row;
}
```
--- /task ---

Now you need to call `infoRow` and append the result to the table you created in `makeCard`. You should do this inside `makeCard` and, by nesting your function calls inside each other, you can do it all on one line!

--- task ---
Add this line to `makeCard` after you create the table, but before you `return` the card:

```javascript
table.appendChild(infoRow("Region", country.region));
```
--- /task ---

The table doesn't look great right now but you've already added a class to it, and one to the 'key' cell, which should make them easy to style.

--- task ---
Add this CSS code to `style.css` to style both the table and the `td` tags inside it:

```css
.info-table {
    border-spacing: 2 0;
    margin: 10px auto;
}

.info-table td {
    padding-bottom: 5px;
    padding-top: 5px;
    vertical-align: middle;
}

.key {
    border-right-style: solid;
    font-weight: bold;
    text-align: right;
}
```
--- /task ---

That looks a bit better. Of course, if you want to use your own knowledge of CSS and make it look even better, do so! Now add a little more data by including a few more lines in the `makeCard` function. For now, just use these ones. In the next section we'll look at how to handle more complex information that might have multiple values, like the languages spoken in a country.

--- task ---
Add these lines to your `makeCard` function, just after the earlier 'region' line:

```javascript
table.appendChild(infoRow("Capital", country.capital));
table.appendChild(infoRow("Population", country.population.toLocaleString()));
```
--- /task ---

--- collapse ---
---
title: What is the toLocaleString for?
---
You might have noticed that, unlike the other two pairs, for 'Population', you've used an extra function, `toLocaleString()`, on the value before passing it to `infoRow`. This function takes a number and formats it into a string that matches the number formatting the user would expect, for example using the correct seperator thousands, depending on where the user is located. If you like, try removing it and see what changes!

As you learn to be a more advanced programmer, you should start considering things like this and begin to understand how to create not just a working piece of software, but one that is easy for your users to understand and use.
--- /collapse ---