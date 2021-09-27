---
title: "Golang"
date: 1400-07-04T23:31:53
draft: true
---

### package:
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

### Exported names :

- نامهای اکسپورت شده فقط با حروف بزرگ شروع میشوند
- در غیر اینصورت اکسپورت نخواهند شد

```go
`fmt.Println(math.pi)` // error
`fmt.Println(math.Pi)` // correct

```

### Functions:
برای تعریف آرایه باید حتما براکت باز شدن در همان خز اول باشد

```go
func NAME ( [ARGs] ) [TYPE[,...] ] { // <-mohem

}


// ERROR:
func NAME ( [ARGs] ) [TYPE[,...] ]
{

}

func add(x int, y int) int {
func add(x    , y int) int {
	return x + y
}
```

 بازگشت چند متغیری:

```go
 package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

میتوانیم برای مقادیری که میخواهیم برگردانیم اسم تعریف کنمی:
```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}

// OUTPUT:
// 7 10
```

### Variables:

- متغیر ها توسط کلیمه کلیدی `var` تعریف میشوند
- میتوانند در ابتدا دارای مقدار باشند
- اگر مقدار دهی اولیه نشوند خود زبان `go` به انها مقدار پیش فرض میدهد
- میتوان از عبارت `:=` برای ایجاد متغیر هم استفاده کرد
- اگر از `:=` استفاده کنیم به صورت خودکار با توجه به مقدار سمت راست نوع متغیر هم تعریف میشود
- در خارج از توابع حتما باید از `var` استفاده نماییم

```go
package main

import "fmt"

//−−−−−−−−−−

var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}

//−−−−−−−−−−

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}

//−−−−−−−−

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java)
}

//−−−−−−−



```