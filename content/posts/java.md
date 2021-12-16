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
 public method void main (String[] args){
   G gc = new G();
  gc.method();
 }
}
```
