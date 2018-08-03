# Classes

```python
class Person:
    def __init__(self, firstName, lastName): #constructor
        self.firstName = firstName
        self.lastName = lastName

    def __repr__(self): #how it is printed
        return self.firstName + " " + self.lastName
    
    def __del__(self): #run when last reference to it goes out of scope
        print self.id, 'died'
```

No private variables, `self._x` just indicates private not enforced

