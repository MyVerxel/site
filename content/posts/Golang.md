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

* برای اعداد مقدار پیش فرض ۰ است
* برای نوع بولی false
* برای رشته ها؛ رشته خالی


### Basic types

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```
* موع ‍`int` در سیستم های ۳۲ بیتی ۳۲ بیت و درسیتم های ۶۴ بیتی ۶۴ بیت است

> The int, uint, and uintptr types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems.


### Type conversions

> The expression T(v) converts the value v to the type T. 

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// Or, put more simply:

i := 42
f := float64(i)
u := uint(f)
```

### CONST

- نمیتواند توسط `:=` اعلان شود

```go
const Pi = 3.14
```

### FOR:

```go
for i := 0; i < 10; i++ {
	sum += i
}

//---------

sum := 1
for ; sum < 1000; {
	sum += sum
}

//---------

//WHILE

sum := 1
for sum < 1000 {
	sum += sum
}

//--------

// Forever

for {
}	

```

### if / ELSE:
```go
if x < 0 {
	return sqrt(-x) + "i"
}

/// ELSE

if x {
	//
} else {
	//
}

```

- میشود ار خود if متغیر تعریف کرد و سپس چک کرد
- متغیر تعریف شده فقط در داخل if قابلیت دسترسی دارد

```go
if v := math.Pow(x, n); v < lim {
	return v
}
```

### Switch:

- ایحتیاج به `break` ندارد

> Switch cases evaluate cases from top to bottom, stopping when a case succeeds. 

```go
fmt.Print("Go runs on ")
switch os := runtime.GOOS; os {
case "darwin":
	fmt.Println("OS X.")
case "linux":
	fmt.Println("Linux.")
default:
	// freebsd, openbsd,
	// plan9, windows...
	fmt.Printf("%s.\n", os)
}
```

- اگر i برابر با 1 باید تابع f هیچوقت فراخوانی نمیشود
- چون به صورت پیش فرض `break` را پیاده سازی میکنید ..

```go
switch i {
case 0:
case f():
}

// does not call f if i==0.) 
```

### مهم:

> Note: Time in the Go playground always appears to start at 2009-11-10 23:00:00 UTC, a value whose significance is left as an exercise for the reade


### Defer:

- بعد از اینکه تابع return شد مقدرای که پای دادیم به این تابع اجرا میشود

- به صورت lifo هست؛ یعنی در استک پوش میشه و وقتی return شد به همون صورت از اخر به اول پاپ و اجرا میشه

```go
func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}

//−−−−−−−

for i := 0; i < 10; i++ {
	defer fmt.Println(i)
}
// ۹ ۸ ۷ ۶ ۵ ۴ ....
```

