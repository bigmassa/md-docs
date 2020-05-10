# Run System Command

> The Command function within the os/exec package accepts at least one string - the name of the command/binary you’re trying to run - followed by any number of strings for it’s parameters.

```go
package main

import (
    "fmt"
    "log"
    "os/exec"
)

func main() {

    // Print Go Version
    cmdOutput, err := exec.Command("go", "version").Output()
    if err != nil {
        log.Fatal(err)
    }

    fmt.Printf("%s", cmdOutput)
}
```

