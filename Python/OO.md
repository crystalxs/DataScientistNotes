# Object-Oriented programming

A *class* is the **blueprint** for an object and is basically the name of the type.

An *object* is called an **instance** of the class.

## Class elements

| Object-Oriented             | Function-Oriented |
| --------------------------- | ----------------- |
| methods                     | functions         |
| fields / instance variables | variables         |

Fields are the *state* of the object.

Methods are the *behavior* of the object.

## Object-Oriented Programming Properties

The class *encapsulates* the state and behavior of an object.

*Inheritance* behaves like an `import` or include operation from another class into a new class.

###Definition (Encapsulation)

By convention, class names should be **capitalized** like `Point`.

```python
class Book:
	def __init__(self, title, author):
        self.title = title
        self.author = author
        self.chapters = []
        self.sold = 0
        
    def __str__(self):
    # called when conversion to string needed
    	return f"Book({self.title}, {self.author}, sold={self.sold})"
    
    def __repr__(self):
    # called in interactive mode
    	return self.__str__()
    
    def sell(self, n):
        self.sold += n

# define an object that has no methods and no fields 
# but then can add fields dynamically with assignment statements
# couldn't easily define methods associated with object
class Book:
	pass
```

* All methods defined within an object, must have an explicit first argument called `self`.

###Inheritance

**Inheritance** is the ability for one class to be related to another class in much the same way that people can be related to one another. Children inherit characteristics from their parents. These classes are often referred to as **subclasses**and **superclasses**.

```python
class Account:
    def __init__(self, starting):
        self.balance = starting

    def add(self, value):
        self.balance += value

    def total(self):
        return self.balance
    
    
    
class InterestingAccount(Account): # derive from super class to get subclass
    def __init__(self, starting, rate):
        self.balance = starting # super().__init__(starting)
        self.rate = rate
        
    def total(self): # OVERRIDE method
        return self.balance + self.balance * self.rate
 
    def profit(self):
        return self.balance * self.rate
```

### Abstraction

### Polymorphism

