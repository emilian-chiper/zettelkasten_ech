### Meta
2024-10-31 23:48
**Tags:** [[python]] [[py_basics]] [[py_user_input_while_loops]]
**Status:** #completed 

### The problem
A `for` loop is effective for looping through a list, but you shouldn’t modify a list inside a `for` loop because Python will have trouble keeping track of the items in the list.

#### Moving Items from One List to Another
```Python title:example.py
# Start with users that need to be verified,
#  and an empty list to hold confirmed users.
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

# Verify each user until there are no more unconfirmed users.
# Move each verified user into the list of confirmed users.
while unconfirmed_users:
	current_user = unconfirmed_users.pop()

	print(f"Verifying user: {current_user.title()}")
	confirmed_users.append(current_user)

# Display all confirmed users.
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
	print(confirmed_user.title())

"""
Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
"""
```

### Removing All Instances of Specific Values from a List
```Python title:example.py
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
	pets.remove('cat')

print(pets)

"""
['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
"""
```

### Filling a Dictionary with User Input
```Python title:example.py
responses = {}
# Set flag to indicate polling is active
polling_active = True

while polling_active:
	# Prompt for username and response.
	name = input("\nWhat is your name? ")
	response = input("Which mountain would you like to climb someday? ")

	# Store the response in the dictionary.
	responses[name] = response

	# Find if there are any other poll takers.
	repeat = input("Would you like to let another person respond? (yes/no) ")
	if repeat == 'no':
		polling_active = False

# Polling is complete. Show the results.
print("\n--- Poll Results ---")
for name, response in responses.items():
	print(f"{name} would like to climb {response}.")

"""
What is your name? Eric
Which mountain would you like to climb someday? Denali
Would you like to let another person respond? (yes/ no) yes

What is your name? Lynn
Which mountain would you like to climb someday? Devil's Thumb
Would you like to let another person respond? (yes/ no) no

--- Poll Results ---
Eric would like to climb Denali.
Lynn would like to climb Devil's Thumb.
"""
```