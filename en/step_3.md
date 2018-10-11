## What is JSON?

As proimsed, this step will look at **JSON**. You won't be writing any actual code here, just learning about this very important part of JavaScript. If you've already done the Intermediate JavaScript Sushi, you've worked with JSON before and even created some.

So let's look at some from the Intermediate cards first:

```JavaScript
var toDos =   [
                {
                  text: "My",
                  completed: false
                },
                {
                  text: "to-do",
                  completed: true
                },
                {
                  text: "list",
                  completed: true
                }
              ]
```

JSON stands for **JavaScript Object Notation** and it's basically just bits of JavaScript used to store and send information. In the snippet above you've got an array with some to-do objects in it. Each object has a few variables with values. If you wanted to look up the `text` of the first one you could do so with `toDos[0].text`. You could look up the `completed` value of the second one with `toDos[1].completed`.

You use JSON whenever you want to store information that is somehow connected. For example, if you have a list of information about a sports team, you might want to store things like:
  * Their name, as a text variable.
  * Which league they play in, probably as a JSON object (you can **nest** them inside each other) with the name of the league and the URL where you can find even more JSON with the full info on the league, like a list (array) of all the teams in it. If the team is in more than one league, say a soccer team in the Premiership and the Champions' League, then you'd have an array of those league objects.
  * An array of player objects, including things like their name, age, position, etc.
  * A fixtures array, with the dates and times of their upcoming games and the name and URL (to the same kind of JSON object) for the team they're playing against.
  * Maybe an array of history: which games and leagues they won and when.

You can see that this can quickly turn into a large set of files, linked to each other by URLs that can tell you, or your program, a lot about a subject. You could use this imaginary JSON API to make an app that showed you what matches were coming up this weekend and how those teams had fared when they played in the past. Or one that ranked all the teams in the league by things like wins/losses, score, number of players, etc. Notice that you're getting a lot more information than you're using in those apps, but that's normal with JSON that some other service is providing: They don't know exactly what kind of website or app you're building, so they give you _lots_ of info!

Now it's time to take a look at the JSON PokeAPI is sending you. Check out [dojo.soy/bulbasaur](http://dojo.soy/bulbasaur). I've pasted the JSON for Bulbasaur (Pokémon #1) into this online JSON viewer to make things a bit more readable for you. On the left, you can see the 9081 lines that make up the Bulbasaur JSON. On the right, you can see that as a tree you can click into, which a human being has a better chance of understanding! What's important to learn here is that you don't need to understand all of the JSON to use some of it. **I have not read all of Bulbasaur's file, and I never will.** However, I've written a program that uses it, and you're in the process of doing the same! Since you'll be storing this info in your program, technically, if you get 150 pokemon in there, you'll have over a million lines of code in your program!

On the next card, you're going to create a simpler JSON object for a Pokémon: a handful of lines that you can use to store and retrieve the information you really need.