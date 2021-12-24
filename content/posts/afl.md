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
 
 
 # backTest
 
 بک تست یعنی بررسی گذشته بازار، چه دستی و چه با فرمول،، در اینجا بک تست به معنی نوشتن فرمول هست که نرم افزار توسط اون خرید و فروش رو انجام میده
 و از سود و ضرر هایی که کردیم گزارش تعیه میکنه
 
 توسط متغیرهایی که داره میتونم تعیین کنیم چه پوزیشنی رو میخواییم انتخاب کنیم
 
 ```python
 Buy
 Sell

 Short
 Cover
 
buy - "true" or 1 value opens long trade
sell - "true" or 1 value closes long trade
short - "true" or 1 value opens short trade
cover - "true" or 1 value closes short trade
 ```

از دوتای اولی برای خرید و فروش اسپات اسفتاده میشه

و از دوتای بعدی برای پوزیشین شورت یا فروش یا فیوچر فرم طور

```python
buyprice
sellprice
shortprice
coverprice
```

و چهار متغیر یا آرایه بالا هم برای تعیین قیمت خرید و فروش استفاده میشوند


# positionsize

```python
PositionSize = <size array>

Now you can control dollar amount or percentage of portfolio that is invested into the trade

    positive number define (dollar) amount that is invested into the trade for example:

    PositionSize = 1000; // invest $1000 in every trade

    negative numbers -100..-1 define percentage:
    -100 gives 100% of current portfolio size,
    -33 gives 33% of available equity for example:

    PositionSize = -50; /* always invest only half of the current equity */

    dynamic sizing example:

    PositionSize = - 100 + RSI();

    as RSI varies from 0..100 this will result in position depending on RSI values -> low values of RSI will result in higher percentage invested
```

تغیین میکنه چند درصد از موجودیم رو میخواییم سرمایه گذاری کنیم


---

![Stop Settings](/image/afl/w_settings3.gif)

## Trailing stops
This kind of stop is used to protect profits as it tracks your trade so each time a position value reaches a new high, the trailing stop is placed at a higher level. When the profit drops below the trailing stop level the position is closed. This mechanism is illustrated in the picture below (10% trailing stop is shown):

![Trailing stops](/image/afl/22trailstop.gif)

در تنظمات مقدار تریلینگ استاپ رو مشخص میکنه،

برای مثال در عکس به میزان 10 درصد از HH  قرار میگیره تا سودمون از دست نرده

# ApplyStop 
more: [^5]

از طریق این تابع میتوانیم تمامی stop هایی که در تصویر قبلی نشان داده شده و در تنظظیمات است را پیاده سازی کنیم

```python
 ApplyStop(
	type,
	mode,
	amount,
	exitatstop,
	volatile = False,
	ReEntryDelay = 0,
	ValidFrom = 0,
	ValidTo = -1 
) 



type =
0 = stopTypeLoss - maximum loss stop,
1 = stopTypeProfit - profit target stop,
2 = stopTypeTrailing - trailing stop,
3 = stopTypeNBar - N-bar stop 

mode =
0 - disable stop (stopModeDisable),
1 - amount in percent (stopModePercent), or number of bars for N-bar stop (stopModeBars),
2 - amount in points (stopModePoint);
3 - amount in percent of profit (risk)

amount =
percent/point loss/profit trigger/risk amount.
This could be a number (static stop level) or an array (dynamic stop level)

ExitAtStop

ExitAtStop = 0 - means check stops using only trade price and exit at regular trade price(1)
(if you are trading on close it means that only close price will be checked for exits and exit will be done at close price)
ExitAtStop = 1 - check High-Low prices and exit intraday on price equal to stop level on the same bar when stop was triggered
ExitAtStop = 2 - check High-Low prices but exit NEXT BAR on regular trade price.


```

# Ref
```python
Ref( Close, -1)
```

آرایه را یک واحد شیفت میدهد


# hhv , llv
```python
HHV(H,no);
LLV(L,no);
```

بیشترین مقدار و کمترین مقدار آرایه در یک دوره که تعیین میکنیم

یعنی همان max و یا min در یک دوره rolling شده هست




```python
dayofweek()
month()
```

 
 [^5]: https://www.amibroker.com/guide/afl/applystop.html
 [^4]: http://www.amibroker.com/guide/afl/lastvalue.html
 [^1]: http://www.amibroker.com/kb/2014/09/29/debugging-techniques-part-1-exploration/
 [^2]: https://www.amibroker.com/guide/afl/addcolumn.html
 [^3]: http://www.amibroker.com/guide/afl/barindex.html
 