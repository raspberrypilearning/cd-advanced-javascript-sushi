## Show all the countries

That's a pretty informative country card you've put together. Now a few more lines of code, and the power of APIs, will give you one for every country in the world!

--- task ---
First, update `displayCountries` to use a loop to get every country, rather than just the one you've been using to develop your card:

```javascript
async function displayCountries() {
    countries = await fetchAllCountries();

    console.log(countries);

    var cardContainer = document.getElementById("card-container")

    for (var i = 0; i < countries.length; i++) {
        cardContainer.appendChild(makeCard(countries[i]));
    }
}
```
--- /task ---

A couple of lines of code and there they all are! 

Of course, even if you switch Trinket into fullscreen view, you still only get a big long line of countries. It would be better if they could make use of the available space nicely. Thankfully, this is something CSS can help with!

--- task ---
Update your `style.css` to add a little styling for the `card-container`, like this:

```css
#card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 0 auto;
}
```
--- /task ---

That's it! A beautiful app for giving information on all the countries of the world!