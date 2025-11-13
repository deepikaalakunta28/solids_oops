## SOLIDS
**SOLID:**
SOLID is a set of five object-oriented design principles that help you write clean, maintainable, and easy-to-extend code.

- SOLID Stand for:

**S** – Single Responsibility Principle
**O** – Open/Closed Principle
**L** – Liskov Substitution Principle
**I** – Interface Segregation Principle
**D** – Dependency Inversion Principle

**1. Single Responsibility Principle (SRP):**
A class should do only one job and have only one reason to change.

```python
#  Bad Example 
class Invoice:
    def calculate_total(self):
        pass
    def print_invoice(self):
        pass
    def save_to_db(self):
        pass

# Good Example (follows SRP)
class Invoice:
    def calculate_total(self):
        pass

class InvoicePrinter:
    def print_invoice(self, invoice):
        pass

class InvoiceRepository:
    def save_to_db(self, invoice):
        pass

```

**2. Open/Closed Principle (OCP):**
Classes should be open for extension but closed for modification.

- Example:
```python
#  Bad Example
class Discount:
    def get_discount(self, customer_type):
        if customer_type == "regular":
            return 5
        elif customer_type == "vip":
            return 10

#  Good Example
class Discount:
    def get_discount(self):
        return 5

class VIPDiscount(Discount):
    def get_discount(self):
        return 10

```

**3. Liskov Substitution Principle (LSP):**
A child class must be usable in place of its parent class without breaking anything.
Objects of a superclass should be replaceable with objects of its subclass without breaking the application.

- Example:
```python
# Good Example
class Bird:
    def make_sound(self):
        print("Chirp!")

class FlyingBird(Bird):
    def fly(self):
        print("I can fly!")

class Sparrow(FlyingBird):
    pass

class Ostrich(Bird):
    pass

# Works fine — all are Birds
birds = [Sparrow(), Ostrich()]
for b in birds:
    b.make_sound()

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
High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend on abstractions.
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


## OOPS
1. Class & Object
2. Encapsulation
3. Abstraction
4. Inheritance
5. Polymorphism
6. Method Overloading & Overriding
7. Super()

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

## 2. Encapsulation:
Encapsulation means hiding the internal details of an object and only exposing what is necessary.
### Why Encapsulation?
To protect data from unintended access or modification.

To control how data is accessed or updated.

To make code modular, secure, and easier to maintain.
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
### Why Abstraction 
Abstraction is used to simplify complex systems by hiding unnecessary implementation details and showing only the essential features of an object.
- Example:
```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class CreditCardPayment(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} using Credit Card.")

class PayPalPayment(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} using PayPal.")

# Using abstraction
def complete_payment(payment_method, amount):
    payment_method.pay(amount)

p1 = CreditCardPayment()
p2 = PayPalPayment()

complete_payment(p1, 500)
complete_payment(p2, 1000)

```

## 4. Inheritance
- Inheritance is an OOP concept where one class (child/subclass) acquires the properties and behaviors of another class (parent/superclass).

 1. Single Inheritance
 2. Multiple Inheritance
 3. Hierarchical Inheritance
 4. Multilevel Inheritance

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


** 5.Polymorphism **
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

## 6. Method Overloading and Method Overriding

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

## 7. super()
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



**References**
Real Python — Object-Oriented Programming in Python
- https://realpython.com/python3-object-oriented-programming
- https://www.geeksforgeeks.org/python/python-oops-concepts/
- https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english





