### Meta
2024-12-22 09:45
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_aliens]]
**Status:** #completed 

### Making the Fleet Move
The goal is to make the fleet of aliens move to the right across the screen until it hits the edge, and then make it drop a set amount and move in the other direction. We’ll continue this movement until all aliens have been shot down, one collides with the ship, or one reaches the bottom of the screen.

#### Moving the Aliens Right
To move the aliens, we’ll use an `update()` method in *alien.py*, which we’ll call for each alien in the group of aliens. First, add a setting to control the speed of each alien:
```Python title:settings.py
	def __init__(self):
		--snip--
		# Alien settings
		self.alien_speed = 1.0
```

Then, use this setting to implement `update()` in *alien.py*:’
```Python title:alien.py
	def __init__(self, ai_game):
		"""Initialize the alien and set its starting position."""
		super().__init__()
		self.screen = ai_game.screen
		self.settings = ai_game.settings
		--snip--

	def update(self):
		"""Move the alien to the right."""
		self.x += self.settings.alien_speed
		self.rect.x = self.x
```

In the main `while` loop, we already have calls to update the ship and bullet positions. Now we’ll add a call to update the position of each alien as well:
```Python title:alien_invasion.py
	while True:
		self._check_events()
		self.ship.update()
		self._update_bullets()
		self._update_aliens()
		self._update_screen()
		self.clock.tick(60)
```

We’re about to write some code to manage the movement of the fleet, so we create a new method called `_update_aliens()`. We update the aliens’ positions after the bullets have been updated, because we’ll soon be checking to see whether any bullets hit any aliens.

To keep the code organized, we’ll place it just after `_update_bullets()` to match the order of method calls in the `while` loop. Here’s the first version:
```Python title:alien_invasion.py
	def _update_aliens(self):
		"""Update the positions of all aliens in the fleet."""
		self.aliens.update()
```

#### Creating Settings for Fleet Direction
Now we’ll create the settings that will make the fleet move down the screen and to the left when it hits the right edge of the screen.
```Python title:settings.py
	# Alien settings
	self.alien_speed = 1.0
	self.fleet_drop_speed = 10
	# fleet_direction of 1 represents right; -1 represents left
	self.fleet_direction = 1
```

The setting `fleet_drop_speed` controls how quickly the fleet drops down the screen each time an alien reaches either edge. It’s helpful to separate this speed from the alien’s horizontal speed so you can adjust the two speeds independently.

To implement the setting `fleet_direction`, we could use a text value such as `'left'` or `'right'`, but we’d end up with `if-elif` statements testing for the fleet direction. Instead, because we only have two directions to deal with, let’s use the values `1` and `-1` and switch between them each time the fleet changes direction. (Using numbers also makes sense because moving right involves adding to each alien’s *x*-coordinate value, and moving left involves subtracting from each alien’s *x*-coordinate value.)

#### Checking Whether an Alien Has Hit the Edge
We need a method to check whether an alien is at either edge, and we need to modify `update()` to allow each alien to move in the appropriate direction. This code is part of the `Alien` class:
```Python title:alien.py
	def check_edges(self):
		"""Return True if alien is at edge of screen."""
		screen_rect = self.screen.get_rect()
		return (self.rect.right >= screen_rect.right) or (self.rect.left <= 0)

	def update(self):
		"""Move the alien right or left."""
		self.x += self.settings.alien_speed * self.settings.fleet_direction
		self.rect.x = self.x
```

#### Dropping the Fleet and Changing Direction
When an alien reaches the edge, the entire fleet must drop down and change direction. Therefore, we need to add some code to `AlienInvasion` because that’s where we’ll check whether any aliens are at the left or right edge. We’ll make it happen by writing the methods `_check_fleet_edges()` and `_change_fleet_direction()`, and then modifying `_update_aliens()`. We’ll place these after `_create_alien()`.
```Python title:alien_invasion.py
	def _check_fleet_edges(self):
		"""Respond appropriately if any aliens have reached an edge."""
		for alien in self.aliens.sprites():
			if alien.check_edges():
				self._change_fleet_direction()
				break

	def _change_fleet_direction(self):
		"""Drop the entire fleet and change the fleet's direction."""
		for alien in self.aliens.sprites():
			alien.rect.y += self.settings.fleet_drop_speed
		self.settings.fleet_direction *= -1
```

Here are the changes to `_update_aliens()`:
```Python title:alien_invasion.py
	def _update_aliens(self):
		"""Check if the fleet is at an edge, then update positions."""
		self._check_fleet_edges()
		self.aliens.update()
```