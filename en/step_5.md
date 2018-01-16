## Making a Pokémon

Now you're going to make your own **JSON** object. It's going to be a simple version of a Pokémon. What you're going to need to build a basic Pokédex is listed below. I figured out this list by looking at the **JSON** of one Pokémon using the tool you saw on the last card.
  * The Pokémon's id number
  * Name of the Pokémon
  * A picture of it
  * Its “types” (fire, grass, water, etc.)
  
The Pokémon will be a kind of **object**, just like the ToDo was in the Intermediate JavaScript Sushi Cards. 

+ You can use a `function` to create and `return` an **object**, which lets you keep all the code related to that object neatly organised together. Add this function to your code to do so:

```JavaScript
  function Pokemon(pokemonIndex) {
    var info = pokemonInfo[pokemonIndex]
    
    this.id = info.id
    this.name = info.name
    this.image = pokePics[pokemonIndex]
  
  }
```

The code takes in the index (number in an array) of a Pokémon which it looks up and stores in the `info` **variable**. The `this` **keyword** is used to refer to **variables** attached to the specific Pokémon **object** you're creating. Every Pokémon will have an `id`, `name`, and `image`, so you need to refer to the specific ones attached to *this* Pokémon. What the code does here is take the `name` and `id` from the **JSON** about the Pokémon and the `image` from the **array** (`PokePics`) of images.

+ The next part is a bit trickier: A Pokémon can have more than one type, so you need to create a `types` **array** to store them, and then add them using a `for` **loop** that looks through the types in `info.types` and adds their names into `this.types`. You need to update the `function` you just wrote to add the code for types, like this:

```JavaScript
  function Pokemon(pokemonIndex) {
    var info = pokemonInfo[pokemonIndex]
    
    this.id = info.id
    this.name = info.name
    this.image = pokePics[pokemonIndex]
    
    this.types = []
    
    for(var i = 0; i < info.types.length; i++){
      var type = info.types[i].type.name
      this.types.push(type)
    }
    
  }
```

+ Now that you've got a `function` to make a Pokémon, you need another one that will make all the Pokémon, by calling this `function` as many times as you have Pokémon. As you can probably guess, that's another `for` loop! Aren't `for` loops great?

```JavaScript
  function makePokemonList(pokemonCount) {
    for(var i = 0; i < pokemonCount; i++){
      pokemon.push(new Pokemon(i))
    }
  }
```

Notice how the `new` **keyword** is used to create a `Pokemon` object, using your `Pokemon` `function`. That `new` is telling **JavaScript** that the `Pokemon` function is making an **object**, rather than just doing series of instructions, so it will treat it a little differently. This is why the `Pokemon` **object** gets stored in the `pokemon` **array**, rather than a reference to the `Pokemon` `function`.

+ Add a call to `makePokemonList` to `getPokemon`, passing the number of Pokémon you've fetched as the value of `pokemonCount`, like this:

```JavaScript
  async function getPokemon(pokemonCount){
      pokemon = []
      await fetchManyPokemon(pokemonCount)
      await fetchPokemonImages()
      await makePokemonList(pokemonCount)
  }
```