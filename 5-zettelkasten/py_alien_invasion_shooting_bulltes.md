### Meta
2024-11-14 16:41
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Shooting Bullets
We’ll write code that fires a bullet, which is represented by a small rectangle, when the player presses the spacebar. Bullets will then travel straight up the screen until they disappear off the top of the screen.

#### Adding the Bullet Settings
At the end of the `__init__()` method, we’ll update *setthings.py* to include the values we’ll need for a new Bullet class:
```Python title:settings.py
	def __init__(self):
		--snip--
		# Bullet settings
		self.bullet_speed = 2.0
		self.bullet_width = 3
		self.bullet_height = 15
		self.bullet_color = (60, 60, 60)
```

These settings create dark grey bullets with a width of `3` pixels and a height of `15` px. The bullets will travel slightly faster than the ship.

#### Creating the Bullet Class
```Python title:bullet.py
import pygame
from pygame.sprite import Sprite

class Bullet(Sprite):
	"""A class to manage bullets fired from the ship."""

	def __init__(self, ai_game):
		"""Create a bullet object at the ship's current position."""
		super().__init__()
		self.screen = ai_game.screen
		self.settings = ai_game.settings
		self.color = self.settings.bullet_color

		# Create a bullet rect at (0, 0) and then set correct position.
		self.rect = pygame.Rect(0, 0, self.settings.bullet_widt, self.settings.bullet_height)
		self.rect.midtop = ai_game.ship.rect.midtop

		# Store the bullet's position as a float.
		self.y = float(self.rect.y)

	def update(self):
		"""Move the bullet up the screen."""
		# Update the exact position of the bullet.
		self.y -= self.settings.bullet_speed
		# Update the rect position.
		self.rect.y = self.y

	def draw_bullet(self):
		"""Draw the bullet to the screen."""
		pygame.draw.rect(self.screen, self.color, self.rect)
```

#### Storing Bullets in a Group
Now that we have a `Bullet` class and the necessary settings defined, we can write code to fire a bullet each time the player presses the spacebar. We’ll create a group in `AlienInvasion` to store all the active bullets so we can manage the bullets that have already been fired. This group will be an instance of the `pygame.sprite.Group` class, which behaves like a list with some extra functionality that’s helpful when building games. We’ll use this group to draw bullets to the screen on each pass through the main loop and to update each bullet’s position.
```Python title:alien_invasion.py
--snip--
from ship import Ship
from bullet import Bullet
```

Next, we’ll create the group that holds the bullets in `__init__()`:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		self.ship = Ship(self)
		self.bullets = pygame.sprite.Group()
```

Then, we must update the position of the bullets on each pass through the while loop:
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the main loop for the game."""
		while True:
			self._check_events()
			self.ship.update()
			self.bullets.update()
			self._update_screen()
			self.clock.tick(60)
```

When you call `update()` on a group, the group automatically calls `update()` for each sprite in the group. The line `self.bullets.update()` calls `bullet.update()` for each bullet we place in the group `bullets`.

#### Firing Bullets
We must modify `_check_keydown_events()` to fire a bullet when the player presses the spacebar. We don’t need to change the keyup events because nothing happens when the spacebar is released. We also need to modify `_update_screen()` to make sure each bullet is drawn to the screen before we call `flip()`.

We need a new method to achieve this:
```Python title:alien_invasion.py
	def _check_keydown_events(self, event):
		--snip--
		elif event.key == pygame.K_q:
			sys.exit()
		elif event.key == pygame.K_SPACE:
			self._fire_bullet()

	def _check_keyup_events(self, event):
		--snip--

	def _fire_bullet(self):
		"""Create a new bullet and add it to the bullets group."""
		new_bullet = Bullet(self)
		self.bullets.add(new_bullet)

	def _update_screen(self):
		"""Update images on the screen, and flip to the new screen."""
		self.screen.fill(self.settings.bg_color)
		for bullet in self.bullets.sprites():
			bullet.draw_bullet()
		self.ship.blitme()

		pygame.display.flip()
--snip--
```

#### Deleting Old Bullets
The bullets disappear when they reach the top, but only because Pygame can’t draw them above the top of the screen. The bullets actually continue to exist; their $y$-coordinate values just grow increasingly negative. This is a problem because they continue to consume memory and processing power.

We must remove old bullets, or the game will slow down. To do this, we must detect when the `bottom` value of a bullet’s `rect` has a value of `0`, which indicates it passing the top of the screen:
```Python title:alien_invasion.py
	def run_game(self):
		"""Start the main loop of the game."""
		while True:
			self._check_events()
			self.ship.update()
			self.bullets.update()

		# Get rid of bullets that have disappeared.
		for bullet in self.bullets.copy():
			if bullet.rect.bottom <= 0:
				self.bullets.remove(bullet)
		print(len(self.bullets))

		self._update_screen()
		self.clock.tick(60)
```

When you use a `for` loop with a list (or a group in Pygame), Python expects that the list will stay the same length as long as the loop is running. That means you can’t remove items from a list or group within a `for` loop, so we must loop over a copy of the group.

#### Limiting the Number of Bullets
Many shooting games limit the number of bullets a player can have on the screen at one time; doing so encourages the players to shoot accurately.

To achieve that, we’ll first store the number of bullets allowed in the bullet settings:
```Python title:settings.py
	# Bullet settings
	--snip--
	self.bullet_color = (60, 60, 60)
	self.bullets_allowed = 3
```

This limits the player to three bullets at a time. We’ll use this in `AlienInvasion` to check how many bullets exist before creating a new bullet in `_fire_bullet()`:
```Python title:alien_invasion.py
	def _fire_bullet(self):
		"""Create a new bullet and add it to the bullets group."""
		if len(self.bullets) < self.settings.bullets_allowed:
			new_bullet = Bullet(self)
			self.bullets.add(new_bullet)
```

#### Creating the `_update_bullets()` Method
We must keep `AlienInvasion` reasonably well organized, so now that we’ve written and checked the bullet management code, we can move it to a separate method.

We’ll create a new method called `_update_bullets()` and add it just before `_update_screen()`:
```Python title:alien_invasion.py
	def _update_bullets(self):
	"""Update position of bullets and remove old bullets."""
	# Update bullet positions.
	self.bullets.update()

	# Remove old bullets.
	for bullet in self.bullets.copy():
		if bullet.rect.bottom <= 0:
			self.bullets.remove(bullet)
```

The code for `_update_bullets()` is cut and pasted from `run_game()`; all we’ve done is clarify the comments.

The while loop in `run_game()` looks simple again:
```Python title:alien_invasion.py
	while True:
		self._check_events()
		self.ship.update()
		self._update_bullets()
		self._update_screen()
		self.clock.tick(60)
```