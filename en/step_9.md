## Challenges!

Here are a few ideas on where you could take the project next, if you want to keep working on it. Pick one that interests you and give it a try! If you get stuck, try asking a more experienced coder or searching online.

### Pick a different starting point
Start your list somewhere else in the Pokédex, say from number 100.

--- hints ---
--- hint ---
You'll need to take a new input — the starting position in the list of all Pokémon — and use it and the number of Pokémon you want to work out the right ids.
--- /hint ---
--- hint ---
You'll need to update the `localStorage` code to check for not just the right number of Pokémon, but also the right ids. You can be clever, though. You don't have to check all of them!
--- /hint ---
--- hint ---
You should only need to make changes to two functions: `getPokemon` and `fetchManyPokemon`.
--- /hint ---
--- /hints ---


### Make the filters work together
The two filters don't work together at the moment. So, for example, if you filter to 'flying' and search for 'char' you find all three 'char' Pokémon instead of just Charizard, the only one with the 'flying' type. This is a tricky problem to solve (it took me a few tries!) and it might help to work out the different conditions on a piece of paper first.

--- hints ---
--- hint ---
You'll need to change both of the filter functions.
--- /hint ---
--- hint ---
You'll need to move bits of each function into the other: You'll have to check the type filter in the text search, and the text value in the type search.
--- /hint ---
--- hint ---
You'll need to add a bunch of extra `if` statements inside your existing `if` statements, to check whether things left visible by the first filter are sill left visible by the second.
--- /hint ---
--- /hints ---