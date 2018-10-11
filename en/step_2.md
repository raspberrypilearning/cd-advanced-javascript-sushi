## Getting Pokémon

If you're going to display information about Pokémon, you're going to need some information to display! Luckily, some nice people have put together an API you can use to ask for that information. There are APIs for everything from Google, to Instagram, to YouTube, to the weather! That's where you're going to start: Asking for the information. 

Before you can even do that, though, you're going to need somewhere to put it once you've got it! 

--- task ---
In `script.js` create three empty arrays, like this:

```JavaScript
  var pokemonInfo = [];
  var pokePics = [];
  var pokemon;
```
--- /task ---

 Next, you need to create a function that can `fetch` information about a Pokémon from PokeAPI. You do this by **requesting** a **URL** (web address) and storing the **response**. In the case of PokeAPI, the URL is `https://pokeapi.co/api/v2/pokemon/[id]/`, where `[id]` is the id number of the Pokémon you want. Pikachu, for example, is number 25 and we would request Pikachu's information with `https://pokeapi.co/api/v2/pokemon/25/` . 
 
--- task ---
 Add a function that fetches a Pokémon's details to your `script.js`

```JavaScript
  async function fetchPokemon(pokemonId) {  
    var response = await fetch('https://pokeapi.co/api/v2/pokemon/'+pokemonId.toString()+'/');
    var poke = await response.json();
    pokemonInfo.push(poke);
  }
```
--- /task ---

This function looks relatively normal, taking `pokemonId` as a parameter, fetching the URL, taking the response and `push`-ing it into `pokemonInfo`. However, look at a couple of unusual things here:
  1. Instead of `function`, this is declared as `async function`
  2. Twice, JavaScript is told to `await` something
These two **keywords** always come as a pair — only an `async` function can contain `await`. What `await` means is that, instead of sending off the `fetch` and forgetting about the response back from PokeAPI, JavaScript should pause to `await` the `fetch` being completed, and then pause to `await` the `response` being retrieved as `json`. This means the code doesn't get ahead of itself and try to use the information before PokeAPI has sent it back! There will be more about JSON in the next step, so we're going to skip over it for now.

Now that you can `fetch` and store one Pokémon, it's time to get a bunch of them (gotta catch 'em all!). As you might guess, this involves a `for` loop! 

--- task ---
Add another function in to call your previous one, like this:

```JavaScript
  async function fetchManyPokemon(pokemonCount) {
    for(var i = 1; i <= pokemonCount; i++){
      await fetchPokemon(i);
    }
  }
```
--- /task ---

Notice that, because you're fetching Pokémon by their IDs, which start from `1`, your `for` loop needs to start from `1` instead of the usual `0`.

--- task ---
Get the image for the Pokémon, download it into JavaScript (this bit is unusual, but you'll see why later!) and store it in an array. The function to get a single Pokémon image, given the information about it that you've stored in `pokemonInfo` looks like this:

  ```JavaScript
  async function fetchPokemonImage(pokemonInfo) {
    var imageUrl = pokemonInfo.sprites.front_default;
    
    var imageResponse = await fetch(imageUrl);
    var image = await imageResponse.blob();
    
    var base64 = await getBase64(image);
    
    pokePics.push(base64);
  }
  ```
--- /task ---

What this does is get the URL the image is living at (PokeAPI gave you that as part of the response, earlier), then, just like `fetchPokemon`, it will `fetch` the response (see that it's `await`-ing it again!) and then take the `blob` of the response. Image files, like the `.png` files you're getting here, are `blob` files. What this means, basically, is that they're not text files. Then it converts the blob into text with `getBase64` and stores that textin the `pokePics` array.

--- task ---
Now that you can `fetch` one image, do the same for every Pokémon you've got. Just like before, this is a `for` loop that calls your `function`, but a normal one since you're looping over an array. Notice that it's using `await` again, since there's a `fetch` inside the function it's **calling**. Also, notice that the **parameter** passed to `fetchPokemonImage` is one value from `pokemonInfo`, selected based on the value of `i`.
```JavaScript
  async function fetchPokemonImages() {
    for(var i = 0; i < pokemonInfo.length; i++){
      await fetchPokemonImage(pokemonInfo[i]);
    }
  }
```
--- /task ---

--- task ---
Now, wrap all the fetching functions you've written up into one called `getPokemon`, like this:

```JavaScript
  async function getPokemon(pokemonCount){
      pokemon = [];
      await fetchManyPokemon(pokemonCount);
      await fetchPokemonImages();
  }
```
--- /task ---


Finally, you need to create a `function` that will call your other functions and display some output so you can check everything worked. Since your other functions are `async`, this one has to be too, and has to `await` them. 

--- task ---
Add this at the very bottom of your file and then run it:
```JavaScript
  async function buildDex(pokemonCount){
    await getPokemon(pokemonCount);
    
    var display =  document.getElementById("display");
    display.innerHTML = "";
    var image = document.createElement("img");
    image.src = pokePics[0];
  }

  buildDex(1)
```
--- /task ---

If everything worked there should be a bit of a wait while the information gets loaded and then you'll see a picture of a Pokémon!