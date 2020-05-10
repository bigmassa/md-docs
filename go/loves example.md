# Loves Example

> 1. Take two people's names and the word 'loves'.
>2. Count the number of occurences of each of the letters in 'loves' within their names.
> 3. Add each number together with its next one to get a new number
>
> 4. keep repeating this till you reach a result of 100 or less.
>
> 5. The value is how much of a percent the two people are in love.
>
> Result: 66

```go
package main

import (
	"fmt"
	"strconv"
	"strings"
)

func main() {
	person1 := "romeo montague"
	person2 := "juliet capulet"
	maxRuns := 500
	maxLength := 1000

	words := strings.ToLower(person1 + person2)

	nums := []int{
		strings.Count(words, "l"),
		strings.Count(words, "o"),
		strings.Count(words, "v"),
		strings.Count(words, "e"),
		strings.Count(words, "s"),
	}

	run := 1
	current := nums

	for {
		fmt.Printf("run: %v, len: %v\n", run, len(current))

		new := []int{}

		for i, v := range current {
			if i == 0 {
				continue
			}
			val := current[i-1] + v
			if val >= 10 {
				valStr := strconv.Itoa(val)
				valStrSplit := strings.SplitAfter(valStr, "")
				if v, err := strconv.Atoi(valStrSplit[0]); err == nil {
					new = append(new, v)
				}
				if v, err := strconv.Atoi(valStrSplit[1]); err == nil {
					new = append(new, v)
				}
			} else {
				new = append(new, val)
			}
		}

		current = new

		if len(current) <= 3 {
			res := strings.Trim(strings.Join(strings.Fields(fmt.Sprint(current)), ""), "[]")
			if r, err := strconv.Atoi(res); err == nil {
				if r <= 100 {
					fmt.Printf("result: %v\n", r)
					break
				}
			}
		}

		if len(current) >= maxLength || run >= maxRuns {
			fmt.Println("result: your love is endless and will last forever")
			break
		}

		run++
	}
}
```

