
Python was created in the late 1980s by Guido van Bossum.

Python's defining characteristics: 
1. Interpreted language
2. High-level language
3. Object-Oriented Programming (OOP)

### Fundamental elements of Python syntax:
- Indentation
- Statements
- Variables
- Comments


```python
if points >= 1000:

print("You've achieved Platinum status! Enjoy exclusive benefits.")
elif points >= 500:
print("You're a Gold member! Thank you for your loyalty.")
elif points >= 100:
print("Welcome to the Silver tier! Start earning rewards.")
else:
print("You're a Bronze member. Keep shopping to earn more points!")
```

Basic arithmetic operations

Addition +

Subtraction -

Multiplication *

Division /

### Less frequent arithmetic operations

Floor Division // Performs division and discards any remainder, resulting in a whole number (so 7 // 4 is 1, as 4 goes into 7 a single time evenly). May also be referred to as integer division.

Modulo % Returns the remainder after integer division (so 7 % 4 is 3, as the division has a remainder of 3).

Exponentiation ** Raises a number to the power of another number. To write 24, or two to the fourth power, you write 2 ** 4.

## Loops

```python
for i in range(1, 11):
 print(i)

valid_input = False
while not valid_input:
user_input = int(input("Please enter a number greater than 0: "))
if user_input > 0:
valid_input = True
else:
print("Invalid input. Please try again.")

```

range()

- range(stop): It generates a sequence of numbers starting from 0 (by default) up to, but not including, the stop value, increasing by 1 each time. So, range(5) would loop from 0 through 4.

- range(start, stop): This form allows you to specify the starting value of the sequence. It generates numbers starting from start up to, but not including, the stop value, increasing by 1 each time. So, range (1, 11) would loop from 1 through 10.

- range(start, stop, step)


```python
fruits = ["apple", "banana", "cherry"]
first_fruit = fruits[0]
fruit_length = len(fruits)
print(fruit_length)
fruits.append("date")


students = ["Alice", "Bob", "Charlie"]

for student in students:
  print("Hello,", student)

for i in range(0,len(students)):
  print("Hello,", students[i])
```

### Immutable values

In Python, strings are immutable, meaning their contents cannot be changed after they're created. The code below attempts to change the first character of the string "Hello" from 'H' to 'h'. However, this will result in a TypeError because strings are immutable.

```python 
value = "Hello"
value[0] = 'h' # gives error
print(value) 

#solution
value = "Hello"
new_value = "h" + value[1:]
print(new_value) # Output: hello
```

## Lists

Lists are fundamental data structures in Python, serving as versatile containers for storing collections of items.

**Empty list**: Your program needs to have a list that will be loaded during program execution. You might get values from the user or from a file and store them during program execution. The list must be initialized first.

new_list = []

**Prime numbers**: Your program needs to keep track of prime numbers. You want to declare this list to hold all prime numbers 13 and under as integers:

primes = [2, 3, 5, 7, 11, 13]

**Vowels**: Your program needs to store vowels for use in a comparison. You want to declare this list to hold all vowels as strings:

vowels = ["a", "e", "i", "o", "u"]

**True/false results**: Your program needs to store a history of the result of coin flips (True represents heads, False represents tails): 

coin_flips = [True, False, True, True, False]


### Slicing: Accessing a portion of your list

Sometimes, you only need a portion of your list. Imagine you only want to see the first two elements on a list. Python lets you extract a "slice" of your list, like this:

grocery_list = ["milk", "hummus", "bread", "cheese", "apples"]
print(grocery_list[0:2])

### List Comprehensions: A Concise Approach

[expression for item in iterable]

```python
exam_scores = [55, 70, 78, 52, 68]

curve_amount = 10

# Use a list comprehension to create a new list of curved grades
curved_grades = [score + curve_amount for score in exam_scores]
print("Original scores:", exam_scores)
print("Curved scores:", curved_grades)
```

### Two-Dimensional Lists: Lists within Lists

grid = [
  [1, 2, 3],

  [4, 5, 6],

  [7, 8, 9]

]

|Command|What it does|
|---|---|
|len(list)|Tells you how many things are in the list.|
|list.append(x)|Adds x to the end of the list.|
|list.insert(i, x)|Adds x at position i in the list.|
|list.remove(x)|Removes the first x from the list.|
|list.sort()|Arranges the list in order.|
|list.reverse()|Reverses the order of the items in the list.|
|list.count(x)|Counts how many times x appears in the list.|
|x in list|Checks if x is in the list.|
|list.index(x)|Tells you the position of the first x in the list.|
## Functions

```python
def function_name(parameters):  
    """Docstring to explain what function does"""
    # Code to perform the task
    return result
```


# Classes

Blueprints for objects
Classes contains attributes or data and methods or functions.

Classes have three important abilities: 
- Encapsulation
- Inheritance
- Polymorphism

## Functions in the modern Python ecosystem

Python's rich standard library and the vast ecosystem of third-party packages are built upon functions. Mastering functions is essential for leveraging these tools to build robust and scalable applications. Python offers a range of features that enhance the power of functions:

- **Decorators:** These special functions modify the behavior of other functions without changing their core logic. For example, a @cache decorator could store the results of a computationally expensive function, avoiding redundant calculations.

- **Generators:** These special functions produce a sequence of values on demand, improving memory efficiency and enabling elegant solutions for tasks like processing large datasets. A generator function might yield one line of a file at a time, allowing you to process the file without loading it entirely into memory.

- **F-strings:** These formatted string literals provide a concise and readable way to embed expressions directly within strings, making it easier to generate dynamic output within your functions. For instance, you could use an f-string to format a greeting message like this: f"Hello, {name}! Today is {date.today()}."

- **Type Hints:** These annotations specify the expected data types for function arguments and return values, improving code clarity and enabling static type checking tools to catch potential errors early in the development process. For example, you could define a function like this: def calculate_area(length: float, width: float) -> float: ...


## Variables scope

## The LEGB rule: Python's search strategy for variables

When you use a variable in your code, Python embarks on a systematic search to find its value. The search order is described by the LEGB rule:

1. **Local (L):** Python first checks if the variable exists within the current function or code block.

2. **Enclosing (E):** If not found locally, it looks in enclosing functions (if you're using nested functions, like Russian dolls).

3. **Global (G):** Next, it searches the global scope, i.e., variables defined at the top level of your module.

4. **Built-in (B):** Finally, it checks Python's built-in namespace for pre-defined functions and objects like print, list, etc.


## Encapsulation

```python
class BankAccount:

   def __init__(self, balance):
      self._balance = balance # Private attribute

   def deposit(self, amount):
      self._balance += amount

   def get_balance(self):
      return self._balance
```

## Abstraction

Python's abc module (Abstract Base Classes) takes this a step further by enabling you to define abstract base classes.

```python
from abc import ABC, abstractmethod

class Animal(ABC): # Abstract base class
   @abstractmethod
   def make_sound(self):
      pass

  
class Dog(Animal): # Concrete subclass
  def make_sound(self):
    return "Bark!"
```


**The** __init__ **method: A special constructor**

The __init__ method, often called the constructor, is a special method that Python automatically calls when you create a new object of your class.

```python
def calculate_diameter_circle(radius: float) -> float:

"""Function to return the diameter of the circle"""
    if(radius < 0):
        return -1

    return 2*radius
```

### Variable Number of Arguments (*args and **kwargs) 

Python allows you to define functions that accept a variable number of arguments. You can use *args to collect positional arguments into a tuple and **kwargs to collect keyword arguments into a dictionary.

```python
def flexible_function(*args, **kwargs):
    print("Positional arguments:", args)
    print("Keyword arguments:", kwargs)

  

flexible_function(1, 2, 3, name="Alice", age=30)
```

## Modules

Module is container for code each module contains functions, classes and variables that are all related.

Use **import** keyword to call function provided by that module.

External libraries can be installed using pip

1. Web development - Flask, Django, Requests
2. Data science - NumPy, Pandas, Matplotlib
3. Machine learning - Scikit-learn, PyTorch

```cmd
pip install library_name
```

### Requirements files: Reproducible environments

When working on larger projects or collaborating with others, it's crucial to maintain consistency in the project's environment. A requirements file (requirements.txt) is a simple text file that lists all the packages your project depends on, along with their specific versions. This allows anyone to recreate the project environment with a single command.

pip install -r requirements.

[[Python Intermediate]]