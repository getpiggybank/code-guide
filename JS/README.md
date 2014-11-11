# Piggybank's JavaScript Code Guide

At Piggybank we don't have crazy micro-managy rules on writing JavaScript like [Airbnb](https://github.com/airbnb/javascript). Those guides are gigantic and they take quite a bit of time to study. Instead, we have Three Truths when writing JavaScript:

1. Consistent
2. Explicit
3. Autonomous

## Consistent
#### tl;dr keep the code you add looking like the existing code

The first Truth is keeping code _consistent_. When writing code in an existing file the next engineer looking at the file should have no idea who wrote what line. That means, if all event handlers in the file are named like `eventHandler` such as `clickHandler`, `changeHandler`, etc, and you want to add a `mouseover` handler, don't add a method called `handleMouseover`.

This overrides any style guidelines as well if it's not an easy change. Even though we _suggest_ writing camel-case acronyms in the form of `fooId` over `fooID`, if a project uses `fooID` instead everywhere _use that_. Don't send a PR with a find and replace of every instance of this changed and don't write `fooId` mixed with `fooID`. 

> I’ve learned from experience that if you work harder at it, and apply more energy and time to it, and more consistency, you get a better result.

_- Louis C. K._

## Explicit
#### tl;dr Don't be clever with your code

The second Truth is make sure the code you write is _explicit_. It should be clear what the code is doing. No magic, tricks or cleverness. Try to let your code read like a book. The more jumping around other people working on your code have to do the more frustrated they'll get and the more repeated reading the more foolish they will feel. There will always be lines of code that take many reads to understand, but if you can avoid it stay with being explicit about what the code is doing. Let's take a look at a piece of example code that people may consider "clever" and short:

```js
// Fade in Widget if it has new data, otherwise fade it out
Widget["fade" + (dataAdded ? "In" : "Out" )]();
```

If there was an error on that line of code it could easily take you a couple tries to get what's going on. There's a lot more guessing that needs to happen on this line and some jumping around. Let's rework this to be a few more lines, but much easier to parse by a human:

```js
if (hasNewData) {
  Widget.fadeIn();
}
else {
  Widget.fadeOut();
}
```

Why is the last piece of code better than the first? 

1) The comment isn't even needed here.

2) The `hasNewData` variable is wordier, but it makes it obvious that it will be a boolean type. `dataAdded`, although just two words instead of three, leaves its reader with a guess: is this an object or an array of the new data, or is it saying that there was new data added and therefore a boolean?

3) You can read this code in plain english from top to bottom: if `hasNewData` is `true`, fade in the Widget. Else, fade it out.

This does not mean using a ternary is bad or that you need to push it to the extreme and do `new Object()` when creating an Object. It simply means, use your best judgement to decide if the code you're writing is too clever or not. If you get done writing a piece of code and you think "wow, I can't believe doing it this way works", you probably should _not_ be doing it that way.

> It is no matter whether it be right or wrong, so as it be explicit.

_- Jeremy Bentham_

## Autonomous
#### tl;dr try to take all the code you write and put them in tiny independent modules

The final truth falls along the lines of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), but takes it a bit further than that. Not only should code not repeat itself, it should be _autonomous_ and work on its own whenever possible. Always be asking yourself, "could this code I'm DRYing up become an independent, reusable module?" and if it can be, _do that_. Even if its only a couple lines, you will not only save yourself time by being able to just `require()` that small method in other modules later, other engineers building other features can save an enormous amount of time by just `require()`ing code into their new modules. 

These small, single-task, autonomous modules increase the velocity of understanding code by requiring you to only ingest small amount of logic at a time verse opening a file with 2,000LoC and just seeing a wall of code. That is a huge mental strain and keeps you less focused. Instead, you want to be able to write code that, when an error occurs, the error happens in a file with just a dozen or less lines of code. 

> The good person is they who rule themselves as they do their own property: their autonomous being is modelled on material power.

_-Theodor Adorno_
