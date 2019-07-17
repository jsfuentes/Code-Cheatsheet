# Database Desigm

Minimize data reduncancy with **normalization**

One Primary Keys must be unique, unchanging, non null

[Understanding Query Optimization](https://www.sqlite.org/queryplanner.html):

## Indexes

- none indexes mean full table lookups vs index that binary tree the shit, none primary key indexes create new tiny table for 2 binary tree lookups
- Updating indexes takes longer

##### Should I use a id(surrogate key) or a unique attribute(natural key) for the primary key?

- Be consistent for your entire database so people don't get confused whats the foreign key
- Natural connection to real world that may change and requires some thought, natural more clear when reading in db

## Relationships

### Parent-child 

- one to many
- child has foreign key that is primary key of parent
- Parent is person ordering or author, child is order or book

### Many to Many

- Problems: Lists of ids are hard to maintain and both try to be parents

- Solution: Joining/bridging/intermediate table that becomes the child of both parents. **Compound/composite key** here

- | Student | Class |
  | ------- | ----- |
  | 3       | 4     |
  | 3       | 5     |
  | 5       | 4     |

### Lookup Table

Now have a lu_membership lookup table, that is foreign key in member table instead of stored with member. 

| id   | Membership |
| ---- | ---------- |
| 1    | Bronze     |
| 2    | Silver     |
| 3    | Gold       |

Foreign key constraints means all members can only have memberships that exist, updates to membership ez 

## Foreign Key Constraints

FK constraints refers to what happens to parents referenced by children:

- on delete
- on update

For each action can:

- restrict(stops action)
- cascade(update/delete children as well)
- set null(remove foreign key reference)

## Normalization

**1st Normal Form:** Single elements, not lists. Create new tables with a row with foreign key_id and each element of list

**2nd Normal Form:** Keep attributes in correct table

**3rd Normal Form:** Column depends on column which depends on pk. Transitive dependency: an attribute depends on anthoer attribute in the row i.e star, star meaning which depends on type. Should create new table for stars

## Other

#### Enums

Lets say you use gender across tables like as a requirement of group membership or person

Would you make a table with 

| id   | title  |
| ---- | ------ |
| 1    | male   |
| 2    | female |

And then reference it with foreign keys

Compared to just storing `male` everywhere db level enums are  better b/c:

- foreign key database level assurance (not for lists)
- easy cross platform changes as not typed to code 
- Removes constants in code and puts in db

Worse b/c:

- support weird/difficult seeing gender = 1

##### Naming

`User` or `Users` => [survey](https://stackoverflow.com/questions/338156/table-naming-dilemma-singular-vs-plural-names) says singular cuz 

- slightly clearer on JOINs like join on user, though worse on slect from user, but you can consider it the user table 
- Consistency: Plural forms vary word to word(status, news), what if each entry is plural like studentfacts facts
- In alphabetical order, order then orderdetails better than orderdetails then orders
- less letters :)