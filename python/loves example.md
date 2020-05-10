# Loves Example

> 1. Take two people's names and the word 'loves'.
>
> 2. Count the number of occurences of each of the letters in 'loves' within their names.
>
> 3. Add each number together with its next one to get a new number
>
> 4. keep repeating this till you reach a result of 100 or less.
>
> 5. The value is how much of a percent the two people are in love.
>
> Result: 66

```python
person1 = "romeo montague"
person2 = "juliet capulet"

words = person1.lower() + person2.lower()

initial_numbers = [
    words.count("l"),
    words.count("o"),
    words.count("v"),
    words.count("e"),
    words.count("s"),
]

run = 1
current = initial_numbers

while True:
    print("run:", run, "len:", len(current))

    new = []

    for i, v in enumerate(current):
        if i == 0:
            continue
        val = current[i-1] + v
        if val >= 10:
            val_str = str(val)
            new.append(int(val_str[0]))
            new.append(int(val_str[1]))
        else:
            new.append(val)

    current = new[:]

    if len(current) <= 3:
        res = int("".join([str(x) for x in current]))
        if res <= 100:
            print("result:", res)
            break

    if len(current) > 1000:
        print("result: your love is endless and will last forever")
        break

    run += 1
```

