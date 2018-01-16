## Searching Pokémon

Now you can filter to all the fire types, or whatever types you like (but fire types are the coolest, right? Charizard is awesome). Time to let your users search for their favourite Pokémon! 

+ This means connecting up the text box and the button I've included on the page for you. Their `id`s are `pokemon-name` and `pokemon-name-button`. The code just needs to listen for clicks on the button, take the `value` in `pokemon-name` and compare it to the `name` property of every Pokémon, to see if that name *contains* it, rather than perfectly matches it. So searching for “saur” should find bulbasaur, ivysaur and venusaur. You can test that using `.includes("saur")` on the **string** you're checking. That search function looks like this:

```JavaScript
  function searchDex(event) {
    event.preventDefault()
    var searchText = document.getElementById("pokemon-name").value
    for(var i=0; i < pokemon.length; i++){
      var fig = document.getElementById("pokemon-"+pokemon[i].id.toString())
      if(pokemon[i].name.includes(searchText)){
        fig.style.display = "initial"
      }
      else {
        fig.style.display = "none"
      }
    }
  }
```

+ The last thing you need to do is connect it up to the click listener. There's not really a great place to do that in the code, so just stick it in the end of `buildDex`, since it's part of setting up the page. Like this:

```JavaScript
  async function buildDex(pokemonCount){
    await getPokemon(pokemonCount)
    displayPokemonList()
    createTypePicker()
    document.getElementById("pokemon-name-button").addEventListener("click",searchDex)
  }
```

That's it! You've got a fully working Pokédex! Check out the next card for some ideas on how you can improve the project on your own.