# Swift

## Functions
```
func addTwoNumbers(a:Int, b:Int) -> Int {
    return a+b;
}

print(addTwoNumbers(a: 5, b: 6))
```
Notice the **MANDATORY** typing and naming parameters

## Classes
```
class Rat {
    var health = 5;
}

class Bplate {
    let numberOfIngredientsICantPronounce = 50
    var m_rat: Rat?

    func checkForRat(exterminationInstruction: (Rat) -> Void) {
        if let rat = m_rat{
            exterminationInstruction(rat)
        }
    }
}
```



## Functions as parameters...
func exterminateRat(rat: Rat) {
    print("rip Remy")
    rat.health = 0
}

let myBplate = Bplate()
myBplate.m_rat = Rat()
myBplate.checkForRat(exterminationInstruction: exterminateRat)

## Closure
myBplate.checkForRat(exterminationInstruction: {
    (rat: Rat) in //could specifiy return type too (rat: Rat) -> Void
    print("this is why USC is the lamer school")
    rat.health = 0
})



## Typing
```swift
class Bird {
    func fly() {print("fly")}
}
class Swan: Bird {
    func poop() {}
}

var myBird: Bird
myBird = Swan()

if let forSureSwan = myBird as? Swan {
    forSureSwan.fly()
}

guard let data = response.result.value as? [String : Any] else {
    print("could not parse JSON")
    return
}
```

## Strings

aString.replacingOccurrences("\n", "")

#### PYTHON SPLIT
```
import Foundation

var str: String = "First Last"
var strArr = str.components(separatedBy: " ")
```
