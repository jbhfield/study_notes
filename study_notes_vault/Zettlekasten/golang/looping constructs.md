---
aliases:
tags:
  - looping
  - for_loop
  - loop
references:
  - "[[golang]]"
date: 11-08-2025
time: 07:45
---
# looping constructs
In golang there is only one real looping construct, and that is the `for loop`.

## basic for loop
```go
package main
import "fmt"

func main(){
	sum := 0 
	for i := 0; i < 10; i++ { // note the ;
		sum += i // loop body
	}
}
```

## the init and post are optional
```go
package main
import "fmt"

func main(){
	sum := 1
	for ; sum < 100; { // note the empty init and no post operator
		sum += sum // double sum
	}
	fmt.Println(sum) // print sum at end
}
```

## "while loops" in go
```go
package main
import "fmt"

func main(){
	sum := 1
	for sum < 1000 { 
	// note for "expression" is just saying while sum < 1000
		sum += sum
	}
	fmt.Println(sum)
}
```

## infinite loop
```go
package main

func main(){
// notice there is no expression so it will just always evalute to true.
	for { 
		if somecondition {
		// be sure to remember evalute and break out on some condition
			break
		}
	}
}
```