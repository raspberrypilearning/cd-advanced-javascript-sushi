## Filtering Pokémon

Now you've got a pretty cool looking list of Pokémon displaying for you, it's time to add some tools to help users find the Pokémon they're looking for. You're going to create two of them: A filter based on the type of the Pokémon and a search based on its name. 

+ To be able to filter by type, you need to have a list of all they types that Pokémon in your list have. The easiest way to do this is to make **JavaScript** create the list for you, as an **array**. You do this by:
 1. Creating an empty **array** to store your types (`typesList`)
 2. Looping over each of the Pokémon
 3. Inside that loop, looping over each of the current Pokémon's types
 4. Then check if the type is *not* already in your list. The code for that is `typesList.indexOf(type) === -1`. If it was in the **array** this would return the **index** (position number) of the type.
 5. If it is not in the **array**, adding it
 
+ Also, you may want to sort it A–Z to make finding a type easier for users. That's simple, as A–Z (or smallest to largest for numbers) is the default sort for **JavaScript** **arrays**, so you can just use `typesList.sort()`. Here's the new `function` you should add to your code:

```JavaScript
  function getTypesList() {
    var typesList = []
    for(var i = 0; i < pokemon.length; i++){
      for(var j = 0; j < pokemon[i].types.length; j++){
        var type = pokemon[i].types[j]
        if(typesList.indexOf(type) === -1){
          typesList.push(type)
        }
      }
    }
    typesList.sort() // alphabetize the list, to find things easily
    return typesList
  }
```

+ Right, now you have that list, you need to update the HTML `<select>` tag, with the `type-picker` id, that users will use to pick types. Right now, there's a single `<option>` tag inside it and that just says “Loading” so users know not to use it until it's ready. You need to insert `<option>` tags for all of the types, as well as an “all” option, so they can see all the Pokémon. Notice that `<option>` tags don't just contain the type as text to display (the `TextNode`), but also as a `value` **property**. 

+ You then need to add a listener, like the ones used to detect clicks in the Intermediate JavaScript Sushi project, which will detect changes and run another `function` that you'll make in the next step, called `filterDexByType`. Here's the code for the `createTypePicker` function you'll use to do this:

```JavaScript
  function createTypePicker() {
    var typePicker = document.getElementById("type-picker")
    var typesList = getTypesList()
    
    typePicker.innerHTML = "<option value=\"all\">all</option>"
    
    for(var i = 0; i < typesList.length; i++){
      var type = document.createElement("option")
      type.value = typesList[i]
      var typeName = document.createTextNode(typesList[i])
      type.appendChild(typeName)
      typePicker.appendChild(type)
    }

    typePicker.addEventListener("change", filterDexByType)
  }
```

+ Try testing the selection by adding an `alert` with the type. Don't forget to remove it once the filtering is working though!

Now you've got everything set up for your user to be able to tell the program what type they want to filter to. Time to actually filter things! 

+ The easiest way to do this is to just hide the Pokémon that don't match the filter, rather than adding or removing them. You can do that by changing the `style.display` property of the `<figure>` **tags** you created. So what you'll need is a loop that takes the type You can get that from the `this.value` property, since `this` will be referring to the **HTML** tag that triggered the `function`. That tag is the `<select>` tag, whose value is the value of the selected `<option>` tag. The `function` to do this (and handle the special case of showing everything if “all” is selected) is below, and you can go ahead and add it, then test your filters!

```JavaScript
  function filterDexByType(){
    var selectedType = this.value

    for(var i=0; i < pokemon.length; i++){
      var fig = document.getElementById("pokemon-"+pokemon[i].id.toString())
      
      if(pokemon[i].types.indexOf(selectedType) === -1){
        if(selectedType === "all"){
          fig.style.display = "initial"
        }
        else{
          fig.style.display = "none"
        }
      }
      else {
        fig.style.display = "initial"
      }
    
    }

  }
```

