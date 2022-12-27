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

[مثال])(https://go.dev/tour/methods/4)

> With a value receiver, the Scale method operates on a copy of the original Vertex value. The  method must have a pointer receiver to change the Vertex value declared in the main function. 

