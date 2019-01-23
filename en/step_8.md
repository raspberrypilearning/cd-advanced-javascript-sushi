## Displaying multiple-items of information

You've mastered displaying single information values, but what about things that might have more than one value, like languages spoken in a country, or timezones that cover it? To handle that, you need to upgrade your `infoRow` function to be able to handle an array as input. You could also create a separate `manyInfoRow` function, but since a lot of the work done by either function would be the same, this would create extra work, and extra possibilites for bugs, if you had to come back and update how your info rows were created later. So keeping them together is the way I would build this program.

The first thing to do is think about how to display multiple items like this. HTML has a natural structure for that: the unordered list (`ul`) tag. So let's start there.

--- task ---
Create a function called `makeList` that accepts an array of strings and returns an unordered HTML list containing those strings:

```javascript
function makeList(listItems) {
    var list = document.createElement("ul");

    for (var i = 0; i < listItems.length; i++) {
        var item = document.createElement("li");
        item.appendChild(document.createTextNode(listItems[i]));
        list.appendChild(item);
    }

    return list;
}
```
--- /task ---

Now, you need to call this function from inside `infoRow`, but only when you've got an array as an input. Luckily, JavaScript can tell you if a variable is an array. `Array.isArray(value)` will return a value of `true` if the contents of the `value` variable is an array and `false` if it's not.

--- task ---
Update `infoRow` to check if `value` is an array and, if it is, to use `makeList` rather than trying to display it as a simple string of text.

```javascript
function infoRow(key, value) {
    var row = document.createElement("tr");

    var keyCell = document.createElement("td");
    keyCell.classList.add("key");
    keyCell.appendChild(document.createTextNode(key));
    row.appendChild(keyCell);

    var valueCell = document.createElement("td");
    valueCell.classList.add("value");

    if (Array.isArray(value)) {
        valueCell.appendChild(makeList(value));
    } else {
        valueCell.appendChild(document.createTextNode(value));
    }

    row.appendChild(valueCell);

    return row;
}
```
--- /task ---

--- task ---
Next, add the languages to your card by adding this line to your `makeCard` function, before the `return` statement.

```javascript
table.appendChild(infoRow("Language", country.languages));
```

Watch what happens!
--- /task ---

That doesn't seem quite right, does it? Just a lot of '[object Object]' appearing in your table, instead of the names of languages. Open up the console again and expand the countries array you've printed there. Open up country 0, Afghanistan, and then open up the languages array inside it. You'll see that, rather than being an array of strings, this is an array of JSON objects! That's a bit too complex for `infoRow` to handle. Luckily, JavaScript has a built-in function that can take one array, pass every item in that array through a function, and return an array of the results. It's called the `map` function and you're going to use it to quickly create a list of the names of the languages from these objects.

--- task ---
Update the language line in `makeCard` to this:

```javascript
table.appendChild(infoRow("Language", country.languages.map(lang => lang.name)));
```
--- /task ---
