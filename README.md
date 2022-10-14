# Documentation for Jetej

# Code Blocks
Jetej composes of a `<game>` block, followed by any number of `<object>`, `<event>` and `<function>` blocks. 

Each block must start with `<>` and end with a `;`

These are the built-in attributes: 

### `<game>`
 - `background` an image or a colour
 - `score`
 - `init` function call(s)

    Eg: `init: spawn(Player, 50, 50), spawn(Box, 400, 200)`

### `<object>`
 - `name` *requried*
 - `image`
 - `life`
 - `speed x` 
 - `speed y`
 - `width`
 - `height` 
 - `mass` 
 - `bounce`
 - `have collision`
 - `update` function call(s)

### `<event>`
 - `object1` name of an object. *requried*
 - `object2` name of an object. *requried*
 - `actions` function call(s). *requried* 


### `<function>`
 - `name` *requried*
 - `param` *requried*; parameter(s). 
 - `body` *requried*; instructions wrapped in `{` and `}`.
    can be function calls, ifs or variable assignments

# Built-in Functions

 - `random(num, num)`
 - `random(num)`
 - `spawn(name, x, y)`
 - `delete(object)`
 - `score(amount)`
 - `basicControls()` move using arrow keys or `W` `A` `S` `D`, requires user to press down the key for the object to move
 - `directionControls()` makes a moving object 'turn' to a direction
 - `winGame()`
 -`loseGame()`


# Examples 
## Hello World

```
<game>
init: spawn(Player,50,50)
;
 
<object>
name: Player
image: circle
update: basicControls()
;
```
This creates a circle that the payer can control with arrow keys or `W` `A` `S` `D`

## Box collector game
```
<game>
score: 0
init: spawn(Player, 50, 50), 
spawn(Box, 400, 200),
spawn(Wall, -10,0), 
spawn(Wall, 500, 0),
spawn(Bound, 10, 0),
spawn(Bound, 0, 300);

 
<object>
name: Player
image: hexagon
speed x: 50
update: directionControls(), checkEnd();
 
<object>
name: Box
image: square
have collision: false;

<object>
name: Tri
image: triangle;
have collision: false;

<object>
name: Wall
image: circle
width: 10
height: 300;

<object>
name: Bound
image: circle
width: 500
height: 10;

<event>
object1: Player
object2: Box
actions: delete(object2), 
spawn(Tri, random(10, 500) , random(10, 300) ), 
spawn(Box, random(10, 500) , random(10, 300) ), 
score(1);


<event>
object1: Player
object2: Tri
actions: delete(object2), 
spawn(Tri, random(10, 500) , random(10, 300)), 
score(-1);


<function>
name: checkEnd
param: i
body: 
{
    if (game.score > 3, winGame())
    if (game.score < 0, loseGame())
};
```