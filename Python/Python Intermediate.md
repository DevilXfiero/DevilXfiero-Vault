
## Lists: Your versatile data containers

## Tuples: Immutable data collections

- **Creating a Tuple:** Creating a tuple is similar to creating a list, but instead of square brackets, you use parentheses to enclose your items. For example:

my_tuple = (10, 20, "python")

Here, my_tuple holds three elements: the integers 10 and 20, and the string "python."

- **Accessing Elements (Indexing and Slicing):** Just like lists, you can access individual elements of a tuple using their index, and you can extract a subset of elements using slicing. The syntax remains identical. For instance, my_tuple[2] would return the string "python," and my_tuple[0:2] would give you the first two elements (10, 20).

- **Immutability in Action:** The immutability of tuples means that once you've defined my_tuple as shown above, you won't be able to do something like my_tuple[1] = 30 or my_tuple.append("new item"). Python would raise an error if you tried to modify the tuple's contents.

## Real-world application: Geographic coordinates



## Sets: Collections of unique items

- **Creating a Set:** You can create a set by enclosing your elements within curly braces {}, separated by commas. If you try to include duplicate elements, Python automatically eliminates them. For instance:

my_set = {1, 2, 3, 3}

- **Unordered Nature:** Since sets are unordered, you can't rely on the position of elements. This means you can't access elements by index (like my_set[0]) as you would with a list.
    
- **Key Operations:** Sets are designed for efficient operations involving unique elements. You can easily:

    - add() new elements to a set.
    - remove() elements from a set.
    - Find the union() of two sets (all elements from both sets).
    - Find the intersection() of two sets (elements common to both sets).
    - Find the difference() between two sets (elements in one set but not the other).

## Dictionaries: Key-value pairs

- **Creating a dictionary:** You construct a dictionary by enclosing key-value pairs within curly braces {}. Each key-value pair is separated by a colon :, and pairs are separated by commas. For example:
    

my_dict = {"name": "Alice", "age": 30, "city": "New York"}

In this dictionary, "name," "age," and "city" are keys, and "Alice," 30, and "New York" are their corresponding values.

- **Accessing values:** To retrieve a value from the dictionary, you use its associated key. In our example, my_dict["age"] would return the value 30.

- **Mutability and flexibility:** Dictionaries are dynamic structures. You can add new key-value pairs, modify the values associated with existing keys, or even remove pairs altogether. This adaptability makes dictionaries suitable for a wide range of applications where data needs to be updated or changed over time.

- **Common operations:** Dictionaries offer a variety of convenient methods for working with key-value pairs:
    
    - get(): Safely retrieve a value by its key (returns None if the key doesn't exist).
    - items(): Get all key-value pairs as a list of tuples.
    - keys(): Get all keys in the dictionary.
    - values(): Get all values in the dictionary.
    - update(): Merge another dictionary into the existing one.

## Real-world application: Product catalog
products = {

"P101": {"name": "Laptop", "price": 999.99},

"P102": {"name": "Smartphone", "price": 599.99}

}


```python
shopping_list = ["apples", "bananas", "milk"] # List for items
item_quantities = {"apples": 3, "bananas": 1} # Dictionary for quantities

# User adds an item
shopping_list.append("eggs")
item_quantities["eggs"] = 12

# User increases the quantity of bananas
item_quantities["bananas"] += 2

# User removes apples
shopping_list.remove("apples")
del item_quantities["apples"]

# Print updated list and dictionary
print(shopping_list)
print(item_quantities)
```

## Error Handling and debugging

try and except block 

```python
import logging

my_dict = {"a": 1, "b": 2}

try:
   print(my_dict["c"])
except KeyError as e:
   logging.error(f"KeyError encountered: {e}")
finally: 
   # used to close file and cleanup resources
# Handle the error or provide a fallback mechanism
```


Raising custom exceptions
```python
class InvalidCredentialsError(Exception):
   pass

# ... later in your code ...

if not valid_credentials(username, password):
   raise InvalidCredentialsError("Incorrect username or password")
```


# Unit Testing

pytest
```python
import pytest

from your_flask_app import app # Import your Flask app

  

@pytest.fixture

def client():
  """Create a test client for interacting with the Flask app."""
  app.config['TESTING'] = True # Enable testing mode
  with app.test_client() as client:
      yield client

  

def test_user_registration(client):

   """Simulate a user registration and check the response."""
   data = {'username': 'testuser', 'email': 'testuser@example.com',          'password': 'testpassword'}
    response = client.post('/register', data=data)
    assert response.status_code == 302 # Expect a redirect after successful registration

# Further checks on database or session data can be added here

  
def test_login(client):

   """Simulate a user login and verify the response."""
   data = {'username': 'existinguser', 'password': 'correctpassword'}
   response = client.post('/login', data=data)
   assert response.status_code == 200 # Expect a successful login
   assert b'Welcome, existinguser' in response.data # Check if welcome message is present

  

# More tests for other routes, form submissions, database interactions, etc. can be added here
```

