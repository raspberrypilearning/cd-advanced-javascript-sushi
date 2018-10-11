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


* Speed up increasing the list size. Right now every Pokémon is re-loaded to `localStorage` if you add one. How can you be smarter about that?

* Right now, the two filters don't work together. So if you filter to “flying” and search for “char” you find all three “char” Pokémon instead of just Charizard, the only one with the “flying” type. Fix that!

* Try adding more filters, using the **JSON** viewer from the “What is JSON?” card to pick some interesting values and creating some filters based on them like on the “Filtering Pokémon” card.