## The Life Of Dino

![The Life Of Dino Screenshot](https://raw.githubusercontent.com/abdalmoniem/TheLifeOfDino/master/assets/screenshot.png)

A simple artificial intelligence to teach Google Chrome's offline dinosaur to
jump cactus, using a simple Genetic Algorithm.

## Installation:
1. Install `Node.js` on your computer.
2. Clone/download this folder to your computer.
3. run `npm install` within this folder
4. Open Chrome's dinosaur game and put aside the terminal (It MUST be on the same screen)
	**(Tip: go to developer tools, and under network, set to offline )**
5. run `node index` within this folder. If the game was located, it will move the cursor
   of the mouse to the origin of the `floor` of the dino. Press `s` key in the terminal to 
   start learning. 

## How does it work:
We have 3 different inputs to be read from the pixels of the screen:

1. Distance to the next cactus
2. Length of the next cactus
3. Speed of the incomming cactus

We also have, one output with 3 possible states:

1. output < 0.45: Press DOWN key
2. output > 0.55: Press UP key
3. default: Release both keys

## Genetic Algorithm:
Each Generation consists of 12 neural networks (Genomes). 

Each genome is tested with the game, by constantly mapping the read 
inputs from  the game to the inputs of the neural network, and by getting
the output/activation from the network and applying to the keys of the
keyboard.

While testing each genome, we keep track of it's "fitness" by counting
jumped cactus in the game.

When an entire generation is completed, we remove the worst genomes until
achieving `N` genomes. With those `N` genomes, we then select two randomly,
and cross-over their values/configurations. After that, we apply random mutations
in the values/configurations of the Neural Network, creating a new genome.

We do the cross-over/mutation until we get 12 genomes again, and repeat it constantly.


## Implementation:
All the implementation was done using Node.js, with Synaptic (Neural Network library),
and RobotJs (a library to read pixels and simulate key presses).

There are a few files in the project:

- `start.js`: It tight all things together.

- `Scanner.js`: Basic abstraction layer above RobotJs library that reads the screen like
  ray tracing. It also has some utility functions.

- `UI.js`: Global scope for the UI management. It initializes and also updates the screen
  on changes.

- `GameManipulator.js`: Has all the necessary code to read sensors, and apply outputs
  to the game. Is also responsible for computing points, getting the game state and
  triggering callbacks/listeners to real implementation.

- `Learner.js`: It is the core implementation of the Genetic Algorithm. This is where
  "magic" happens, by running generations, doing "natural" selection, cross-over, mutation and so on...


## How to Load a genome:
1. Make sure Genome is inside `genomes` folder with a `.json` extension
2. Run the program
3. Click the list in the terminal
4. Navigate up/down to the wanted file
5. Press `enter` (then, to start, press `s`)


## Be aware of a game bug:
The dino game has an anoying bug: It starts to "drift" to the right with time
making the dino to be wrong offseted from the origin of the game. That, makes
the program to read the dino as a cactus, since it is the same color.

You can fix that by continuously refreshing the page, or, by pasting this code inside the 
console in the element inspector:

```js
setInterval(function (){Runner.instance_.tRex.xPos = 21}, 2000)
```
