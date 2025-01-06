### Meta
2024-12-16 18:49
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_aliens]]
**Status:** #completed 

### Creating the First Alien
Placing one alien on the screen is like placing a ship on the screen. Each alien’s behavior is controlled by a class **called** `Alien`, similar to the `Ship` class.

#### Creating the Alien Class
Now we’ll write the `Alien` class and save it as *alien.py*:

```Python title:alien.py
import pygame
from pygame.sprite import Sprite

class Alien(Sprite):
	"""A class to represent a single alien in the fleet."""

	def __init__(self, ai_game):
		"""Initialize the alien and set its starting position."""
		super().__init__()
		self.screen = ai_game.screen

		# Load the alien image and set its rect attribute.
		self.image = pygame.image.load('img/alien.png')
		self.rect = self.image.get_rect()

		# Start each new alien at the top left of the screen.
		self.rect.x = self.rect.width
		self.rect.y = self.rect.height

		# Store the alien's exact horizontal position.
		self.x = float(self.rect.x)
```

This `Alien` class doesn’t need a method for drawing it to the screen; instead, we’ll use a Pygame group method that automatically draws all the elements of a group to the screen.

#### Create an Instance of the Alien
We want to create an instance of `Alien` so we can see the first alien on the screen. Because it’s part of our setup work, we’ll add the code for this instance at the end of the `__init__()` method in `AlienInvasion`. Eventually, we’ll create an entire fleet of aliens, which will be quite a bit of work, so we’ll create a new helper method called `_crete_fleet()`.

The order of methods in this class doesn’t matter, as long as there’s some consistency to how they’re placed. We position `_create_fleet` just before the `_update_screen()` method, but anywhere in `AlienInvasion` will work. First, we’ll import the `Alien` class.

Here are the updated import statements.
```Python title:alien_invasion.py
--snip--
from bullet import Bullet
from alien import Alien
```

An here’s the updated `__init__()` method:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		self.ship = Ship(self)
		self.bullets = pygame.sprite.Group()

	self._create_fleet()
```

We create a group to hold the fleet of aliens, and we call `_create_fleet()`:
```Python title:alien_invasion.py
	def _create_fleet(self):
		"""Create the fleet of aliens."""
		# Make an alien.
		alien = Alien.self()
		self.aliens.add(alien)
```

In this method, we’re creating one instance of `Alien` and then adding it to the group that will hold the fleet. The alien will be placed in the default upper-left area of the screen.

To make the alien appear, we must call the group’s `draw()` method in `_update_screen()`:
```Python title:alien_invasion.py
	def _update_screen(self):
		--snip--
		self.ship.blitme()
		self.aliens.draw(self.screen)

		pygame.display.flip()
```

When calling `draw()` on a group, Pygame draws each element in the group at the position defined by its `rect` attribute. The `draw()` method requires one argument: a surface on which to draw the elements from the group.