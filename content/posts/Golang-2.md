---
title: "Golang-2"
date: 1401-10-08T15:29:30
draft: false
---

### Methods

در زبان گو کلاس نداریم در نتیجه باید از تایپ ها استفاده کنیم

```go
type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
	v := Vertex{3, 4}
	fmt.Println(v.Abs())
}

```

در اینجا تابع abs به ساختار Vertex متصل شده است و اگر یک نمومه از vertex بسازیم میتوانیم به متدهای مختصی این ساختار دسترسی داشته باشیم


```go
package main

import "fmt"

type F struct {
  x int
  y string
}

func ( f F ) test (s string) string {
  return s
}

func main() {
  i := F{}
  fmt.Println(  i.test( "salam" ) )
}
```


### Methods are functions

> Remember: a method is just a function with a receiver argument.
> Here's Abs written as a regular function with no change in functionality. 

متد ها توابعی هستند که فقط آرگومان ویژه دارند در نتیجه مینواین به این شکل بنویسیم:

```go
package main

import (
	"fmt"
	"math"
)

type Vertex struct {
	X, Y float64
}

func Abs(v Vertex) float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
	v := Vertex{3, 4}
	fmt.Println(Abs(v))
}
```


به این معنی که نمیواتیم متغیر ها را در حالت عادی در توابع عوض کنیم؛ و حتما باید به ضورت اشاره گر تعریف شود

```go
package main

import "fmt"

type F struct {
  x int
}

func ( f F ) test() {
  f.x=11
}
func ( f *F ) ptest() {
  f.x=99
}

func main() {
  i := F{x:10}
  i.test()
  fmt.Println(i.x )
  i.ptest()
  fmt.Println(i.x )
}

// 10
// 99
```

ابتدا مقدار x برابر با ۱۰ شد و تایع صدا زده شد؛ در تابع مقدار x به صورت محلی به ۱۱ تغییر پیدا کرد؛ ولی با خروج از تابع مقدار ۱۰ در x مانده بود؛ سپس تابع دوم که اشاره گر ثبول میکرد صدا شده شد و مقدار x تغییر داده شد و در x کلی هم تغییر داده شد

[مثال](https://go.dev/tour/methods/4)

> With a value receiver, the Scale method operates on a copy of the original Vertex value. The  method must have a pointer receiver to change the Vertex value declared in the main function. 

### interface

اینترفیس یک type است که مشخص میکند struct باید دارای چه متدهایی باشد

نکته: هر strct ای که دارای این متد ها باشد میتوند عضوی از interface باشد

```go
type I interface {
  M()
}
```

کد بالا یک interface بنام I را تعریف میکند که باید تابع M در آن تعریف شده باشد

در ساختاری که تابع M داشته باشد میتواند بعنوان I نیز تعریف شود

```go
package main

import "fmt"

type I interface {
  M()
}

type T struct {
  S string
}

func (t T) M() {
  fmt.Println(t.S)
}

func main() {
  var i I = T{"hello"}
  i.M()
}
```
[منبع](https://go.dev/tour/methods/10)

در کد بالا متغیر i از نوع interface به نام I تعریف شده؛ اما ساختار T به آن اختصاص داده شده است؛ چون ساختار T‌ دارای متد M است؛ در نتیجه این پیاده سازی صحیح است و میتوان تابع M‌ را فراخونی کرد


[ex1](https://gobyexample.com/interfaces) - 
[ex2](https://golangbyexample.com/interface-in-golang/) - 

```go
package main

import "fmt"

type i interface {
  p1()
  p2()
}

type S struct {}
type Z struct {}

func (s S) p1 () {
  fmt.Println("s1" )
}

func (s S) p2 () {
  fmt.Println("s2" )
}



func (s Z) p1 () {
  fmt.Println("z1" )
}

func (s Z) p2 () {
  fmt.Println("z2" )
}

func (s Z) p3 () {
  fmt.Println("z3" )
}

func main() {
  var s i = S{}
  var z i = Z{}
  s.p1()
  z.p2()
}

```

در مثال بالا ساختار Z سه متد p1 p2 p3 را پیاده ازی کرده است؛ اما همچنان میتواند عضوی از اینترفیس i باشد؛ زیرا در این اینترفیس پیاده سازی  فقط دو متد p1 p2 اهمیت دارد و هر ساختاری که این دو متذ را پیاده کند میتواند از نوع اینترفیس i باشید؛

اما متغیر z دیگر به p3 دسترسین ندارد و نمیتواند آن را فراخوانی کند؛ برای دسترسی به p3 بدون اینترفیس باید بنویسیم:

```go
var z Z = Z{}
z.p3()
```

### Interface values

اینترفیس ها مقدار و تایپ خودشون رو در زیر لایه هایی که میشه بهش دسترسی داشت نگه داری میکنند

[در یک همچنین فرمتی](https://go.dev/tour/methods/11)
```go
(value, type)
```
مثال

```go
type I interface {
  M()
}
type T struct {
  S string
}
func (t *T) M() {
  fmt.Println(t.S)
}
func main() {
  var i I

  i = &T{"Hello"}
  describe(i)
  i.M()

}

func describe(i I) {
  fmt.Printf("(%v, %T)\n", i, i)
}

//(&{Hello}, *main.T)
//Hello
```

### empty interface

لینترفیس های خالی زیر مجموعه هر تایپی هستند

(منبع)[https://go.dev/tour/methods/14]

```go
package main

import "fmt"

func main() {
  var i interface{}
  describe(i)

  i = 42
  describe(i)

  i = "hello"
  describe(i)
}

func describe(i interface{}) {
  fmt.Printf("(%v, %T)\n", i, i)
}

//(<nil>, <nil>)
//(42, int)
//(hello, string)
```

