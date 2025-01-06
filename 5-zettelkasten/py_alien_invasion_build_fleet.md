### Meta
2024-12-20 18:05
**Tags:**  [[py_projects]] [[py_alien_invasion]] [[py_ai_aliens]]
**Status:** #**completed** 

### Building the Alien Fleet
To draw a fleet, we must figure out how to fill the upper portion of the screen with aliens, without overcrowding the game window. We’ll add aliens across the top of the screen until there’s no space left for a new alien. Then we’ll repeat the process as long as there is vertical space to add a new row.

#### Creating a Row of Aliens
To make a full row, we’ll first make a single alien so we have access to the alien’s width. We’ll place it on the left side of the screen and then keep adding aliens until we run out of space:
```Python title:alien_invasion.py
	def _create_fleet(self):
		"""Create the fleet of aliens."""
		# Create an alien and keep adding aliens until there's no room left.
		# Spacing between aliens is one alien width.
		alien = Alien(self)
		alien_width = alien.rect.width

		current_x = alien_width
		while current_x < (self.settings.screen_width - 2 * alien_width):
			new_alien = Alien(self)
			new_alien.x = current_x
			new_alien.rect.x = current_x
			self.aliens.add(new_alien)
			current_x += 2 * alien_width
```

#### Refactoring `_create_fleet()`
We’ll add a new helper method, `_create_alien()`, and call it from `_create_fleet()`:
```Python title:alien_invasion.py
	def _create_fleet(self):
		--snip--
		while current_x < (self.settings.screen_width - 2 * alien_width):
			self._create_alien(current_x)
			current_x += 2 * alien_width

	def _create_alien(self, x_position):
		"""Create an alien and place it in the row."""
		new_alien = Alien(self)
		new_alien.x = x_position
		new_alien.rect.x = x_position
		self.aliens.add(new_alien)
```

#### Adding Rows
To finish the fleet, we’ll keep adding more rows until we run out of room.
We’ll use a nested loop–we’ll wrap another `while` loop around the current one. The inner loop will place aliens horizontally in a row by focusing on the alien’s *x*-values. The outer loop will place aliens vertically by focusing on the *y*-values. We’ll stop adding rows when we get near the bottom of the screen, leaving enough space for the ship and some room to start firing at the aliens.
```Python title:example.py
	def _create_fleet(self):
		"""Create the fleet of aliens."""
		# Create an alien and keep adding aliens until there's no room left.
		# Spacing between aliens is one alien width and one alien height.
		alien = Alien(self)
		alien_width, alien_height = alien.rect.size

		current_x, current_y = alien_width, alien_height
		while current_y < (self.settings.screen_height - 3 * alien_height):
			while current_x < (self.settings.screen_width - 2 * alien_width):
				self._create_alien(current_x, current_y)
				current_x += 2 * alien_width

		# Finished a row; reset x value, and increment y value.
		current_x = alien_width
		current_y += 2 * alien_height
```

Notice the indentation of the last two lines of code. They’re inside the outer `while` loop, but inside the inner one. This block runs after the inner loop is finished; it runs once after each row is created. After each row has been added, we reset the value of `current_x` so the first alien in the next row will be placed at the same position as the first alien in the previous rows. Then we add two alien heights to the current value of `current_y`, so the next row will be placed further down the screen.

We need to modify `_create_alien()` to set the vertical position of the alien correctly:
```Python title:alien_invasion.py
	def _create_alien(self, x_position, y_position):
		"""Create an alien and place it in the fleet."""
		new_alien = Alien(self)
		new_alien.x = x_position
		new_alien.rect.x = x_position
		new_alien.rect.y = y_position
		self.aliens.add(new_alien)
```