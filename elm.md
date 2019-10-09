# Elm

Functional language that compiles to js

- No runtime errors in practice. No null. No undefined is not a function. 
- You must handle all cases, statically typed

## Functions

Elm has implicit functions, cant change global variables in its

```elm
add : Int -> Int -> Int
add num1 num2 = num1 + num2
```

No loops in elm, currying by default(give one argument returns curried ft)

```elm
babyAnimals a b = "i love a" ++ a ++ " and " ++ b
babyKoalas = babyAnimals "koalas"
babyKoalas "puppies" -- "i love koalas and puppies"
```

Chaining so no unneeded variables(like lodash chain)

## Types

Would have to deal with if mix every time

```elm
type Disposition = Surly | Friendly | Ambivalent | Mix Disposition Disposition
type alias Cat = {
	name: String,
	weight: Float,
	disposition: Disposition
}
seamus = Cat "Seamus" 22.2 Surly
```

## Maybe

```elm
type Maybe a
   = Just a 
   | 
   
type alias User = 
{ name: String
  , age: Maybe Int
}

sue: User
sue = {name = "Sue", age = "Nothing"}
canBuyAlcohol user = 
  case user.age of 
    Nothing -> False
    Just age -> age >= 21
```

## Json

Must decode and type JSON, must write decoder

## Build for Production

```bash
elm-make src/Main.elm --output=build/main.js
```

```html
<script src="Build/main.js"></script>
<script>
	const node = document.getElementbyId('main');
  const app = Elm.Main.embed(node);
</script>
```

