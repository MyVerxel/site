---
title: "java"
date: 1400-09-25T12:45:43
draft: false
---

# شروع:

```java
//filename Gg.java
public class Gg{
  public static void main ( String[] args ) {
    ...
  }
}
```
# خواندن از ورودی

```java
import java.util.Scanner; // program uses class Scanner
Scanner input new Scanner(System.in);
number1= input.nextInt ();
```
# نوشتن در خروجی

```java
System.out.print()
System.out.println()
System.out.printf( format , ...)
```

# تعریف متغیر


```java
int number1;
```
اینها نوع اصلی هستند که باید به حروف کوچک نوشته شوند

1. int
2. float
3. double
4. char
5. boolean
6. byte
7. short
8. long

# محاسبات
حرف ٪ به معنی باقیمانده است


# کلاس

```java
public class G {
  public static void method (){
    ///code
  }
}
public class caller {
 public static void main (String[] args){
   G gc = new G();
  gc.method();
 }
}
```
# سازنده ها

```java
public class G {
  private String ss;
  public G (String str){
    ss =str;
  }
}

//
G h = new G("text");
....
```

# دستورات شرطی

```java
if ( condition )
{

}

else if ( .. )
{
}

else ( ... )
{
}

cond > 6 ? 7 : 8 ;


a > b
a >= b
a <= b
a == b
```

اگر از if و else های تو در توی بدون آکولاد استفاده کنیم، دچار مشکل else سرگردان میشویم، برای مثال

```java
if (1)
  if (2)
    aaa
  else
   bbbb
```
در شرایط بالا else متعلق به if اولی خواهد شد! برای حل مشکل باید از اکولاد استفاده کنیم. 
