---
title: "android"
date: 1400-10-04T00:00:27
draft: false
---

# SEARCH 

 - GRIDE LAYOUT (FILE J)
 
 

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
... findViewById( R.id.textView );
//...............
@string/textText
//...............
@drawble/icon123 //<- file icon123.png tuye res/drawble hast
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

برای فرستادم مقادیر از یک اکتیویتی به یک اکتیویتی دیگر باید مقادر را putExtra کنیم

و برای دیفات در یک اکتیویتی باید آنرا get کنیم


[این دو فایل دیده شود](https://github.com/pipitsong/androidPRJ/tree/15a795b6d7c16c82cf0852aa355ea5e6ae2577fa/app/src/main/java/com/example/myapplication)

همچنین برای چک کردن اینکه کلید همراه intent ارسال شده و وجود داره یا نه:

```java
Bundle extras = getIntent().getExtras()
if( extras.containsKey("test") )
{
	extras.getString("phone");
}
```


# lifeCircle

چرخه اکتیوتی ها یک چرخه زندگی هست که نحوه اجرا شدن اکتیویتی و متد ها را به ترتیب نشون میده

![life Circle](/image/android/lifeCircle.PNG)


# menu (file E)

دو نوع منو داریم یکی آپشن و یکی هم متریال؟! 

برای ایجاد آپشن روی res کلیک راست میکنیم و ادد ریسوزس میزنیم و منو رو انتخاب میکنیم

با اینکار یک افایل xml به ریسورس اضافه میشه که شامل منو هست و میتونیم منو و ساب منو و گروه اضافه کنیم


بعد از ایجاد منو ها، در فایل جاوا برای اینکه این فایل منو رو به اکتیویتی اتچ کنیم، باید در تابع زیر برنامه بنویسیم

```java
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        
        return super.onCreateOptionsMenu(menu);
    }
```

این تابع در هنگتم لود اکتیویتی فراخوانی میشه که باید در اون بگیم منو میخواییم 

برای اینکار از دستور زیر استفاده میکنیم :

```java
getMenuInflater().inflate(R.menu.menu_main,menu);
```

که یه رفرنس به فایل ریسوسر منو و اسم منو میدیم که باعث میشه اون رو توی اکتیویتیمون لود کنه


هر وقت هرکد.م از آیتم ها لکلیک بشن تابع زیر به صدا در میاد

```java
onOptionsItemSelected
```

توی این تابع باید آیدی هر Itam که اومده رو بگیریم، و به این متوجه میشیم روی کدوم Item کلیک شده

```java    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        if( item.getItemId() == R.id.alakiToast ){
            Toast.makeText(this, "alaki!", Toast.LENGTH_LONG).show();
        }else
        {
            Toast.makeText(this, "vaghei!", Toast.LENGTH_LONG).show();
        }
        return super.onOptionsItemSelected(item);
    }
```

برای ادد کردم منو به شکل برنام نویسی :

```java
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        menu.add("item1");
		SubMent item2 = menu.addSubmenu("item2");
		item2.add("sub item2");
        return super.onCreateOptionsMenu(menu);
    }
```


# editText

[code](https://github.com/pipitsong/androidPRJ/blob/e7c1bf24de9a9ddc85913dcc85d8dd2a9d81e954/app/src/main/java/com/example/myapplication/MainActivity.java)

```java
		//global
		EditText et ;
		//main
        et = findViewById(R.id.etTest);
        et.setOnFocusChangeListener(this);
        TextWatcher textWatcher = new TextWatcher() {
            @Override
            public void beforeTextChanged(CharSequence charSequence, int i, int i1, int i2) {

            }

            @Override
            public void onTextChanged(CharSequence charSequence, int i, int i1, int i2) {
                tv.setText(  charSequence );
            }

            @Override
            public void afterTextChanged(Editable editable) {

            }
        };
        et.addTextChangedListener(textWatcher);
		
		
		
	@Override
    public void onFocusChange(View view, boolean b) {
        String s = "Hii";
        if (view.getId() == R.id.etTest){
            s = "Byyy";
        }
        if (b) s="sick";
        Toast.makeText(this, s  , Toast.LENGTH_SHORT).show();
    }
```

دریافت متن و ست کردن متن

```java
 String s = et.getText().toString();
 et.setText(TEXT);
```


# xml (layout)

بعد ازاینکه لایه ها رو ساختیم برای اکتیویتی میتوانیم یک لایه را در یک لایه دیگه Include کنیم

برای اینکار در فیال xml از دستور include استفاده میکنیم

```java
<include layout="@layout/NAME_FILE_XML" 
	android:id="@+id/id_layout"/>
```


# handle activiti with class
[See](https://github.com/pipitsong/androidPRJ/tree/576b460f250ea309bfe4e0adb64e1ce0d47aa029/app/src/main/java/com/example/myapplication)

# home

دکمه back در بالای اکتیویتی برای بازگشت به اکتیویتی قبلی 
و همچنین برنامه ننویسیبرا این دکمه

[line25](https://github.com/pipitsong/androidPRJ/blob/6d2670747402c01f700cac013fe51fcd58be5bf8/app/src/main/java/com/example/myapplication/MainActivity2.java#L25)

```java
getSupportActionBar().setDisplayHomeAsUpEnabled(true);
```

تابعی که بعد از کیلیک شدن به این دکمه فراخوانی مشود همان تابع onOptionsItemSelected هست
که برای اسیر ایتم ها منو هم فراخوانی میشد

[line 43](https://github.com/pipitsong/androidPRJ/blob/6d2670747402c01f700cac013fe51fcd58be5bf8/app/src/main/java/com/example/myapplication/MainActivity2.java#L43)

```java
if(item.getItemId() == android.R.id.home)
{
	finish();
}
```

