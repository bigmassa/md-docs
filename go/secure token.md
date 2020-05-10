# Secure Token

> Create a base64 encoded token to use with `github.com/gorilla/sessions`. Copy and paste into [https://play.golang.org/](https://play.golang.org/).

```go
package main

import (
	"encoding/base64"
	"fmt"

	"github.com/gorilla/securecookie"
)

func main() {
	key := securecookie.GenerateRandomKey(32) // 32 or 64
	encoded := base64.StdEncoding.EncodeToString(key)
	fmt.Println(encoded)
}
```

