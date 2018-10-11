## Filtering Pokémon

Now you've got a pretty cool looking list of Pokémon displaying for you, it's time to add some tools to help users find the Pokémon they're looking for. You're going to create two of them: A filter based on the type of the Pokémon and, on the next page, a search based on its name. 

To be able to filter by type, you need to have a list of all they types that Pokémon in your list have. The easiest way to do this is to make JavaScript create the list for you, as an array. You do this by:
 1. Creating an empty array to store your types (`typesList`)
 2. Looping over each of the Pokémon
 3. Inside that loop, looping over each of the current Pokémon's types
 4. Then check if the type is *not* already in your list. The code for that is `typesList.indexOf(type) === -1`. If it was in the array this would return the **index** (position number) of the type.
 5. If it is not in the array, adding it
 
Also, you may want to sort the list of types A–Z to make finding a type easier for users. That's simple, as A–Z (or smallest to largest for numbers) is the default sort for JavaScript arrays, so you can just use `typesList.sort()`. 

--- task ---
Add this function to your code to create an alphabetically sorted list of types.

```JavaScript
  function getTypesList() {
    var typesList = [];
    for(var i = 0; i < pokemon.length; i++){
      for(var j = 0; j < pokemon[i].types.length; j++){
        var type = pokemon[i].types[j];
        if(typesList.indexOf(type) === -1){
          typesList.push(type);
        }
      }
    }
    typesList.sort(); // alphabetize the list, to find things easily
    return typesList;
  }
```
--- /task ---



Now that you have the types list, you need to put it in the HTML `<select>` tag, with the `type-picker` id, that users will use to pick types. At the moment, there's a single `<option>` tag inside it and that just says 'Loading' so users know not to use it until it's ready. You have to insert `<option>` tags for all of the types, as well as an 'all' option, so they can see all the Pokémon. Notice that `<option>` tags don't just contain the type as text to display (the `TextNode`), but also as a `value` property, which is what code reading the option will use. 

You also need to add a listener — an instruction to JavaScript to wait for a particular event and then run a function — which will detect changes and run another function that you'll make in the next step, called `filterDexByType`. 


--- task ---
Add the this `createTypePicker` function to your code to update the options list and call `filterDexByType` when a change happens.

```JavaScript
  function createTypePicker() {
    var typePicker = document.getElementById("type-picker");
    var typesList = getTypesList();
    
    typePicker.innerHTML = "<option value=\"all\">all</option>";
    
    for(var i = 0; i < typesList.length; i++){
      var type = document.createElement("option");
      type.value = typesList[i];
      var typeName = document.createTextNode(typesList[i]);
      type.appendChild(typeName);
      typePicker.appendChild(type);
    }

    typePicker.addEventListener("change", filterDexByType);
  }
```
--- /task ---

Try testing the selection by adding an `alert` with the type. Don't forget to remove it once the filtering is working though!

Now you've got everything set up for your user to be able to tell the program what type they want to filter to. Time to actually filter things! 

The easiest way to do this is to just hide the Pokémon that don't match the filter, rather than adding or removing them. 

--- task ---
Hide a Pokémon's listing by changing the `style.display` property of the `<figure>` tag you created for it. To do this you'll need is a loop that takes the type and hides each Pokémon that matches it. You can get the type from the `this.value` property, since `this` will be referring to the HTML `<select>` tag that triggered the function. The value of the `<select>` tag is the value of the selected `<option>` tag.

Add this code to your program to do the hiding, then test it by selecting some types from the filter.

```JavaScript
  function filterDexByType(){
    var selectedType = this.value;

    for(var i=0; i < pokemon.length; i++){
      var fig = document.getElementById("pokemon-"+pokemon[i].id.toString());
      
      if(pokemon[i].types.indexOf(selectedType) === -1){
        if(selectedType === "all"){
          fig.style.display = "initial";
        }
        else{
          fig.style.display = "none";
        }
      }
      else {
        fig.style.display = "initial";
      }
    
    }

  }
```
--- /task ---

