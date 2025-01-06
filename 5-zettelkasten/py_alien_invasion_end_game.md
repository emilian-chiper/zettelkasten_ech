### Meta
2024-12-23 08:11
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_aliens]]
**Status:** #completed 

### Ending the Game
What’s the fun and challenge in playing a game you can’t lose? If the player doesn’t shoot down the fleet quickly enough, we’ll have the aliens destroy the ship when they make contact. At the same time, we’ll limit the number of ships a player can use, and we’ll destroy the ship when an alien reaches the bottom of the screen.

#### Detecting Alien-Ship Collisions
We start by checking for collisions between aliens and the ship so we can respond appropriately when an alien hits it. We’ll check for alien-ship collisions immediately after updating the position of each alien in `AlienInvasion`:
```Python title:alien_invasion.py
	def _update_aliens(self):
		--snip--
		self.aliens.update()

		# Look for alien-ship collisions.
		if pygame.sprite.spritecollideany(self.ship, self.aliens):
			print("Ship hit!!!")
```

The `spritecollideany()` function takes two arguments: a sprite and a group. The function looks for any member of the group that has collided with the sprite and stops looping through the group as soon as it finds one member that has collided with the sprite. Here, it loops through the group `aliens` and returns the first alien if it finds that has collided with the ship.

If no collisions occur, `spritecollideany()` returns `None` and the `if` block doesn’t execute.

#### Responding to Alien-Ship Collisions
Instead of destroying the `ship` instance and creating a new one, we’ll count how many times the ship has been hit by tracking statistics for the game. Tracking statistics will also be useful for scoring.

We’ll create a new module, `GameStats`, for this very purpose.
```Python title:game_stats.py
class GameStats:
	"""Track statistics for Alien Invasion."""

	def __init__(self, ai_game):
		"""Initialize statistics."""
		self.settings = ai_game.settings
		self.reset_stats()

	def reset_stats(self):
		"""Initialize statistics that can change during the game."""
		self.ships_left = self.settings.ship_limit
```

We’ll make one `GameStats` instance for the entire time *Alien Invasion* is running, but we’ll need to reset some statistics each time the player starts a new game. To do this, we’ll initialize most of the statistics in the `reset_stats()` method, instead of directly in `__init__()`. We’ll call this method from `__init__()` so the statistics are set properly when the `GameStats` instance is first created. We’ll also be able to call `reset_stats()` anytime the player starts a new game. Right now, we have only one statistic, `ships_left`, the value of which will change throughout the game.

The number of ships the player starts with should be stored in *settings.py* as `ship_limit`:
```Python title:settings.py
	# Ship settings
	self.ship_speed = 1.5
	self.ship_limit = 3
```

We must also make a few changes in *alien_invasion.py* to create an instance of `GameStats`. First, we’ll update the `import` statements at the top of the file:
```Python title:alien_invasion.py
import sys
from time import sleep

import pygame

from settings import Settings
from game_stats import GameStats
from ship import Ship
--snip--
```

We import the `sleep()` function from the `time` module in the Python standard library, so we can pause the game for a moment when the ship is hit. We also import `GameStats`.

We’ll create an instance of `GameStats` in `__init__()`:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		self.screen = pygame.display.set_mode(
			(self.settings.screen_width, self.settings.screen_height)
		)
		pygame.display.set_caption("Alien Invasion")

		# Create an instance to store game statistics.
		self.stats = GameStats(self)

		self.ship = Ship(self)
		--snip--
```

We make the instance after creating the game window but before defining other game elements, such as the ship.

When an alien hits the ship, we’ll subtract `1` from the number of ships left, destroy all existing aliens and bullets, create a new fleet, and reposition the ship in the middle of the screen. We’ll also pause the game for a moment so the player can notice the collision and regroup before a new fleet appears.

Let’s place most of this code in a new method called `_ship_hit()`. We’ll call this method from `_update_aliens()` when an alien hits the ship:
```Python title:alien_invasion.py
	def _ship_hit(self):
		"""Respond to the ship being hit by an alien."""
		# Decrement ships_left.
		self.stats.ships_left -= 1

		# Get rid of any remaining bullets and aliens.
		self.bullets.empty()
		self.aliens.empty()

		# Create a new fleet and center the ship.
		self._create_fleet()
		self.ship.center_ship()

		# Pause.
		sleep(0.5)
```

In `_update_aliens()`, we replace the `print()` call with a call to `_ship_hit()` when an alien hits the ship:
```Python title:alien_invasion.py
	def _update_aliens(self):
		--snip--
		if pygame.sprite.spritecollideany(self.ship, self.aliens):
			self._ship_hit()
```

Here’s the new method `center_ship`, which belongs to *ship.py*:
```Python title:ship.py
	def center_ship(self):
		"""Center the ship on the screen."""
		self.rect.midbottom = self.screen_rect.midbottom
		self.x = float(self.rect.x)
```

We center the ship the same way we did in `__init__()`. After centering it, we reset the `self.x` attribute, which allows us to track the ship’s exact position.

**Note:** Notice that we never make more than one ship; we make only one ship instance for the whole game and recenter it whenever the ship has been hit. The statistics `ships_left` will tell us when the player has run out of ships.

#### Aliens That Reach the Bottom of the Screen
If an alien reaches the bottom of the screen, we’ll have the game respond the same way it does when an alien hits the ship. To check when this happens, add a new method in *alien_invasion.py*:
```Python title:alien_invasion.py
	def _check_aliens_bottom(self):
		"""Check if any aliens have reached the bottom of the screen."""
		for alien in self.aliens.sprites():
			if alien.rect.bottom >= self.settings.screen_height:
				# Treat this the same as if the ship got hit.
				self._ship_hit()
				break
```

We’ll call this method from `_update_aliens()`:
```Python title:alien_invasion.py
	def _update_aliens(self):
		--snip--
		# Look for alien-ship collisions.
		if pygame.sprite.spritecollideany(self.ship, self.aliens):
			self._ship_hit()

		# Look for aliens hitting the bottom of the screen.
		self._check_aliens_bottom()
```

We call `_check_aliens_bottom()` after updating the positions of all the aliens and after looking for alien-ship collisions. Now a new fleet will appear every time the ship is hit by an alien or an alien reaches the bottom of the screen.

#### Game Over!
*Alien Invasion* feels more complete now, but the game never ends. The value of `ships_left` just grows increasingly negative. Let’s add a `game_active` flag, so we can end the game when the player runs out of ships. We’ll set this flag at the end of the `__init__()` method in `AlienInvasion`:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		# Start Alien Invasion in an active state.
		self.game_active = True
```

Now add code to `_ship_hit` that sets `game_active` to `False` when the player has used up all their ships:
```Python title:alien_invasion.py
	def _ship_hit(self):
		"""Respond to ship being hit by alien."""
		if self.stats.ships_left > 0:
			# Decrement ships_left.
			self.stats.ships_left -= 1
			--snip--
			# Pause
			sleep(0.5)
		else:
			self.game_active = False
```

Most of `_ship_hit()` is unchanged. We’ve moved all the existing code into an `if` block, which tests to make sure the player has at least one ship remaining. If so, we create a new fleet, pause, and move on. If the player has no ships left, we set `game_active` to `False`.

#### Identifying When Parts of the Game Should Run
We must identify the parts of the game that should always run and the parts that should run only when the game is active:
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the main loop for the game."""
		while True:
			self._check_events()

			if self.game_active:
				self.ship.update()
				self._update_bullets()
				self._update_aliens()

			self._update_screen()
			self.clock.tick(60)
```

In the main loop, we must always call `_check_events()`, even if the game is inactive. For example, we still need to know if the user presses Q to quit the game or clicks the button to close the window. We also continue updating the screen so we can make changes to the screen while waiting to see whether the player chooses to start a new game. The rest of the function calls must happen only when the game is active, because when the game is inactive, we don’t need to update the positions of game elements.