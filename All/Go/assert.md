# Assert

`import "github.com/stretchr/testify/assert"`

### Basic Example

```go
import (
  "testing"
  "github.com/stretchr/testify/assert"
)

func TestSomething(t *testing.T) {
  assert.Equal(t, "Hi", "Hi", "The two words should be the same.")
}
```

## Common

- .Equal
- .Error
- .NoError
- .True
- .False