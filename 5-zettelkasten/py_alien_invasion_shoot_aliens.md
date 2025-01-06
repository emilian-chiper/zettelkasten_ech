### Meta
2024-12-22 12:24
**Tags:** [[py_projects]] [[py_alien_invasion]] [[py_ai_aliens]]
**Status:** #completed 

### Shooting Aliens
We’ve built our ship and fleet of aliens, but when the bullets reach the aliens, they simply pass through because w'e aren’t checking for collisions. In the game programming, *collisions* happen when game elements overlap. To make the bullets shoot down aliens, we’ll use the function `sprite.groupcollide()` to look for collisions between numbers of two groups.

#### Detecting Bullet Collisions
We want to know right away when a bullet hits an alien so we can make an alien disappear as soon as it’s hit. To do this. we’ll look for collisions immediately after updating the position of all the bullets.

The `sprite.groupcolide()` function compares the `rects` of each element in one group with the `rects` of each element in another group. In this case, it compares each bullet’s `rect` with each alien’s `rect` and returns a dictionary containing the bullets and liens that have collided. Each key in the dictionary will be a bullet, and the corresponding value will be the alien that was hit.

Add the following code to the end of `_update_bullets()` to check for collisions between bullets and aliens:
```Python title:alien_invasion.py
	def _update_bullets(self):
		"""Update position of bullets and get rid of old bullets."""
		--snip--

		# Check for any bullets that have hit aliens.
		# If so, get rid of the bullet and the alien.
		collisions = pygame.sprite.groupcollide(self.bullets, self.aliens, True, True)
```

The new code we added compares the positions of all the bullets in `self.bullets` and all the aliens in `self.aliens`, and identifies any that overlap. Whenever the `rects` of a bullet and alien overlap, `groupcollide()` adds a key-value pair to the dictionary it returns. The two `True` arguments tell Pygame to delete the bullets and aliens that have collided. (To make a high-powered bullet that can travel to the top of the screen, destroying every alien in its path, you could set the first Boolean argument to `False` and keep the second Boolean argument set to `True` The aliens hit would disappear, but all bullets would stay active until they disappeared off the top of the screen.)

#### Repopulating the Fleet
One key feature of *Alien Invasion* is that the aliens are relentless: every time the fleet is destroyed, a new fleet should appear.

To make a new fleet of aliens appear after a fleet has been destroyed, we first check whether the `aliens` group is empty. If so, we make a call to `_create_fleet()`. We perform this check at the end of `_update_bullets()`, because that’s where the individual aliens are destroyed.
```Python title:alien_invasion.py
	def _update_bullets(self):
		--snip--
		if not self.aliens:
			# Destroy existing bullets and create new fleet.
			self.bullets.empty()
			self._create_fleet()
```

#### Speeding Up the Bullets
Change the value in *settings.py*:
```Python title:settings.py
	# Bullet settings
	self.bullet_speed = 2.5
	self.bullet_width = 3
	--snip--
```

#### Refactoring `_update_bullets()`
```Python title:alien_invasion.py
	def _update_bullets(self):
		--snip--
		# Get rid of bullets that have disappeared.
		for bullet in self.bullets.copy():
			if bullet.rect.bottom <= 0:
				self.bullets.remove(bullet)

		self._check_bullet_alien_collisions()

	def _check_bullet_alien_collisions(self):
		"""Respond to bullet-alien collisions."""
		# Remove any bullets and aliens that have collided.
		collisions = pygame.sprite.groupcollide(
			self.bullets, self.aliens, True, True)
		if not self.aliens:
			# Destroy existing bullets and create new fleet.
			self.bullets.empty()
			self._create_fleet()
```