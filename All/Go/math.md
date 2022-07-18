# Math

common ops

```go
var int1 int = 5
var float1 float64 = 42
sum := float64(int1) + float1
```

#### `math` packageeee 

math.Pi

#### Big Num to get precision

```go
import "math/big"

var b1, b2, b3, bigSum big.Float
b1.SetFloat64(23.5)
b2.SetFloat64(65.1)
b3.SetFloat64(76.3)

bigSum.Add(&b1, &b2).Add(&bigSum, &b3)
fmt.Printf("BigSum = %.10g\n", &bigSum)
```

### Converstion

```go
price, _, _ := big.ParseFloat(p, 10, 2, big.ToZero) //base 10, precision 2, rounding mode tozero
```

