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

## Storing and Querying Ranges

Store start and end

Query by checking if its greater than start and less then end 