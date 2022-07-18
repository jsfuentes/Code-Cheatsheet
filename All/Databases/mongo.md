# General Mongo

## Queries

`.find({query})` or in MongoDb Compass find

#### Example Queries

````json
{"loc" : {$regex : ".*Public Affairs Building 1015A.*"}}
{ tag: "red" }
{ tags: "red" } //tags is an array i.e ["red", "blue"]
{ dim_cm: { $gt: 25 } } //dim_cm > 25
{ dim_cm: { $gt: 15, $lt: 20 } //15 < dim_cm < 20 
{ "size.uom": "in" } //nested field
{ "size.h": { $lt: 15 }, "size.uom": "in"} //AND
{ 'instock.qty': { $lte: 20 } } //instock is an array, selects docs where some object.qty in instock array is <=20
{ item: { $not: /^p.*/ } } //find something not starting with p
````

## Structuring Schema

Embedding documents

- Embedded documents are documents with schemas of their own that are part of other documents

- Lots of unneccessary data could be sent
- Many to many get messy, great for one to one
- Memory problem

Referenced documents

- when you populate it requires an individual query for each
- saves are only atomic at the document level, so all referenced saves not atomic
- Efficiency problems

### Advanced

#####Storing and Querying Ranges 

Store start and end

Query by checking if its greater than start and less then end 