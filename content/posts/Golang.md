---
title: "Golang"
date: 1400-07-04T23:31:53
draft: false
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

### Pointer:

- توسط `&` میتوانیم ادرس اشاگر را بدست بیاوریم
- توسط `*` به محل ان اشاگره اشاره میکتیم
- در تعریف اشارگرها باید در کنار نوع متغیر `*` قرار داد

```go
var u int
var j *int

j = &u
*j = 12

fmt.Println(  u ) // 12
fmt.Println( *j ) // 12

```

### struct:

- شامل مقادیر مختلفی از متغیر ها است 
- متغیر هایش میتوانند در همان لحظه اولیه مقدار دهی شودند و یا بعدا مقدرا دهی شودند
- چون متغیر های `go` دارای مقادیر پیش فرض هستند پس بعد از تعریف اولیه تمامی متغیرهایش دارای مقدار میباشند

```go

type Vertex struct {
	X int
	Y int
}

fmt.Println(Vertex{1, 2}) // {1 2}

v := Vertex{1, 2}
v.X = 4
fmt.Println(v) // {4 2}

s := []struct {
	i int
	b bool
}

```

### Pointers to structs

- در اشاگر های ساختار هنگام دسترسی به یک فیلد باید بنویسم `(*p).X` اما به علت دست و پا گیر بودن زبان به ما این اجازه را میدهد که بنویسم `p.X` 


```go
package main

import "fmt"

type Vertex struct {
	X int
	Y int
}

func main() {
	v := Vertex{1, 2}
	p := &v
	p.X = 1e9 // <= (*p).X
	fmt.Println(v)
}

```

- میشود در هنگام ساخت یک نمونه جدید توسط نام فیلد به آن مقدار داد

```go
package main

import "fmt"

type Vertex struct {
	X, Y int
}

var (
	v1 = Vertex{1, 2}  // has type Vertex
	v2 = Vertex{X: 1}  // Y:0 is implicit
	v3 = Vertex{}      // X:0 and Y:0
	p  = &Vertex{1, 2} // has type *Vertex
)

func main() {
	fmt.Println(v1, p, v2, v3)
}
//{1 2} &{1 2} {1 0} {0 0}
```

### Arrays:
- توسط عبارت `[]T` تعریف میشود
- تعداد خانه های آرایه جطیی از نوع ان محسوب میشود
- در نتیجه نیمشود در اینده تغییر داد
- راه حل جزایگزین استفاده از `make` هست که در آینده میرسیم بهش

بک آرایه اعداد صحیح با طول ۱۰ و انواع تعریف های دیگر:

```go
var a [10]int

var a [2]string
a[0] = "Hello"
a[1] = "World"

primes := [6]int{2, 3, 5, 7, 11, 13}

```

### Slices:
- ایره ها طول های ثابتی دارند
- برای ایجاد ارایه های با طورهای متغیراز `slice` استفاده میکنیم
- کاربرد `slice` ها از ارایه ها بیشتر است

```go
package main

import "fmt"

func main() {
	primes := [6]int{2, 3, 5, 7, 11, 13}

	var s []int = primes[1:4]
	fmt.Println(s)
}
```
- میتوانیم توسظ درستور زیر یک بخشی از یک آرایه را جدا کنیم و در `slice`بریزیم
- از و از خود **low** شروع و تا و نه خود **high** را شامل میشود

```go
a[low : high]
```

## مهم
- تغییر بخشی از آرایه اسلایس شده در آرایه اصلی هم تاثیر گذار است
- اسلایس ها هیچ داده رو ذخیره نمیکنند وفقط به عنوان یک زیر لابه و یا یک ارجاع به ارایه ها استفاده میشود

```go
primes := [6]int{2, 3, 5, 7, 11, 13}

var s []int = primes[1:4]
s[1] = 120 // change prime
```

### Slice literals

میتوانند همانند آرایه های بدون ذکر طول استفاده شوند

```go
package main

import "fmt"

func main() {
	q := []int{2, 3, 5, 7, 11, 13}
	fmt.Println(q)

	r := []bool{true, false, true, true, false, true}
	fmt.Println(r)

	s := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}
	fmt.Println(s)
}

```

این نوع استفاده از اسلایس مجاز است:

```go
a[0:10]
a[:10]
a[0:]
a[:]
```

### Slice length and capacity [^2]

[^2]: https://tour.golang.org/moretypes/11

> The length of a slice is the number of elements it contains.

> طول یک برش تعداد عناصر موجود در آن است.

> The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice. 

> ظرفیت یک برش تعداد عناصر موجود در آرایه زیرین است که از اولین عنصر در برش شمارش می شود.


- `len` تعداد المنت ها
- `cap` میشود تعداد المنت هایی که در زیر لایه ارایه موجود است. شمارش از اولین عنصر شروع میشود


 اسلایس زیر دارای مقدار ‍`nil` میباشد
  گخ به این معنا میباشد که هم `len`  و هم  `cap` ان صفر هستند
```go
var s []int
```


منبع [^1]

[^1]: https://www.w3-farsi.com/posts/62895/slice-in-golang/

در خط 6 کد بالا، ما یک آرایه به طول 11 کاراکتر ایجاد کرده ایم. یعنی تعداد عناصر آرایه 11 می باشد. در خط 8 یک برش یا Slice از این آرایه ایجاد کرده ایم. [4:7] در خط 11 بدین معنی است که از عنصری که دارای اندیس 6 تا عنصری که دارای اندیس 7 است را برش بزن. یعنی کاراکتر های t و h را جدا کن و در داخل یک Slice به نام sliceOfCharacter قرار بده. حال در خطوط 14-10 با استفاده از دو متد ()len و ()cap طول و ظرفیت آرایه و Slice را به دست آورده ایم. طول و ظرفیت آرایه به هم برابرند. یعنی تعداد عناصر آرایه مشخص کننده طول و ظرفیت آرایه است. اما در Slice وضع بدین منوال نیست. طول Slice تعداد عناصر Slice، که در مثال بالا 2 عنصر هستند، ولی ظرفیت Slice از جاییکه برش آرایه شروع شده است تا پایان آرایه می باشد یعنی 5. برای درک بهتر به شکل زیر توجه کنید:

```go
 package main

 import "fmt"


 func main() {

     var arrayOfCharacter = [11] string { "s","l","i","c","e"," ","t","h","i","s","!" }

 

     sliceOfCharacter := arrayOfCharacter[6:8]

 

     fmt.Println("Capacity of array :", cap(arrayOfCharacter))

     fmt.Println("Lenght   of array :", cap(arrayOfCharacter))

     fmt.Println()

     fmt.Println("Capacity of slice :", cap(sliceOfCharacter))

     fmt.Println("Lenght   of slice :", len(sliceOfCharacter))

 }
 ```

 ![slice in go](/image/slice-in-golang-01.png)

### Creating a slice with make
توسط تابع `make` هم میشود اسلایس ایحاد کرد

```go
b := make([]int, 0, 5) // len(b)=0, cap(b)=5
```

### slices of slice

```go
board := [][]string{
	[]string{"_", "_", "_"},
	[]string{"_", "_", "_"},
	[]string{"_", "_", "_"},
}

// The players take turns.
board[0][0] = "X"
board[2][2] = "O"
board[1][2] = "X"
board[1][0] = "O"
board[0][2] = "X"
```

### Appending to a slice

```go
var s []int
s = append(s, 0)

```

### Range
- کار همان `foreach` را میکند
- در مورد اسلایس ها دو مقدار ایندکس و مقدار را برمیگرداند

```go
package main

import "fmt"

var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

func main() {
	for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
}
```

اگر احتیاج به مقداری نداریم میتوانیم از `_` استفاده کنمی

```go
pow := make([]int, 10)

for i, _ := range pow
for _, value := range pow
for i := range pow
```

### Maps

- همان دیکشنری در پایتون
- دارای مقدار و کلید 

- بعد از ایجاد توسط `var` مپ دارای مقدار `nil` میباشد
- اگر تلاش کنیم وقتی که مقدار `nil` دارد از آن استافده کنیم؛ دچار خطای `panic` میشویم
- در نتیجه باید برای مقدار دهی اولیه از `make` استافده کرد

> Map types are reference types, like pointers or slices, and so the value of m above is nil; it doesn’t point to an initialized map. A nil map behaves like an empty map when reading, but attempts to write to a nil map will cause a runtime panic; don’t do that. To initialize a map, use the built in make function

```go

map[ KEY_TYPE ] VALUE_TYPE


/// ERROR

var m map[string]Vertex
//m = make(map[string]Vertex)
m["Bell Labs"] = Vertex{
	40.68433, -74.39967,
}

/// CORRECT

var m map[string]Vertex
m = make(map[string]Vertex)
m["Bell Labs"] = Vertex{
	40.68433, -74.39967,
}

/// CORRECT (without use var)

m := make(map[string]Vertex)
m["Bell Labs"] = Vertex{
	40.68433, -74.39967,
}

```

### Map literals

ترکیب انواع مختلف داده ای

```go
package main

import "fmt"

type Vertex struct {
	Lat, Long float64
}

var m = map[string]Vertex{
	"Bell Labs": Vertex{
		40.68433, -74.39967,
	},
	"Google": Vertex{
		37.42202, -122.08408,
	},
}

/*
If the top-level type is just a type name, you can omit it from the elements of the literal. 

var m = map[string]Vertex{
	"Bell Labs": {40.68433, -74.39967},
	"Google":    {37.42202, -122.08408},
}
*/

func main() {
	fmt.Println(m)
}

```

- هر عضو `map` دو مقدرا برمیگرداند؛ اولی مقدار و دیگیری وضعیت
- اگر `key` موجود بود که `elem` مثدار و در `ok` مثدار صحیح قرار میگیرد
- در غیر این صورت مقدار `ok` برابر با `false` میشود

```go
elem, ok = m[key]
```

مثال:

```go

delete(m, "Answer")
fmt.Println("The value:", m["Answer"])

v, ok := m["Answer"]
fmt.Println("The value:", v, "Present?", ok)

/*
The value: 0
The value: 0 Present? false
*/

```

### Function values

```go
 package main

import (
	"fmt"
	"math"
)

func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

func main() {
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))

	fmt.Println(compute(hypot))
	fmt.Println(compute(math.Pow))
}

//--------------

package main

import "fmt"

func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}

func main() {
	pos, neg := adder(), adder()
	for i := 0; i < 10; i++ {
		fmt.Println(
			pos(i),
			neg(-2*i),
		)
	}
}
```


