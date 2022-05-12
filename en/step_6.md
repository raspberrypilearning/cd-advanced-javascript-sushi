## Using JSON in your card

Now it's time to start using some of that lovely data you got! A couple of quick updates should plug the data into the `makeCard` function you've already created:

--- task ---
Update `makeCard` to accept a `country` parameter, and to use it to get the name it displays from `country.name` instead of using a text string you give it.

```javascript
function makeCard(country) {
    
    var card = document.createElement("div");
    card.classList.add("item-card");

    card.appendChild(textTag("h2",country.name));

    return card;
}
```
--- /task ---

--- task ---
Have `displayCountries` pass the first country in the `countries` array to `makeCard`:

```javascript
async function displayCountries() {
    countries = await fetchAllCountries();

    console.log(countries);

    var cardContainer = document.getElementById("card-container")
    
    cardContainer.appendChild(makeCard(countries[0]));
}
```
--- /task ---

When the page reloads, you should see 'Afghanistan' appear as the country name on your card.

--- task ---
Add a little colour! Update `makeCard` with a couple of extra lines to include the flag of the country from the JSON. Note that the JSON doesn't actually contain the image, just the URL of the image, but you can use that as the `src` on an `img` tag and it will load up just fine!

```javascript
function makeCard(country) {
    
    var card = document.createElement("div");
    card.classList.add("item-card");

    card.appendChild(textTag("h2",country.name));

    var flag = document.createElement("img");
    flag.src = country.flag;
    card.appendChild(flag);

    return card;
}
```
--- /task ---

When the page reloads, you may find the flag is a little large! You can fix this by creating a class with a smaller width or height, and then adding that class to the flag image.

--- task ---
In `style.css` create a 'country-flag' class:

```css
.country-flag {
    width: 100px;
}
```
--- /task ---

--- task ---
Back in `script.js` add the `country-flag` class to `flag`.

```javascript
function makeCard(country) {
    
    var card = document.createElement("div");
    card.classList.add("item-card");

    card.appendChild(textTag("h2",country.name));

    var flag = document.createElement("img");
    flag.src = country.flag;
    card.appendChild(flag);
    flag.classList.add("country-flag");
    
    return card;
}
```
--- /task ---