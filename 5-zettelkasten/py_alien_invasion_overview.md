### Meta
2024-11-12 21:20
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Planning Your Project
When you’re building a large project, it’s important to prepare a plan before you begin to write code. Your plan will keep you focused and make it more likely that you’ll complete the project.

#### Describing Alien Invasion
In *Alien Invasion*, the player controls a rocket ship that appears at the bottom center of the screen. The player can move the ship right and left using the arrow keys and shoot bullets using the spacebar. When the game begins, a fleet of aliens fills the sky and moves across and down the screen. The player shoots and destroys the aliens. If the player destroys all the aliens, a new fleet appears that moves faster than the previous fleet. If any alien hits the player’s ship or reaches the bottom of the screen, the player loses a ship. If the player loses three ships, the game ends.

For the first development phase, we’ll make a ship that can move right and left when the player presses the arrow keys and fire bullets when they press the spacebar. After that, we’ll move on to the aliens and refine the gameplay.

### Installing Pygame
```BASH title:example.sh
python -m pip install --user pygame
```

