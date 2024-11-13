### Meta
2024-11-12 21:22
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Starting the Game Project
We’ll begin building the game by creating an empty Pygame window. Later, we’ll draw the game elements, such as the ship and the aliens, on this window. We’ll also make our game respond to user input, set the background color, and load a ship image.

#### Creating a Pygame Window and Responding to User Input
We’ll make an empty Pygame window by creating a class to represent the game.

```Python title:alien_invasion.py
import sys

import pygame

class AlienInvasion:
	"""Overall class to manage game assets and behavior."""

	def __init__(self):
		"""Initialize the game, and create game resources."""
		pygame.init()

		self.screen = pygame.display.set_mode((1200, 800))
		pygame.display.set_caption("Alien Invasion")

	def run_game(self):
		"""Start the main loop for the game."""
		while True:
			# Watch for keyboard and mouse events.
			for event in pygame.event.get():
				if event.type == pygame.QUIT:
					sys.exit()

			# Make the most recently drawn screen visible.
			pygame.display.flip()

if __name__ == '__main__':
	# Make a game instance, and run the game.
	ai = AlienInvasion()
	ai.run_game()
```

*Alien Invasion* starts as a class called `AlienInvasion`. In the `__init__()` method, the `pygame.init()` function initializes the background settings that Pygame needs to work properly. Then, we call `pygame.display.set_mode()` to create a display window to serve as drawing board for the graphical elements. The argument `(1200, 800)` is a tuple that defines the dimensions of the game window, which will be $1200 \cdot 800 px$. We assign this window to the attribute `self.screen`, so it will be available in all methods in the class.

The object assigned to `self.screen` is called a *surface* – a part of the screen where a game element can be displayed. Each element in the game is its own surface. The surface returned by `display.set_mode()` represents the entire game window. When activating the game loop, this surface will be redrawn on every pass through the loop, so it can be updated with any changes triggered by user input.

The game is controlled by the `run_game()` method. This contains a `while` loop that runs continually. The `while` loop contains an event loop and code that manages screen updates. An *event* is an action that the user performs while playing the game, such as pressing a key or moving the mouse. To make our program respond to events, we write an *event loop* to *listen* for events and perform appropriate tasks depending on the kinds of events that occur. The `for` loop nested inside the `while` loop is an event loop.

To access the events that Pygame detects, we’ll use the `pygame.event.get()` function. This function returns a list of events that have taken place since the last time this function was called. Any keyboard or mouse event will cause this `for` loop to run. Inside the loop, we’ll write a series of conditional statements to detect and respond to specific events. For example, when the player clicks the game window’s close button, a `pygame.QUIT` event is detected and we call `sys.exit()` to exit the game.

The call to `pygame.display.flip()` tells Pygame to make the most recently drawn screen visible. tells Pygame to make the most recently dranw swn screen visible. In this case, it simply draws an empty screen on each pass through the `while` loop, erasing the old screen so only the new screen is visible. When we move the game elements around, `pygame.display.flip()` continually updates the display to show the new positions of game elements and hide the old ones, creating the illusion of smooth movement.

At the end of the file, we create an instance of the game and then call `run_game()`. We place `run_game()` in an `if` block that only runs if the file is called directly. When you run this `alien_invasion.py` file, you should see an empty Pygame window.

#### Controlling the Frame Rate
Ideally, games should run at the same speed, or *frame rate*, on all systems. Controlling the frame rate of a game that can run on multiple systems is a complex issue, but Pygame offers a relatively simple way to accomplish this goal. We’ll make a clock, and ensure the clock ticks once on each pass through the main loop. Any time the loop processes faster that the rate we define, Pygame will calculate the correct amount of time to pause so that the game runs at a consistent rate.

We’ll define the clock in the `__init__()` method:
```Python title:alien_invasion.py
	def __init__(self):
		"""Initialize the game, and create game resources."""
		pygame.init()

		self.clock = pygame.time.Clock()
		--snip--
```

After initializing `pygame`, we create an instance of the class `Clock`, from the `pygame.time` module. Then we’ll make the clock tick at the end of the `while` loop in `run_game()`:
```Python title:alien_invasion.py
	def run_game(self):
		"""Star the game loop."""
		while True:
			--snip--
			pygame.display.flip()
			self.clock.tick(60)
```

The `tick()` method takes one argument: the frame rate for the game. Here, we’re using `60` as a value, so Pygame will do its best to make the loop run exactly 60 times per second.

**Note:** Pygame’s `clock` should help the game run consistently on most systems. If it makes the game run less consistently on your system, you can try different values for the frame rate. If you can’t find a good frame rate, you can leave clock out entirely and adjust the game’s settings so it runs well on your system.

#### Setting the Background Color
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		pygame.display.set_caption("Alien Invasion")

		# Set the background color
		self.bg_color = (230, 230, 230)

	def run_game(self):
		--snip--
			for event in pygame.event.get():
				if event.type == pygame.QUIT:
					sys.exit()

			# Redraw the screen during each pass through the loop.
			self.screen.fill(self.bg_color)

			# Make the most recently drawn screen visible.
			pygame.display.flip()
			self.clock.tick(60)
```

Colors in Pygame are specified as [[color_model_rgb|RGB colors]]. The color value `(230, 230, 230)` mixes equal amounts of red, blue, and green, which produces a light gray background color. We assign this color to `self.bg_color`.

We fill the screen with the background color using the `fill()` method, which acts on a surface and takes only one argument: a color.

#### Creating a Settings Class
Create a new file named *settings.py* inside the *alien_invasion* directory, and add this initial `Settings` class:
```Python title:settings.py
class Settings:
	"""A class to store all settings for Alien Invasion."""

	def __init__(self):
		"""Initialize the game's settings."""
		# Screen settings
		self.screen_width = 1200
		self.screen_height = 800
		self.bg_color = (42, 39, 63)
```

To make an instance of `Settings` in the project and use it to access our settings, we modify *alien_invasion.py* as follows:
```Python title:alien_invasion.py
--snip--
import pygame

from settings import Settings

class AlienInvasion:
	"""Overall class to manage game assets and behavior"""

	def __init__(self):
		"""Initialize the game, and create game resources."""
		pygame.init()
		self.clock = pygame.time.Clock()
		self.settings = Settings()

		self.screen = pygame.display.set_mode(
			(self.settings.screen_width, self.settings.screen_height))
		pygame.display.set_caption("Alien Invasion")

	def run_game(self):
		--snip--
		# Redraw the screen during each pass through the loop.
		self.screen.fill(self.settings.bg_color)

		# Make the most recently drawn screen visible.
		pygame.display.flip()
		self.clock.tick(60)
--snip--
```