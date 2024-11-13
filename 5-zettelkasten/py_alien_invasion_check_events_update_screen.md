### Meta
2024-11-12 23:11
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Refactoring: The `_check_events()` and `_update_screen()` Methods
In this section, we’ll break the `run_game()` method, which is getting lengthy, into two helper methods. A *helper method* does work inside a class but isn’t meant to be used by code outside the class. In Python, a single leading underscore indicates a helper method.

#### The `_check_events()` Method
We’ll move the code that manages events to a separate method called `_check_events()`. This will simplify `run_game()` and isolate the event management loop. Isolating the event loop allows you to manage events separately from other aspects of the game, such as updating the screen.
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the main loop for the game."""
		while True:
			self._check_events()

			# Redraw the screen during each pass through the loop.
			--snip--

	def _check_events(self):
		"""Respond the keypresses and move events."""
		for event in pygame.event.get():
			if event.type == pygame.QUIT:
				sys.exit()
```

To call a method from within a class, use dot notation with the variable `self` and the name of the method.

#### The `_update_screen()` Method
To further simplify `run_game()`, we’ll move the code for updating the screen to a separate method called `_update_screen()`:
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the game loop."""
		while True:
			self._check_events()
			self._update_screen()
			self.clock.tick(60)

	def _check_events(self):
		--snip--

	def _update_screen(self):
		"""Update images on the screen, and flip to the new screen."""
		self.screen.fill(self.settings.bg_color)
		self.ship.blitme()

		pygame.display.flip()
```