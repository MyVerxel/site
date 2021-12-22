---
title: "Afl"
date: 1400-09-30T10:30:27
draft: false
---

1. تمامی عبارت ها به سمی‌کالن بسته می‌شود
2. از نقطه برای دسترسی به ابجکت مورد نظر استفاده میشود

##  به بزرگی کوچکی حروف حساسیت نیستند
امکان اینها ارایه هستند
```python
o open
c close
h high
l low
v volume
```

#  آرایه ها
از طریق براکت می‌توان مقداری را ست کرد ویا صدا زد

```python
a[0] = 33 //set

a[0] //get
```
## مثال

```python
MA( Close, 10 );
 IIf( H > Ref(H,-1), MA(H,20), MA(C,20) );
```

```python
relational ( <, >, <=, >= )
equality ( ==, != )

 bit-wise
| 
&
 
 
Logical operators:
NOT
AND
OR
```
عبارت زیر ولید است

```python
i = j = k = 0
```

# محاسبات
```python
+
-
/
*
%
^
+=
-=
/=
*=
%=
^=
&=
|=
```
 ساختار


```python
if ( CONDITION )
{

}

for( i = 0; i < 10; i++ )
{
}
```


----


```python
typeof() operator

The typeof operator is used in the following way:
typeof (operand)
The typeof operator returns a string indicating the type of the *unevaluated* operand.

Possible return values are:

"undefined" - identifier is not defined

"number" - operand represents a number (scalar)

"array" - operand represents an array

"string" - operand represents a string

"function" - operand is a built-in function identifier

"user function" - operand is a user-defined function

"object" - operand represents COM object

"member" - operand represents member function or property of COM object

"handle" - operand represents Windows handle

"unknown" - type of operand is unknown (should not happen)typeof operator allows among other things to detect undefined variables in the following way
```


----


```python
The unary operators (++ and --) are called “prefix” increment or decrement operators
++
--
[] array element operator
```

----

###   ثابت BarCount تعداد نهایی کندلهایی که در دسترس داریم را بر میگرداند


```python
BarCount constant gives the number of bars in array (such as Close, High, Low, Open, Volume, etc). Array elements are numbered from 0 (zero) to BarCount-1. BarCount does NOT change as long as your formula continues execution, but it may change between executions when new bars are added, zoom factor is changed or symbol is changed.
```


# matrix
یه ارایه دو بعدی است


```python
my_var_name = Matrix( rows, cols, initvalue);

To access matrix elements, use:
my_var_name[ row ][ col ];

where
row is a row index (0... number of rows-1)
and
col is a column index (0... number of columns-1)
```

# توابع

```python
sqrt()
rsi( period )
macd()
ema( data , period )

```
تابع iif یک تابع شرطی است که بر روی ارایه کار می‌کند


```python
dynamicrsi = IIf( Close > MA(C,10), RSI(9), RSI(14) );
```

همچنین بدون iif من می‌توانیم شروط را پیاده سازی کنیم
یک ارایه بر میگرداند که اگر شرط درست بود،مقدار یک در غیر اینصورت مقدار صفر

```python
result = RSI(14) > 70;
```

# ValueWhen

تکنیک های دیباگ [^1]

کد زیر را ذخیره کرده و از قسمت انالایز سپس explorer کرده

```python
Filter = 1; // show all bars
//
m = MA( C, 10 );
cond = Cross( C, m );
bi = BarIndex();
//
AddColumn( C, "Close" );
AddColumn( m, "Mov Avg" );
AddColumn( cond, "Condition");
AddColumn( bi, "BarIndex" );
AddColumn( ValueWhen( cond, bi ), "ValueWhen( cond, BarIndex() )" );
AddColumn( ValueWhen( cond, Close), "ValueWhen( cond, Close )" )
```

 ![slice in go](/image/afl/valuewhen-1.gif)
 
 این تابع در صروتی که شرط بقرار باشد مقدار آرایه را برمیگرداند و آنرا حفظ میکند
 
```python
/*
If you run above code you will clearly see how ValueWhen picks 
the value when condition is true and “holds” 
it for all other bars (when condition is false).
*/

 ValueWhen(EXPRESSION, ARRAY, n = 1) 

```
 
 مقدار EXPRESSION یک ارایه با مقادیر صحیح یا غلط هستن
 در جایی که EXPRESSION صحیح باشد، مقدار متناظر آن در array برگردانده میشود 
 و تا مقدار بعدی که EXPRESSION صحیح باشد آن مقدار نگه داری میشود
 
 
 
 # AddColumn
 ```python
  AddColumn( array, name,
		format = 1.2, textColor = colorDefault,
		bkgndColor = colorDefault, width = -1,
		barchart = Null ) 
 ```
 
 یک ستون به قسمت انالایزر اضافه میکند که میتوانیم دیتاهای خود را در ان ببینیم [^2]
 
برای اینکه دیتاها روی تمامی کندل ها نمایش داده شود باید مقدار filter را در ابتدا یک کنیم [^1]

```python
Filter = 1; // show all bars
```
 
 # BarIndex
 شماره کندل را بر میگرداند [^3]
 
 # LastValue
 ```python
  LastValue(ARRAY, lastmode = True ) 
 ```
 اخرین مقدار آرایه بر میگرداند [^4]
 
 اگر اخرین مقداری وجود نداشته باشد صفر برمیگرداند
 
 آخرین مقدار محاسبه شده آرایه مشخص شده را برمی گرداند. نتیجه این تابع را می توان به جای ثابت (NUMBER) در هر آرگومان تابع استفاده کرد.
  
اگر آخرین نوار آرایه تعریف نشده یا تهی باشد (به عنوان مثال، فقط 100 روز بارگیری شده است و آخرین مقدار میانگین متحرک 200 روزه را درخواست می کنید)، تابع lastvalue صفر را برمی گرداند.
هشدار: از آنجایی که این تابع مقدار آخرین نوار آرایه را دریافت می کند، به فرمولی اجازه می دهد تا به آینده نگاه کند، اگر نوار فعلی آخرین مورد نباشد.
 
 
# trace
```python
_TRACE ("MSG")
```
یک پیام در سیستم لاگ ویندوز ثبت میکند

برای دیدم لاگ در خود امی بروکی از قیمت وسندوز لاگ را فعال کنید

سپس در صفحه لاگ راست کلیلک کنید و مدل هدنترنال لاگ را انتخاب کنید

 هر جا از این کد استفاده کنیم پیام مورد نظر ما در صفحه چاپ خواهد شد
 
 
 
 
 
 [^4]: http://www.amibroker.com/guide/afl/lastvalue.html
 [^1]: http://www.amibroker.com/kb/2014/09/29/debugging-techniques-part-1-exploration/
 [^2]: https://www.amibroker.com/guide/afl/addcolumn.html
 [^3]: http://www.amibroker.com/guide/afl/barindex.html
 