---
title: "android"
date: 1400-10-04T00:00:27
draft: false
---

اکتیوی ها از کلاس AppCompatActivity ارث میبرند

```java
    TextView tv ;
    Button bt;
```

متغیر های tv و bt از نوه تکست و دکمه هستند، 

# setContentView 

نحتوای layout رو نشون میده که در فایل های xml هستند

# نحوه دسترسی به ریسورس ها

در جا وا از سریق کلاس R 

و در xml از طریق @ و میتونیم به ریسوسرس دسترسی پیدا کنیم

```java
setContentView(R.layout.activity_main);
//...............
@string/textText
```

در مورد اول در کد جاوا میگیم که از layout اکتوتی اصلی رو میخواییم

و در مورد دوم میگیم برو به فایل strings و امتن اونی که اسمش textText هست رو بیار واسمون


# id

برای ست کردن id به المنت از این طریق عمیل میکنیم

و بعدا برای اضافه کردن خاصیت جدید به این المنت از طریق همین id باید اقدام کنیم

```java
android:id="@+id/button"
```

# findViewById

وقتی میخواییم به خصوصیات به شی دسترسی داشته باشیم با ایتن تابع و از طریق ایدی که در مرحله قبل ست کردیم
میتوانیم یک instance از شی را برگدانیم


```java
package com.example.ali.myapplication2;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import org.w3c.dom.Text;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    TextView tv ;
    Button bt;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        bt = findViewById( R.id.button );
        bt.setOnClickListener( this );
        tv = findViewById( R.id.textView );
    }

    @Override
    public void onClick(View view) {
        tv.setText("dsdsdsd");
    }
}
```

# Intetnt

برای رفتن از یک اکتیویتی به یک اکتیویتی دیگر با ید از intetnt استفاده کنیم

اول یک کلاس نمونه به همراه پاس دادن یک ابجکت از اون رو میسازیم؛

و سپس استارت میکنیم

```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivityForResult(intent);
```

# lifeCircle

چرخه اکتیوتی ها یک چرخه زندگی هست که نحوه اجرا شدن اکتیویتی و متد ها را به ترتیب نشون میده

![life Circle](/image/android/lifeCircle.PNG)
