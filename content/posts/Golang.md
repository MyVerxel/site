---
title: "Golang"
date: 1400-07-04T23:31:53
draft: true
---

هر برنامه باید دارای یک پکیچ باشد :

```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}
```
