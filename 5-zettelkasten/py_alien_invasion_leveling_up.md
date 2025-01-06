### Meta
2024-12-23 14:41
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_scoring]]
**Status:** #completed 

### Leveling Up
In our current game, once a player shoots down the entire fleet, the player reaches a new level, but the game difficulty doesn’t change. Let’s make things a bit more challenging by increasing the game’s speed each time a player clears the screen.

#### Modifying the Speed Settings
We’ll first reorganize the `Settings` class to group the game settings into static and dynamic ones. We’ll also ensure any settings that change during the game reset when we start a new game. Here’s `__init__()` for *settings.py*:
```Python title:settings.py
	def __init__(self):
		"""Initialize the game's static settings."""
		--snip--

		# Alien settings
		self.fleet_drop_speed = 10

		# How quickly the game speeds up
		self.speedup_scale = 1.1

		self.initialize_dynamic_settings()
```

We continue to initialize settings that stay constant in the `__init__()` method. We add a `speedup_scale` setting to control how quickly the game speeds up: a value of `2` will double the game speed every time the player reaches a new level; a value of `1` will keep the speed constant. A value like `1.1` should increase the speed enough to make the game challenging but not impossible. Finally, we call the `initialize_dynamic_settings()` method to initialize the values for attributes that must change throughout the game.

Here’s the code for `initialize_dynamic_settings()`:
```Python title:settings.py
	def initialize_dynamic_settings(self):
		"""Initialize settings that change throughout the game."""
		self.ship_speed = 1.5
		self.bullet_speed = 2.5
		self.alien_speed = 1.0

		self.fleet_direction = 1
```

This method sets the initial values for the ship, bullet, and alien speeds. We’ll increase these speeds as the player progresses in the game and reset them each time the player starts a new game. We include `fleet_direction` in this method so the aliens always move right at the beginning of a new game. We don’t need to increase the value of `fleet_drop_speed`, because when the aliens move faster across the screen, they’ll also come down the screen faster.

To increase the speeds of the ship, bullets, and aliens each time the player reaches a new level, we’ll write a new method called `increase_speed()`:
```Python title:settings.py
	def increase_speed(self):
		"""Increase speed settings."""
		self.ship_speed *= self.speedup_scale
		self.bullet_speed *= self.speedup_scale
		self.bullet_speed *= self.speedup_scale
```

To increase the speed of these game elements, we multiply each speed setting by the value of `speedup_scale`.

We increase the game’s tempo by calling `increase_speed()` in `_check_bullet_alien_collisions()` when the last alien in a fleet has been shot down:
```Python title:alien_invasion.py
	def _check_bullet_alien_collisions(self):
		--snip--
		if not self.aliens:
			# Destroy existing bullets and create new fleet.
			self.bullets.empty()
			self._create_fleet()
			self.settings.increase_speed()
```

Changing the values of the speed settings `ship_speed`, `alien_speed`, and `bullet_speed` is enough to speed up the entire game.

#### Resetting the Speed
Now we need to return any changed settings to their individual values each time the player starts a new game; otherwise, each new game would start with the increased speed settings of the previous game:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		"""Start a new game when the player clicks Play."""
		button_clicked = self.play_button.rect.collidepoint(mouse_pos)
		if button_clicked and not self.game_active:
			# Reset the game settings.
			self.settings.initialize_dynamic_settings(************)
```