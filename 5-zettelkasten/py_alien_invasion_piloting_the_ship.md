### Meta
2024-11-13 18:48
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Piloting the Ship
We’ll write code that responds when the player presses the right or left arrow key. We’ll focus first on movement to the right, and then we’ll apply the same principles to control movement to the left.

#### Responding to a Keypress
Whenever the player presses a key, that keypress is registered in Pygame as an event. Each event i picked up by the `pygame.event.get()` method. We need to specify in our `_check_events()` method what kind of events we want the game to check for. Each keypress is registered as a `KEYDOWN` event.

When Pygame detects a `KEYDOWN` event, we need to check whether the key that was presses is one that triggers a certain action. For example, if the player presses the right arrow key, we want to increase the ship’s `rect.x` value to move the ship to the right:
```Python title:alien_invasion.py
	def _check_events(self):
		"""Respond to keypress and mouse events."""
		for event in pygame.event.get():
			if event.type == pygame.QUIT:
				sys.exit()
			elif event.type == pygame.KEYDOWN:
				if event.key == pygame.K_RIGHT:
					# Move the ship to the right.
					self.ship.rect.x += 1
```

#### Allowing Continuous Movement
When the player holds down the right arrow key, we want the ship to continue moving right until the player releases the key.

To achieve that, we’ll have the game detect a `pygame.KEYUP` event so we’ll know when the right arrow key is released; then, we’ll use the `KEYDOWN` and `KEYUP` events together with a flag called `moving_right` to implement continuous motion.

The `Ship` class controls all attributes of the ship, so we’ll give it an attribute called `moving_right` and an `update()` method to check the status of the `moving_right` flag. The `update()` method will change the position of the ship if the flag is set to `True`. We’ll call this method once on each pass through the `while` loop to update the position of the ship.

```Python title:ship.py
class Ship:
	"""A class to manage the ship."""

	def __init__(self, ai_game):
		--snip--
		# Start each new ship at the bottom center of the screen.
		self.rect.midbottom = self.screen_rect.midbottom

		# Movement flag; starts with a stationary ship.
		self.moving_right = False

	def update(self):
		"""Update the ship's position based on the movement flag."""
		if self.moving_right:
			self.rect.x += 1

	def blitme(self):
		--snip--
```

Now we need to modify `_check_events()` so that `moving_right` is set to `True` when the right arrow key is pressed and `False` when the key is released:
```Python title:alien_invasion.py
	def _check_events(self):
		"""Respond to keypresses and mouse events."""
		for event in pygame.event.get():
		--snip--
		elif event.type == pygame.KEYDOWN:
			if event.key == pygame.K_RIGHT:
				self.ship.moving_right = True
		elif event.type = pygamne.KEYUP:
			if event.key == pygame.K_RIGHT:
				self.ship.moving_right = False
```

Next, we modify the `while` loop in `run_game()` so it calls the ship’s `update()` method on each pass through the loop:
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the main loop for the game."""
		while True:
			self._check_events()
			self.ship.update()
			self._update_screen()
			self.clock.tick(60)
```

The ship’s position will be updated after we’ve checked for keyboard events and before we update the screen. This allows the ship’s position to be updated in response to player input and ensures the updated position will be used when drawing the ship to the screen.

#### Moving Both Left and Right
```Python title:ship.py
	def __init__(self, ai_game):
		--snip--
		# Movement flags; start with a ship that's not moving.
		self.moving_right = False
		self.moving_left = False

	def update(self):
		"""Update the ship's position based on movement flags."""
		if self.moving_right:
			self.rect.x += 1
		if self.moving_left:
			self.rect.x -= 1
```

If we used `elif` for motion to the left, the right arrow key would always have priority. Using two `if` blocks makes the movements more accurate when the player might momentarily hold down both keys wen changing directions.

We must make two additions to `_check_events()`:
```Python title:alien_invasion.py
def _check_events(self):
	"""Respond to keypresses and mouse events."""
	for event in pygame.event.get():
		--snip--
		elif event.type == pygame.KEYDOWN:
			if event.key == pygame.K_RIGHT:
				self.ship.moving_right = True
			elif event.key == pygame.K_LEFT:
				self.ship.moving_left = True

		elif event.type == pygame.KEYUP:
			if event.key == pygame.K_RIGHT:
				self.ship.moving_right = False
			elif event.key == pygame.K_LEFT:
				self.ship.moving_left = False
```

#### Adjusting the Ship’s Speed
Currently, the ship moves one pixel per cycle through the `while` loop, but we can take finer control of the ship’s speed by adding a `ship_speed` attribute to the `Settings` class. We’ll use this attribute to determine how far to move the ship on each pass through the loop.
```Python title:settings.py
class Settings:
	"""A class to store all settings for Alien Invasion."""

	def __init__(self):
		--snip--

		# Ship settings
		self.ship_speed = 1.5
```

We’re using a float for the speed setting to give us finer control of the ship’s speed when we increase the tempo of the game later on. However, `rect` attributes such as `x` store only integer values, so we need to make some modifications to `Ship`:
```Python title:ship.py
class Ship:
	"""A class to manage the ship."""

	def __init__(self, ai_game):
		"""Initialize the ship and set its starting position."""
		self.screen = ai_game.screen
		self.settings = ai_game.settings
		--snip--

		# Store a float for the ship's exact horizontal position.
		self.x = float(self.rect.x)

		# Movement flags; start with a ship that's not moving.
		self.moving_right = False
		self.moving_left = False

	def update(self):
		"""Update the ship's position based on movement flags."""
		# Update the ship's x value, not the rect.
		if self.moving_right:
			self.x += self.settings.ship_speed
		if self.moving_left:
			self.x -= self.settings.ship_speed

		# Update react object from self.x.
		self.rect.x = self.x

	def blitme(self):
		--snip--
```

#### Limiting the Ship’s Range
The ship will disappear off either edge of the screen if you hold down an arrow key long enough. We correct this by modifying the `update()` method in `Ship`:
```Python title:ship.py
	def update(self):
		"""Update the ship's position based on movement flags."""
		# Update the ship's x value, not the rect.
		if self.moving_right and self.rect.right < self.screen_rect.right:
			self.x += self.settings.ship_speed
		if self.moving_left and self.rect.left > 0:
			self.x -= self.settings.ship_speed

		# Update rect object from self.x.
		self.rect.x = self.x
```

#### Refactor `_check_events()`
The `_check_events()` method will increase in length as we continue to develop the game, so let’s break it into two separate methods: one that handles `KEYDOWN` events, another that handles `KEYUP` events:
```Python title:alien_invasion.py
	def _check_events(self):
		"""Respond to keypresses and mouse events."""
		for event in pygame.event.get():
			if event.type == pygame.QUIT:
				sys.exit()
			elif event.type == pygame.KEYDOWN:
				self._check_keydown_events(event)
			elif event.type == pygame.KEYUP:
				self._check_keyup_events(event)

	def _check_keydown_events(self, event):
		"""Respond to keypresses."""
		if event.key == pygame.K_RIGHT:
			self.ship.moving_right = True
		elif event.key == pygame.K_LEFT:
			self.ship.moving_left = True

	def _check_keyup_events(self, event):
		"""Respond to key releases."""
		if event.key == pygame.K_RIGHT:
			self.ship.moving_right = False
		elif event.key == pygame.K_LEFT:
			self.ship.moving_left = False
```

#### Pressing Q to Quit
```Python title:alien_invasion.py
	def _check_keydown_events(self, event):
		--snip--
		elif event.key == pygame.K_LEFT:
			self.ship.moving_left = True
		elif event.key == pygame.K_q:
			sys.exit()
```

#### Running the Game in Fullscreen Mode
```Python title:alien_invasion.py
	def __init__(self):
		"""Initialize the game, and create game resources?"""
		pygame.init()
		self.settings = Settings()

		self.screen = pygame.display.set_mode((0, 0), pygame.FULLSCREEN)
		self.settings.screen_width = self.screen.get_rect().width
		self.settings.screen_height = self.screen.get_rect().height
		pygame.display.set_caption("Alien Invasion")
```

**Note:** Make sure you can quit by pressing Q before running the game in fullscreen mode; Pygame offers no default way to quit a game while in fullscreen mode.