### Meta
2024-11-12 21:24
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_ship]]
**Status:** #completed 

### Adding the Ship Image
To draw the player’s ship on the screen, we’ll load an image and then use the Pygame `blit()` method to draw the image.

Give [https://opengameart.org.](https://opengameart.org.) a look for free assets. Do credit artists.

#### Creating the Ship Class
To use our ship, we’ll create a new `ship` module that will contain the class `Ship`. This class will manage most of the behavior of the players’ ship:
```Python title:ship.py
import pygame

class Ship:
	"""A class to manage the ship."""

	def __init__(self, ai_game):
		"""Initialize the ship and set its starting position."""
		self.screen = ai_game.screen
		self.screen_rect = ai_game.screen.get_rect()

		# Load the ship image and get its rect.
		self.image = pygame.image.load('images/ship.bmp')
		self.rect = self.image.get_rect()

		# Start each new ship at the bottom center of the screen.
		self.rect.midbottom = self.screen_rect.midbottom

	def blitme(self):
		"""Draw the ship at its current location."""
		self.screen.blit(self.image, self.rect)
```

Pygame is efficient because it lets you treat all game elements like rectangles (*rects*), even if they’re not exactly shaped like rectangles. Treating an element as a rectangle is efficient because rectangles are simple geometric shapes. When Pygame needs to figure out whether two game elements have collided, for example, it can do this more quickly if it treats each object as a  rectangle. This approach usually works well enough that no one playing the game will notice that we’re not working with the exact shape of each game element.

The `__init__()` method of `Ship` takes two parameters: the `self` reference and a reference to the current instance of the `AlienInvasion` class. This will give `Ship` access to all the game resources defined in `AlienInvasion`. We then assign the screen to an attribute of `Ship`, so we can access it easily in all the methods in this class. We access the screen’s `rect` attribute using the `get_rect()` method and assign it to `self.screen_rect`. Doing so allows us to place the ship in the correct location on the screen.

To load the image, we call `pygame.image.load()` and give it the location of our ship image. This function returns a surface representing the ship, which we assign to `self.image`. When the image is loaded, we call `get_rect()` to access the ship surface’s `rect`attribute so we can later use it to place the ship.

When you’re working with a `rect` object, you can use the *x-* and *y-* coordinates of the top, bottom, left, and right edges of the rectangle, as well as the center, to place the object. You can set any of these values to establish the current position of the `rect`. When you’re centering a game element, work with the `center`, `centerx` or `centery` attributes of a `rec`. When you’re working at an edge of the screen, work with the `top`, `bottom`, `left`, or `right` attributes. There are also attributes that combine these properties, such as `midbottom`, `midtop`, `midleft`, and `midright`. When you’re adjusting the horizontal or vertical placement of the `rect`, you can just use the `x` and `y` attributes, which are the *x-* and *y-* coordinates of its top-left corner. These attributes spare you from having to do calculations that game developers formerly had to do manually, and you’ll use them often.

**Note:** In Pygame, the *origin (0, 0)* is at the top-left corner of the screen, and coordinates increase as you go down and to the right. On a $1200 \times 800$ screen, the origin is at the top-left corner, and the bottom-right corner has the coordinates *(1200, 800)*. These coordinates refer to the game window, not the physical screen.

#### Drawing the Ship to the Screen
```Python title:alien_invasion.py
--snip--
from settings import Settings
from ship import Ship

class AlienInvasion:
	"""Overall class to manage game assets and behavior."""

	def __init__(self):
		--snip--
		pygame.display.set_caption("Alien Invasion")

		self.ship = Ship(self)

	def run_game(self):
		--snip--
		# Redraw the screen during each pass through the loop.
		self.screen.fill(self.settings.bg_color)
		self.ship.blitme()

		# Make the most recently drawn screen visible.
		pygame.display.flip()
		self.clock.tick(60)
--snip--
```