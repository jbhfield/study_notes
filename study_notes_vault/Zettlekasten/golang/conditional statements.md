---
aliases:
tags:
date: "11-08-2025"
time: "08:14"
references:
---
# conditionals in go
## if statement
```go
package main
import (
	"fmt"
	"math"
)
func main(){
// there are no () parenthesis, but braces are always required
	if x < 0 {
		// do something
	}
}
```

## starting an if with a statement
> [!WARNING] statement scope
> The scope of variables define in a statement at the beginning, are only in scope until the end of the if.
> 
> OR in the event there is also an "else" the variable in the statement at the beginning of the if is also in scope inside the else block attached to the if statement.
```go
package main
import (
	"fmt"
	"math"
)

func pow(x, n, lim float64){
	// note the v:= math.Pow(x, n);
	// before the if evaluation of v < lim
	if v:= math.Pow(x, n); v < lim {
		return v
	}
	return lim // default to return the limit if v > lim
}

func main(){
	fmt.Println(
		pow(3, 2, 10)
		pow(3, 2, 20)
	)
}
```

## switch statements
```go
package main
import (
	"fmt"
	"runtime"
)

func main(){
	fmt.Println("Go runs on ")
	/*
	notice how succint the switch is (similar to if) using a evaluation statement prior to the switch itself 
		no need for os := runtime.GOOS and then switch os {..}
	*/
	switch os := runtime.GOOS; os{
		case "darwin":
			fmt.Println("macOS.")
		case "linux":
			fmt.Println("Linux")
		default:
			//executes in the event the prior cases did not match
			// freebsd, openbsd,
			// plan9, windows...
			fmt.Printf("%s.\n", os)
	}
}
```

### evaluating function return in switch case statement
In go you can use the value returned from a function, to match a case statement in a switch.
```go
package main
import (
    "fmt"
)

func mytest_func() int {
    return 4 // Will return 4
}

func main() {
    i := 4
    switch i {
    case 1:
        fmt.Println("one")
    case 2:
        fmt.Println("two")
    case 3:
        fmt.Println("three")
    case mytest_func(): // will evaluate to 4 and trigger "four"
        fmt.Println("four")
    default:
        fmt.Println("default")
    }
}
```

### switch with no condition
You can do a switch with no condition; instead evaluating some other statement in the cases. For instance, see the t time below.
```go
package main

import (
	"fmt"
)

func main(){
	t := time.Now()
	switch { // <- this is the same as switch true {...}
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour () < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}
}
```