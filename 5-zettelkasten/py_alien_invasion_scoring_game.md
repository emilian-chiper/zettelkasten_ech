### Meta
2024-12-23 18:08
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_scoring]]
**Status:** #completed  

### Scoring
Let’s  implement a scoring system to track the game’s score in real time and display the high score, level, and number of ships remaining.

The score is a game statistic, so we’ll add a score attribute to `GameStats`:
```Python title:game_stats.py
class GameStats:
	--snip--
	def reset_stats(self):
		"""Initialize statistics that can change during the game."""
		self.ship_left = self.ai_settings.ship_limit
		self.score = 0
```

To reset the score each time a new game starts, we initialize `score` in `reset_stats()` rather than `__init__()`.

#### Displaying the Score
To display the score on the screen, we first create a new class, `Scoreboard`. For now, this class will just display the current score. Eventually, we’ll use it to report the high score, level, and number of ships remaining as well. Here’s the first part of the class; save it as *scoreboard.py*.
```Python title:scoreboard.py
import pygame.font

class Scoreboard:
	"""A class to report scoring information."""

	def __initi__(self, ai_game):
		"""Initialize scorekeeping attributes."""
		self.screen = ai_game.screen
		self.screen_rect = self.screen.get_rect()
		self.settings = ai_game.settings
		self.stats = ai_game.stats

		# Font settings for scoring information.
		self.text_color = (30, 30, 30)
		self.font = pygame.font.SysFont(None, 48)

		# Prepare the initial score image.
		self.prep_score()
```

Because `Scoreboard` writes text to the screen, we begin by importing the `pygame.font` module. Next, we give `__init__()` the `ai_game` parameter so it can access the `settings`, `screen`, and `stats` objects, which it will need to report the values we’re tracking. The we set a text color and instantiate a font object.

To turn the text to be displayed into an image, we call `prep_score()`, which we define here:
```Python title:scoreboard.py
	def prep_score(self):
		"""Turn the score into a rendered image."""
		score_str = str(self.stats.score)
		self.score_image = self.font.render(score_str, True, self.text_color, self.settings.bg_color)

		# Display the score at the top right of the screen.
		self.score_rect = self.score_image.get_rect()
		self.score_rect.right = self.screen_rect.right - 20
		self.score_rect.top = 20
```

In `prep_score()`, we turn the numerical value `stats.score` into a string and then pass this string to `render()`, which creates the image. To display the score clearly onscreen, we pass the screen’s background color and the text color to `render()`.

We’ll position the score in the upper-right corner of the screen and have it expand to the left as the score increases and the width of the number grows. To make sure the score always lines up with right side of the screen, we create a `rect` called `score_rect` and set its right edge 20 pixels from the right edge of the screen. We then place the top edge 20 pixels down from the top of the screen.

Then we create a `show_score()` method to display the rendered score image:
```Python title:scoreboard.py
	def show_score(self):
		"""Draw score to the screen."""
		self.screen.blit(self.score_image, self.score_rect)
```

This method draws the score image onscreen at the location `score_rect` specifies.

#### Making a Scoreboard
To display the score, we’ll create a `Scoreboard` instance in `AlienInvasion`. First, let’s update the `import` statements:
```Python title:alien_invasion.py
--snip--
from game_stats import GameStats
from scoreboard import Scoreboard
--snip--
```

Next, we make an instance of `Scoreboard` in`__init__()`:
```Python title:alien_invasion.py
	def __init__(self):
		--snip--
		pygame.display.set_caption("Alien Invasion")

	# Create an instance to store game statistics,
	#   and create a scoreboard.
	self.stats = GameStats(self)
	self.sb = Scoreboard(self)
	--snip--
```

The we draw the scoreboard onscreen in `_update_screen()`:
```Python title:alien_invasion.py
	def _update_screen(self):
		--snip--
		self.aliens.draw(self.screen)

		# Draw the score information.
		self.sb.show_score()

		# Draw the play button if the game is inactive.
		--snip--
```

We call `show_score()` just before we draw the Play button.

#### Updating the Score as Aliens are Shot Down
To write a live score onscreen, we update the value `stats.score` whenever an alien is hit, and then call `prep_score()` to update the score image. But first, let’s determine how many points a player gets each time they shoot down an alien:
```Python title:settings.py
	def initialize_dynamic_settings(self):
		--snip--

		# Scoring settings
		self.alien_points = 50
```

We’ll increase each alien’s point value as the game progresses. To make sure this point value is reset each time a new game starts, we set the value in `initialize_dynamic_settings()`.

Let’s update the score i n`_check_bullet_alien_collisions()` each time an alien is shot down:
```Python title:alien_invasion.py
	def _check_bullet_alien_collisions(self):
		"""Respond to bullet-alien collisions."""
		# Remove any bullets and aliens that have collided.
		collisions = pygame.sprite.groupcollide(self.bullets, self.aliens, True, True)

		if collisions:
			self.stats.score += self.settings.alien_points
			self.sb.prep_score()
		--snip--
```

When a bullet hits an alien, Pygame returns a `collisions` dictionary. We check whether the dictionary exists, and if it does, the alien’s value is added to the score. We then call `prepr_score()` to create a new image for the updated score.

#### Resetting the Score
Right now, we’re only prepping a new score *after* an alien has been hit, which works for most of the game. But when we start a new game, we’ll still see our score from the old game until the first alien is hit.

We can fix this by prepping the score when starting a new game:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		--snip--
		if button_clicked and not self.game_active:
			--snip--
			# Reset the game statistics.
			self.stats.reset_stats()
			self.sb.prep_score()
			--snip--
```

We call `prep_score()` after resetting the game stats when starting a new game. This preps the scoreboard with a score of 0.

#### Making Sure to Score All Hits
As currently written, our code could miss scoring for some aliens. For example, if two bullets collide with aliens during the same pass through the loop or if we make an extra-wide bullet to hit multiple aliens, the player will only receive points for hitting one of the aliens. To fix this, let’s refine the way that bullet-alien collisions are detected.

In `_check_bullet_alien_collisions()`, any bullet that collides with an alien becomes a key in the `collisions` dictionary. The value associated with each bullet is a list of aliens it has collided with. We loop through the values in the `collisions` dictionary to make sure we award points for each alien hit:
```Python title:alien_invasion.py
	def _check_bullet_alien_collisions(self):
		--snip--
		if collisions:
			for aliens in collisions.values():
				self.stats.score += self.settings.alien_points * len(aliens)
			self.sb.prep_score()
		--snip--
```

If the `collisions` dictionary has been defined, we loop through all values in the dictionary. Remember that each value is a list of aliens hit by a single bullet. We multiply the value of each alien by the number of aliens in each list and add this amount to the current score. To test this, change the width of a bullet to 300 pixels and verify that you receive points for each alien you hit with your extra-wide bullets; then return the bullet width to its normal value.

#### Increasing Point Values
Because the game gets more difficult each time a player reaches a new level, aliens in later levels should be worth more points. To implement this functionality, we’ll add code to increase the point value when the game’s speed increases.
```Python title:settings.py
class Settings:
	"""A class to store all settings for Alien Invasion."""

	def __init__(self):
		--snip--
		# How quickly the game speeds up.
		self.speedup_scale = 1.1
		# How quickly the alien point values increase
		self.score_scale = 1.5

		self.initialize_dynamic_settings()

	def initialize_dynamic_settings(self):
		--snip--

	def increase_speed(self):
		"""Increase speed settings and alien point values."""
		--snip--

		self.alien_points = int(self.alien_points * self.score_scale)
```

To see the value of each alien, add a `print` call to `increase_speed()` method in `Settings`:
```Python title:example.py
	def increase_speed(self):
		--snip--
		self.alien_points = int(self.alien_points * self.score_scale)
		print(self.alien_points)
```

The new point value should appear in terminal each time you reach a new level.

#### Rounding the Score
Most arcade-style shooting games report scores as multiples of 10, so let’s follow that lead with our scores. Also, let’s format the score to include comma separators in large numbers. We’ll make this change in `Scoreboard`:
```Python title:scoreboard.py
	def prep_score(self):
		"""Turn the score into a rendered image."""
		rounded_score = round(self.stats.score, -1)
		score_str = f"{rounded_score:,}"
		self.score_image = self.font.render(score_str, True, self.text_color, self.settings.bg_color)
		--snip--
```

The `round()` function normally rounds a float to a set number of decimal places given as the second argument. However, when you pass a negative number as the second argument, `round()` will round the value to the nearest 10, 100, 1000, and so on. This code tells Python to round the value of `stats.score` to the nearest 10 and assign it to `rounded_score`.

We then use a format specifier in the f-string for the score. A *format specifier* is a special sequence of characters that modifies the way a variable’s value is presented. In this case, the sequence `:,` tells Python to insert commas at appropriate places in the numerical value that’s provided. This results in strings like `1,000,000` instead of `1000000`.

#### High Scores
Every player wants to beat a game’s high score, so let’s track and report high scores to give players something to work toward. We’ll store high scores in `GameStats`:
```Python title:game_stats.py
	def __init__(self, ai_game):
		--snip--
		# High score should never be reset.
		self.high_score = 0
```

Because the high score should never be reset, we initialize `high_score` in `__init__` rather than in `reset_stats()`.

Next, we’ll modify `Scoreboard` to display the high score. Let’s start with the `__init__()` method:
```Python title:scoreboard.py
	def __init__(self, ai_game):
		--snip--
		# Prepare the initial score images.
		self.prep_score()
		self.prep_high_score()
```

The high score will be displayed separately from the score, so we must add a new method, `prep_high_score()` to prepare the high-score image.
```Python title:scoreboard.py
	def prep_high_score(self):
		"""Turn the high score into a rendered image."""
		high_score = round(self.stats.high_score, -1)
		high_score_str = f"{high_score:,}"
		self.high_score_image = self.font.render(high_score_str, True, self.text_color, self.settings.bg_color)

		# Center the high score at the top of the screen.
		self.high_score_rect = self.high_score_image.get_rect()
		self.high_score_rect.centerx = self.screen_rect.centerx
		self.high_score_rect.top = self.score_rect.top
```

We round the high score to the nearest 10 and format it with commas. We then generate an image from the high score, center the high score `rect` horizontally, and set its `top` attribute to match the top of the score image.

The `show_score` method now draws the current score at the top right and the high score at the top center of the screen:
```Python title:scoreboard.py
	def show_score(self):
		"""Draw score to the screen."""
		self.screen.blit(self.score_image, self.score_rect)
		self.screen.blit(self.high_score_image, self.high_score_rect)
```

To check for high scores, we’ll write a new method, `check_high_score()`, in `Scoreboard`:
```Python title:scoreboard.py
	def check_high_score(self):
		"""Check to see if there's a new high score."""
		if self.stats.score > self.stats.high_score:
			self.stats.high_score = self.stats.score
			self.prep_high_score()
```

The method checks the current score against the high score. If the current score is greater, it replaces the value stored in `high_score` and calls `prep_high_score()` to update the high score’s image.

We must call `check_high_score()` each time an alien is hit after updating the score in `_check_bullet_alien_collisions()`:
```Python title:alien_invasion.py
	def _check_bullet_alien_collisions(self):
		--snip--
		if collisions:
			for aliens in collisions.values():
				self.stats.score += self.settings.alien_points * len(aliens)
			self.sb.prep_score()
			self.sb.check_high_score()
		--snip--
```

We call `check_high_score()` when the `collisions` dictionary is present, and we do so after updating the score for all the aliens that have been hit.

#### Displaying the Level
To display the player’s level in the game, we first need an attribute in `GameStats` representing the current level. To reset the level at the start of each new game, initialize it in `reset_stats`:
```Python title:game_stats.py
	def reset_stats(self):
		"""Initialize statistics that can change during the game."""
		self.ships_left = 0
		self.level = 1
```

To have `Scoreboard` display the current level, we call a new method, `prep_level()` from `__init__()`:
```Python title:scoreboard.py
	def __init__(self, ai_game):
		--snip--
		self.prep_high_score()
		self.prep_level()
```

Here’s `prep_level()`:
```Python title:example.py
	def prep_level(self):
		"""Turn the level into a rendered image."""
		level_str = str(self.stats.level)
		self.level_image = self.font.render(level_str, True, self.text_color, self.settings.bg_color)

		# Position the level below the score.
		self.level_rect = self.level_image.get_rect()
		self.level_rect.right = self.score_rect.right
		self.level_rect.top = self.score_rect.bottom + 10
```

The `prep_level()` method creates an image from the value stored in `stats.level` and sets the image’s `right` attribute to match the score’s `right` attribute. It then sets the `top` attribute 10 pixels beneath the bottom of the score image to leave space between the score and the level.

We must also update `show_score()`:
```Python title:scoreboard.py
	def show_score(self):
		"""Draw scores and level to the screen."""
		self.screen.blit(self.score_image, self.score_rect)
		self.screen.blit(self.high_score_image, self.high_score_rect)
		self.screen.blit(self.level_image, self.leve_rect)
```

This new line draws the level image to the screen.

We’ll increment `stats.level` and update the level image in `_check_bullet_alien_collisions()`:
```Python title:alien_invasion.py
	def _check_bullet_alien_collisions(self):
		--snip--
		if not self.aliens:
			# Destroy existing bullets and create new fleet.
			self.bullets.empty()
			self._creat_fleet()
			self.settings.increase_speed()

			# Increase level.
			self.stats.level += 1
			self.sb.prep_level()
```

If a fleet is destroyed, we increment the value of `stats.level` and call `prep_level()` to make sure the new level displays correctly.

To ensure the level image updates properly at the start of a new game, we also call `prep_level()` when the player clicks the Play button:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		--snip--
		if button_clicked and not self.game_active:
			--snip--
			self.sb.prep_score()
			self.sb.prep_level()
			--snip--
```

We call `prep_level()` right after calling `prep_score()`.

#### Displaying the Number of Ships
Finally, let’s display the number of ships the player has left, but this time, let’s use a graphic. To do so, we’ll draw ships in the upper-left corner of the screen to represent how many ships are left, just as many classic arcade games do.

First, we need to make `Ship` inherit from `Sprite` so we can create a group of ships:
```Python title:ship.py
import pygame
from pygame.sprite import Sprite

class Ship(Sprite):
	"""A class to manage the ship."""

	def __init__(self, ai_game):
		"""Initialize the ship and set its starting position."""
		super().__init__()
		--snip--
```

Next, we must modify `Scoreboard` to create a group of ships we can display. Here are the `import` statements for `Scoreboard`:
```Python title:scoreboard.py
import pygame.font
from pygame.sprite import Group

from ship import Ship
```

Because we’re making a group of ships, we import the `Group` and `Ship` classes.

Here’s `__init__()`:
```Python title:scoreboard.py
	def __init__(self, ai_game):
		"""Initialize scorekeeping attributes."""
		self.ai_game = ai_game
		self.screen = ai_game.screen
		--snip--
		self.prep_level()
		self.prep_ships()
```

We assign the game instance to an attribute, because we’ll need it to create some ships. We call `prep_ships()` after the call to `prep_level()`. Here’s `prep_ships()`:
```Python title:scoreboard.py
	def prep_ships(self):
		"""Show how many ships are left."""
		self.ships = Group()
		for ship_number in range(self.stats.ships_left):
			ship = Ship(self.ai_game)
			ship.rect.x = 10 + ship_number * ship.rect.width
			ship.rect.y = 10
			self.ships.add(ship)
```

The `prep_ships()` method creates an empty group, `self.ships`, to hold the ship instances. To fill this group, a loop runs once for every ship the player has left. Inside the loop, we create a new ship and set each ship’s *x*-coordinate value so the ships appear next to each other with a 10-pixel margin on the left side of the group of ships. We set the *y*-coordinate value 10 pixels down from the top of the screen so the ships appear in the upper-left corner of the screen. Then we add each new ship to the group `ships`.

Now we must draw the ships to screen:
```Python title:scoreboard.py
	def show_score(self):
		"""Draw scores, level, and ships to screen."""
		--snip--
		self.ships.draw(self.screen)
```

To show the player how many ships they have to start with, we call `prep_ships()` when a new game starts. We do this in `_check_play_button()` in `AlienInvasion`:
```Python title:alien_invasion.py
	def _check_play_button(self, mouse_pos):
		--snip--
		if button_clicked and not self.game_active:
			--snip--
			self.sb.prep_level()
			self.sb.prep_ships()
			--snip--
```

We also call `prep_ships()` when a ship is hit, to update the display of ship images when the player loses a ship:
```Python title:alien_invasion.py
	def _ship_hit(self):
		"""Respond to ship being hit by alien."""
		if self.stats.ships_left > 0:
			# Decrement ships_left, and update scoreboard.
			self.stats.ships_left -= 1
			self.sb.prep_ships()
			--snip--
```

