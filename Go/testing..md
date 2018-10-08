# Testing

```go
import (
	"testing"

	"assistant/knowledge/data/json"

	"github.com/stretchr/testify/assert"
)

func TestTransformHerePhoneNumber(t *testing.T) {
	rawNumberOnlyNumbers := "6783108763"
	res, err := transformHerePhoneNumber(nil, "", rawNumberOnlyNumbers, "", "", nil, nil, nil)
	assert.NoError(t, err)
	assert.Equal(t, res, "(678)310-8763")
}
```

