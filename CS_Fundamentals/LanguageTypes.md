# Language Types

## OOP, Functional, Declaritive

### Declarative 

Express logic in code, and control flow is deduced

E.g SQL, Prolog

### Functional

Immutable, functions are first class 

Pros

- simpler rules
- better parallelism because no race conditions
- more bug free/easier to debug 

Cons

- performance can be bad 
- harder to logic sometimes
- harder to hire for 

**Statically Typed**: Variables have specific types at compiletime

**Dynamically Typed**: Variables define their type at runtime

**Strongly vs Weakly Typed** : About if it automatically converts float to integers or strings or it must be explicit

### Compiled Vs Interpreted

In principle, not a lang characteristic as you can compile or interpret a lang

##### Compiled

C++ and Java are compiled meaning they are turned in byte code and need to be precompiled

##### Interpreted

Python, JS is interpretrated meaning it is turned into byte code as needed

- Garbage collection
- dont have to define types

## Other Paradigms

##### Map Reduce

Map ft - process key/value to generate intermediate key/value

Reduce ft - merges all intermediate values with same key 

Implementation handles parallelization, machine failure, and data locality/optimization

Ship computation to machine that holds needed data instead of data to compution 

*Implementation: Master Slave with 64MB block size and redundancy, commodity machines*


