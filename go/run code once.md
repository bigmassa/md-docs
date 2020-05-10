# Run Code Once

> Using a web server as an example, there are multiple stages you can load resources. Within the main() function and within the handler are the obvious two - each with their own advantages and disadvantages. Within the main function can hinder the start-up time of the server, while code within the handler is run on every request.
>
> Sometimes we want to load a resource only once and when it’s first needed. This means it needs to be in the http handler. We have to be careful how we do this though, as each time the handler is called it will be in a separate goroutine. We could use a global variable and if it hasn’t been set (or == nil), load the resource - but this won’t be safe from a concurrency point of view as you could end up running the load sequence twice.
>
> The best way to achieve this is therefore using the sync.Once mutex to efficiently run code once even across goroutines. The example below should demonstrate this.
>
> Copy and paste into [https://play.golang.org/](https://play.golang.org/).

```go
package main

import (
    "fmt"
    "sync"
)

var doOnce sync.Once

func main() {
    DoSomething()
    DoSomething()
}

func DoSomething() {
    doOnce.Do(func() {
        fmt.Println("Run once - first time, loading...")
    })
    fmt.Println("Run this every time")
}
```