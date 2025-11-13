# OOPS AND SOLIDS CHEATSHEET

## OOPS
1. Class & Object
2. Encapsulation
3. Abstraction
4. Inheritance
5. Polymorphism
6. Constructor
7. Method Overloading & Overriding
8. Super()

## 1. Class & Object

**Class:**
A class is a blueprint that defines the structure and behavior (data + methods) of objects.

**Object:**
An object is an instance of a class created in memory.

- Example:
```python
class Student:
    def __init__(self, name, roll):
        self.name = name
        self.roll = roll

    def show(self):
        print("Name:", self.name)
        print("Roll:", self.roll)

s1 = Student("Jahnavi", 101)
s1.show()
```

## 2. Encapsulation
Encapsulation is the process of bundling data and methods together while restricting direct access using private variables.

- Example:
```python
class Bank:
    def __init__(self, balance):
        self.__balance = balance   # private variable

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

b = Bank(1000)
b.deposit(500)
print(b.get_balance())
```

## 3. Abstraction
Abstraction hides unnecessary implementation details and shows only the essential features.

- Example:
```python
from abc import ABC, abstractmethod

class Car(ABC):
    @abstractmethod
    def start(self):
        pass

class Tesla(Car):
    def start(self):
        print("Tesla starts silently")

t = Tesla()
t.start()
```

## 4. Inheritance
- Inheritance is an OOP concept where one class (child/subclass) acquires the properties and behaviors of another class (parent/superclass).

 -  There are five types of Inheritance.
 1. Single Inheritance
 2. Multiple Inheritance
 3. Hierarchical Inheritance
 4. Multilevel Inheritance
 5. Hybrid Inheritance

**1. Single Inheritance:**
A child class inherits from one parent class.

- Example:
```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def display(self):
        print("Child")

c = Child()
c.show()
c.display()
```

**2. Multiple Inheritance**
A child class inherits from more than one parent class.

- Example:
```python
class A:
    def showA(self):
        print("A")

class B:
    def showB(self):
        print("B")

class C(A, B):   # multiple inheritance
    pass

c = C()
c.showA()
c.showB()
```

**3. Hierarchical Inheritance**
Multiple child classes inherit from the same parent class.

- Example:
```python
class Parent:
    def show(self):
        print("Parent")

class Child1(Parent):
    pass

class Child2(Parent):
    pass

c1 = Child1()
c2 = Child2()

c1.show()
c2.show()
``` 

**4. Multilevel Inheritance**
Inheritance that forms a chain — child → parent → grandparent.

- Example:
```python
class A:
    def showA(self):
        print("A")

class B(A):
    def showB(self):
        print("B")

class C(B):
    def showC(self):
        print("C")

c = C()
c.showA()
c.showB()
c.showC()
```

**5. Hybrid Inheritance**
A combination of two or more types of inheritance.

- Example:
```python
class A:
    def showA(self):
        print("A")

class B(A):
    def showB(self):
        print("B")

class C:
    def showC(self):
        print("C")

class D(B, C):   # hybrid (B inherits A, D inherits B + C)
    pass

d = D()
d.showA()
d.showB()
d.showC()
```

## 5. Polymorphism
Polymorphism allows the same function name to behave differently based on the object calling it.

- Example:
```python
class Dog:
    def sound(self):
        print("Bark")

class Cat:
    def sound(self):
        print("Meow")

def make_sound(animal):
    animal.sound()

make_sound(Dog())
make_sound(Cat())
```

## 6. Constructor
A constructor (__init__) is a special method that automatically initializes object variables when the object is created.

```python
class Demo:
    def __init__(self):
        print("Object created")

d = Demo()
```

## 7. Method Overloading and Method Overriding

**Method Overloading**
Method overloading is defining multiple methods with the same name but different parameters (not natively in Python).

- Python does NOT support method overloading directly.

- Example:
```python
class Math:
    def add(self, a, b, c=0):
        return a + b + c

m = Math()
print(m.add(2, 3))
print(m.add(2, 3, 4))
```

**Method Overriding**
Method overriding is redefining a parent class method inside a child class.
- Child modifies Parent method
- Example:
```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def show(self):
        print("Child")

c = Child()
c.show()
```

## 8. super()
super() is used to call parent class methods or constructor from a child class.

- Example:
```python
class A:
    def __init__(self):
        print("A constructor")

class B(A):
    def __init__(self):
        super().__init__()
        print("B constructor")

b = B()
```

# SOLIDS

**SOLID:**
SOLID is a set of five object-oriented design principles that help you write clean, maintainable, and easy-to-extend code.
These five principles make software:
1. easier to understand
2. easier to change
3. less buggy
4. more reusable

- SOLID Stand for:

**S** – Single Responsibility Principle
**O** – Open/Closed Principle
**L** – Liskov Substitution Principle
**I** – Interface Segregation Principle
**D** – Dependency Inversion Principle

**1. Single Responsibility Principle (SRP):**
A class should do only one job and have only one reason to change.

- Bad Code(one class doing too many things)
```python
class Student:
    def save_to_db(self):
        pass
    def print_report(self):
        pass

- Good Code (Split responsibilities):
class StudentDB:
    def save(self):
        pass

class StudentReport:
    def print(self):
        pass
```

**2. Open/Closed Principle (OCP):**
Classes should be open for extension but closed for modification.

- Example:
Instead of changing existing code, we extend it.
```python
class Discount:
    def get_discount(self, amount):
        return amount * 0.10

class PremiumDiscount(Discount):
    def get_discount(self, amount):
        return amount * 0.20    # extended behavior
```

**3. Liskov Substitution Principle (LSP):**
A child class must be usable in place of its parent class without breaking anything.

- Example:
```python
class Bird:
    def fly(self):
        print("Bird flying")

class Sparrow(Bird):  # valid substitution
    pass

def make_it_fly(bird):
    bird.fly()

make_it_fly(Sparrow())   # Works perfectly
```
- A Penguin class would violate LSP because penguins cannot fly.

**4. Interface Segregation Principle (ISP):**
Don’t force a class to implement methods it does not need.

- Example:
- Bad Code:
```python
class Worker:
    def code(self): pass
    def cook(self): pass

- Good Code (Split into small Interfaces):
class Coder:
    def code(self): pass

class Chef:
    def cook(self): pass
```

**5. Dependency Inversion Principle (DIP):**
Depend on abstractions, not concrete classes.
- Example:
- Bad code:
```python
class MySQL:
    def connect(self):
        pass

class App:
    def __init__(self):
        self.db = MySQL()
```
- Good Code:
```python
class Database:
    def connect(self):
        pass

class MySQL(Database):
    def connect(self):
        pass

class App:
    def __init__(self, db: Database):
        self.db = db
```

**Simple SOLID Summary**
Principle	     Meaning
  S	       One class = one job
  O	       Extend classes without modifying old code
  L	       Child classes must replace parents safely
  I	       Don't force useless methods on a class
  D	       Depend on interfaces, not concrete classes

**References**
- https://www.geeksforgeeks.org/python/python-oops-concepts/
- https://www.youtube.com/playlist?list=PL6n9fhu94yhXjG1w2blMXUzyDrZ_eyOme





