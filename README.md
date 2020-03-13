# Errors

Add stacktrace to your errors

## Usage

```go
package main

import (
	"fmt"
	"strconv"
    "github.com/pechenini/errors"
)
func main() {
	d()
}

func d() {
	_, err := atoi()
	if err != nil {
		fmt.Println(err)
	}
}

func atoi() (int, error) {
	i, err := strconv.Atoi("f42")
	if err != nil {
		return 0, errors.Wrap(err) // annotate errors with stacktrace
	}
	return i, nil
}
```

Output:

```
strconv.Atoi: parsing "f42": invalid syntax
        File: /foo/bar/main.go, Line: 22. Function: main.atoi
        File: /foo/bar/main.go, Line: 13. Function: main.d
        File: /foo/bar/main.go, Line: 9. Function: main.main
```
