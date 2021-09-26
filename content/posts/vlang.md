---
title: "Vlang"
date: 1400-07-03T02:31:16
draft: false
---

# نصب :

```python
git clone https://github.com/vlang/v
cd v
make
```

### ساختار برنامه : 

```python
fn main() {
	println('hello world')
}
```

### comment:

```python
// ...
/*
	.....
*/
```


### functions [^1] :

[^1]: https://github.com/vlang/v/blob/master/doc/docs.md#functions

نوع متغیر بعد از اسم آن میآید


```python
fn NAME ( var TYPE ) TYPE {

}
```

توابع میتوانند اول فراخونی شوند و در ادامه تعریف شوند ...

```python
fn main() {
	println(add(77, 33))
	println(sub(100, 50))
}

fn add(x int, y int) int {
	return x + y
}

fn sub(x int, y int) int {
	return x - y
}
```
برگشت چند متغیری:

```python
fn foo() (int, int) {
	return 2, 3
}

a, b := foo()
println(a) // 2
println(b) // 3
c, _ := foo() // ignore values using `_`
```

نمامی توابع خصوصی هستند مگر اینکه اعلام شوند [^2]
[^2]: https://github.com/vlang/v/blob/master/doc/docs.md#symbol-visibility

> Functions are private (not exported) by default. To allow other modules to use them, prepend pub. The same applies to constants and types.

```python
pub fn public_function() {
}

fn private_function() {
}
```

### متغیر ها :

- متغیر ها اول باید اعلان شوند و سپس استفاده شوند
- تمامی متغیر ها از نوع تغییر ناپذیر یا immutable هستند
- و برا اینکه تبدیل به متغیر های تغییر پدری شودند باید از کلمه کلیدی **mut** در اول نام آنها استفاده کرد
- بر خلاف سایر زبانها در v متغیر ها فقط میتوانند درون توابع تعریف شوند و چیزی به نام متغیر سراسری نداریم

##### نحوه اعلان :

```python
name := 'Bob'
age := 20
large_number := i64(9999999999)
```

> The variable's type is inferred from the value on the right hand side. To choose a different type, use type conversion: the expression `T(v)` converts the value `v` to the type `T`.

نحوه اعلان متغیر تغییر پذیر:
 توسط کلمه `mut`

```python
mut age := 20
println(age)
age = 21
println(age)
```
جابجایی متغیر ها در یک خط بدون تعریف متغیر دیگر:

```python
mut a := 0
mut b := 1
println('$a, $b') // 0, 1
a, b = b, a
```

- اگر متغیری اعلان شود ولی استفاده نشود؛ در هنگاک اجرای برنامه *هشدار* دریافت میکنیم؛ اگر میخوواهیم این هشدار تبدبل به خطا شود و برنامه اجرا نشود از ارگومان `-prod` در هنگام کامپایل استفاده مکنیم
- این حرکت مشابه `go` است

### Types [^3]
[^3]: https://github.com/vlang/v/blob/master/doc/docs.md#v-types

```python
bool

string

i8    i16  int  i64      i128 (soon)
byte  u16  u32  u64      u128 (soon)

rune // represents a Unicode code point

f32 f64

isize, usize // platform-dependent, the size is how many bytes it takes to reference any location in memory

voidptr // this one is mostly used for C interoperability

any // similar to C's void* and Go's interface{}
```

### string:

```python
name := 'Bob'
println(name.len)
println(name[0]) // indexing gives a byte B
println(name[1..3]) // slicing gives a string 'ob'
windows_newline := '\r\n' // escape special characters like in C
assert windows_newline.len == 2

//-----

country := 'Netherlands'
println(country[0]) // Output: 78
println(country[0].ascii_str()) // Output: N

```

- رشته ها هم تغییر پذیر نیستند در نتیجه دستور `name[0] = 'C'` هم نامعتبر است
- رشته ترکیبی از بلیت ها هست همانند `go`
- اما کاراکتر ها از نوع `rune` هستند

کاراکتر ها:

```python
rocket := `h`
assert 'aloha!'[0] == `a`
```

متن های خام:

```python
s := r'hello\nworld'
println(s) // "hello\nworld"
```

تبدیل رشته به عدد:

```python
s := '42'
n := s.int() // 42
```


تبدیل رشته ها به `runes` :

```python
hello := 'Hello World 👋'
hello_runes := hello.runes() // [`H`, `e`, `l`, `l`, `o`, ` `, `W`, `o`, `r`, `l`, `d`, ` `, `👋`]
```

درونیابی رشته ها :
```python
name := 'Bob'
println('Hello, $name!') // Hello, Bob!
```
> It also works with fields: 'age = $user.age'. If you need more complex expressions, use ${}: 'can register = ${user.age > 13}'.


الحاق [^4] :
[^4]: https://github.com/vlang/v/blob/master/doc/docs.md#string-operators

```python
name := 'Bob'
bobby := name + 'by' // + is used to concatenate strings
println(bobby) // "Bobby"
mut s := 'hello '
s += 'world' // `+=` is used to append to a string
println(s) // "hello world"

//

age := 10
println('age = ' + age) // not allowed


age := 11
println('age = ' + age.str())
```


### integers:

```python
a := 0x7B
b := 0b01111011
c := 0o173

num := 1_000_000 // same as 1000000
three := 0b0_11 // same as 0b11
float_num := 3_122.55 // same as 3122.55
hexa := 0xF_F // same as 255
oct := 0o17_3 // same as 0o173

a := i64(123)
b := byte(42)
c := i16(12345)

f := 1.0
f1 := f64(3.14)
f2 := f32(3.14)

f0 := 42e1 // 420
f1 := 123e-2 // 1.23
f2 := 456e+2 // 45600
```