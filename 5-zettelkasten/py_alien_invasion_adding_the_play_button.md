### Meta
2024-12-23 11:17
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_scoring]]
**Status:** #completed 

### Adding the Play Button
In this section, we’ll add a Play button that appears before a game begins and reappears when the game ends so the player can play again.

Right now, the game begins as soon as your run *alien_invasion.py*. Let’s start the game in an interactive state and then prompt the player to click a Play button to begin. To do this, modify the `__init__()` method of `AlienInvasion`:
```Python title:alien_invasion.py
	def __init__(self):
		"""Initialize the game, and create game resources."""
		pygame.init()
		--snip--

		# Start Alien Invasion in an inactive state.
		self.game_active = False
```

Now the game should start in an inactive state, with now way for the player to start it until we make a Play **button**.

#### Creating a Button Class
Because Pygame doesn’t have a built-in method for making buttons, we’ll write a `Button` class to create a filled rectangle with a label. You can use this code to make any button in a game.
```Python title:button.py
import pygame.font

class Button:
	"""A class to build buttons for the game."""

	def __init__(self, ai_game, msg):
		"""Initialize button attributes."""
		self.screen = ai_game.screen
		self.screen_rect = self.screen.get_rect()

		# Set the dimensions and properties of the button.
		self.width, self.height = 200, 50
		self.button_color = (0, 135, 0)
		self.text_color = (255, 255, 255)
		self.font = pygame.font.SysFont(None, 48)

		# Build the button's rect object and center it.
		self.rect = pygame.Rect(0, 0, self.width, self.height)
		self.rect.center = self.screen_rect.center

		# The button message needs to be prepped only once.
		self._prep_msg(msg)
```

First, we import the `pygame.font` module, which lets Pygame render text to the screen. The `__init__()` method takes the parameters `self`, the `ai_game` object, and `msg`, which contains the button’s text. We set the button dimensions, color and text color.

Next, we prepare a `font` attribute for rendering text. The `None` argument tells Pygame to use the default font, and `48` specifies the size of the text. To center the button on the screen, we create a `rect` for the button and set its `center` attribute to match that of the screen.

Pygame works with text by rendering the string you want to display as an image. Finally, we call `_prep_msg()` to handle this rendering. Here’s the code for `_prep_msg()`:
```Python title:button.py
	def _prep_msg(self, msg):
		"""Turn msg into a rendered image and center text on the button."""
		self.msg_image = self.font.render(msg, True, self.text_color, self.button_color)
		self.msg_image_rect = self.msg_image.get_rect()
		self.msg_image_rect.center = self.rect.center
```

The `_prep_msg()` method needs a `self` parameter and the text to be rendered as an image (`msg`). The call to `font.render()` turns the text stored in `msg` into an image, which we then store in `self.msg_image`. The `font.render()` method also takes a Boolean value to turn antialiasing on or off (*antialiasing* makes the edges of the text smoother). The remaining arguments are the specified font color and background color. We set antialiasing to `True` and set the text background to the same color as the button. (If you don’t include a background color, Pygame will try to render the font with a transparent background).

We center the text image on the button by creating a `rect` from the image and setting its `center` attribute to match that of the button.

Finally, we create a `draw_button()` method that we can call to display the button on screen:
```Python title:button.py
	def draw_button(self):
		"""Draw blank button and then draw message."""
		self.screen.fill(self.button_color, self.rect)
		self.screen.blit(self.msg_image, self.msg_image_rec)
```

We call `screen.fill()` to draw the rectangular portion of the button. Then we call `screen.blit()` to draw the text image to the screen, passing it an image and the `rect` object associated with the image. This completes the `Button` class.

#### Drawing the Button to the Screen
We’ll use the `Button` class to create a Play button in `AlienInvasion`. First, we’ll update the import statements:
```Python title:alien_invasion.py
--snip--
from game_stats import GameStats
from button import Button
```

Because we need only one Play button, we’ll create it in the `__init__()` method of `AlienInvasion`. We can place the code at the end:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		self.game_active = False

		# Make the Play button.
		self.play_button = Button(self, "Play")
```

This creates an instance of `Button` with the label `Play`, but it doesn’t draw the button to screen. To do this, we’ll call the button’s `draw_button()` method in `_update_screen()`:
```Python title:alien_invasion.py
	def _update_screen(self):
		--snip--
		self.aliens.draw(self.screen)

		# Draw the play button if the game is inactive.
		if not self.game_active:
			self.play_button.draw_button()

		pygame.display.flip()
```

To make the Play button visible above all other elements on the screen, we draw it after all the other elements have been drawn but before flipping to a new screen. We include it in an `if` block, so the button only appears when the game is inactive.

#### Starting the Game
To start a new game when the player clicks Play, add the following `elif` block to the end of `_check_events()` to monitor mouse events over the button:
```Python title:alien_invasion.py
	def _check_events(self):
		"""Respond to keypresses and mouse events."""
		for event in pygame.event.get():
			if event.type == pygame.QUIT:
				--snip--
			elif event.type == pygame.MOUSEBUTTONDOWN:
				mouse_pos = pygame.mouse.get_pos()
				self._check_play_button(mouse_pos)
```

Pygame detects a `MOUSEBUTTONDOWN` event when the player clicks anywhere on the screen, but we want to restrict our game to respond to mouse clicks only on the Play button. To achieve this, we use `pygame.mouse.get_pos()`, which returns a tuple containing the mouse cursor’s *x*- and *y*-coordinates when the mouse button is clicked. We send these values to the new method `_check_play_button()`:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		"""Start a new game when the player clicks Play."""
		if self.play_button.rect.collidepoint(mouse_pos):
		self.game_active = True
```

We use the `rect` method `collidepoint()` to check whether the point of the mouse click overlaps the region defined by the Play button’s `rect`.

#### Resetting the Game
The Play button code we just wrote works the first time the player clicks Play. But it doesn’t work after the first game ends, because the conditions that caused the game to end haven’t been reset.

To reset the game each time the player clicks Play, we must reset the game statistics, clear out the old aliens and bullets, build a new fleet, and center the ship, as show here:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		"""Start a new game when the player clicks Play."""
		if self.play_button.rect.collidepoint(mouse_pos):
		# Reset the game statistics.
		self.stats.reset_stats():
		self.game_active = True

		# Get rid of any remaining bullets and aliens.
		self.bullets.empty()
		self.aliens.empty()

		# Create a new fleet and center the ship.
		self._create_fleet()
		self.ship.center_ship()
```

#### Deactivating the Play Button
One issue with the Play button is that the button region on the screen will continue to respond to clicks even when the Play button isn’t visible. To fix this, set the game to start only when `game_active` is `False`:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		"""Start a new game when the player clicks Play."""
		button_clicked = self.play_button.rect.collidepoint(mouse_pos)
		if button_clicked and not self.game_active:
			# Reset the game statistics.
			self.stats.reset_stats()
			--snip--
```

The flag `button_clicked` stores a `True` or `False` value, and the game will restart only if Play is clicked *and* the game is not currently active.

#### Hiding the Mouse Cursor
We want the mouse cursor to be visible when the game is inactive, but once play begins, it just gets in the way. To fix this, we’ll make it invisible when the game becomes active. We can do this at the end of the `if` block in `_check_play_button()`:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		"""Start a new game when the player clicks Play."""
		button_clicked = self.play_button.rect.collidepoint(mouse_pos)
		if button_clicked and not self.game_active:
			--snip--
			# Hide the mouse cursor.
			pygame.mouse.set_visible(False)
```

Passing `False` to `set_visible()` tells Pygame to hide the cursor when the mouse is over the game window.

We’ll make the cursor reappear once the game ends so the player can click Play again to begin a new game. Here’s the code to do that:
```Python title:alien_invasion.py
	def _ship_hit(self):
		"""Respond to ship begin hit by alien."""
		if self.stats.ships_left > 0:
			--snip--
		else:
			self.game_active = False
			pygame.mouse.set_visible(True)
```

We make the cursor visible again as soon as the game becomes inactive, which happens in `_ship_hit()`. Attention to details like this makes your game more professional looking and allows the player to focus on playing, rather than figuring out the user interface.