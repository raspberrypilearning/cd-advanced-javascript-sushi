## Displaying Pokémon

Now that you have a list of Pokémon and they're saved and quick to reload, it's time to start working on displaying them! This is mostly about creating **HTML** elements with the content from your Pokémon **objects** in them. It would be helpful to have completed some of the HTML/CSS Sushi Cards, but if you haven't don't worry, this isn't really the same as writing **HTML**. This is telling **JavaScript** to do it for you! 

I've already provided some **CSS** that will handle laying things out for you, as well as the bits of a HTML **form** that you'll need later. 

+ For now, create a `function` that will let you create, instead of the single image of the first Pokémon you've got right now, a more detailed display of any Pokémon you **pass** it. To do this you're going to be creating a **HTML** **element** called a `figure` with an `img` (image) **element** and a `figcaption` (figure caption) **element** inside it. Your image will, naturally, be the picture of the Pokémon. The caption will be the name. I've included comments here (the lines starting with `//`) but you don't need to copy them into your code. They're just there to explain what's happening, as this is more complex than **HTML** creation you may have seen before. It's long, but it's just doing very similar things—creating **HTML** **elements**, setting some **properties** on them and placing them inside each other—a few times. 

```JavaScript
  function makePokemonHTML(pokemon) {
    // Create a figure element
    var figure = document.createElement("figure")
    
    // Give the figure an id based on the Pokémon's id
    // you can use this to select the figure later
    // notice that .toString() is used to convert the number to a string
    figure.id = "pokemon-"+pokemon.id.toString()
    
    // Create an img (image) element
    var image = document.createElement("img")
    
    // Set the src (source) of that element to be the image of the Pokémon
    image.src = pokemon.image
    
    // Create a figcaption element
    var caption = document.createElement("figcaption")
    
    // Create a TextNode (piece of text) that includes the name of the Pokémon
    var pokeName = document.createTextNode("#"+pokemon.id+": "+pokemon.name)

    // Put the "pokeName" TextNode inside the "caption" figcaption tag
    caption.appendChild(pokeName)
    
    // Put the "image" img tag inside the "figure" figure tag
    figure.appendChild(image)

    // Put the "caption" figcaption tag inside the "figure" figure tag
    figure.appendChild(caption)
    
    // Hand back the completed piece of HTML
    return figure
  }
```

+ Now you need a `function` that will loop through the Pokémon you've got and make **HTML** for each of them, `append`-ing it to the displayed list of Pokémon each time. This one's a bit simpler, but I've still included some comments to help. Again, you don't need to include them in your own code!

```JavaScript
  function displayPokemonList() {
    // Select the HTML tag with the id "display"
    // This is a tag I made for you and included in index.html
    var display =  document.getElementById("display")
    
    // Set all the HTML inside that tag to the empty string
    // that is, delete it.
    display.innerHTML = ""
    
    // For each Pokémon in the pokemon array,
    // make HTML using makePokemonHTML and then
    // put that HTML inside the display tag.
    // Note that the append tag will put the latest tag
    // in last. So they'll appear in the order they are in
    // in the pokemon array.
    for(var i = 0; i < pokemon.length; i++) {
      display.appendChild(makePokemonHTML(pokemon[i]))
    }
  }
```

+ Finally, replace the code you've got for displaying a single Pokémon in `buildDex` with code that calls `displayPokemonList` like so:

```JavaScript
  async function buildDex(pokemonCount){
    await getPokemon(pokemonCount)
    displayPokemonList()
  }
```
