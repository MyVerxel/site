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


# iintent call activity with code

برای فراخوانی یک اکتیویتی بطوری که قابل شناسایی باشد، یعنی برای یک کاری صدا کنیم
و منتظر جواب بمانیم، باید یک کد به اکتیویتی ارسال کنیم

```java
--	//startActivity(intetnt);
++	startActivityForResult(intetnt,SUCCES_CODE);
```

ودر اکتیویتی ای که فراخوانی میشود باید توسط setResult یک مقادر return کنیم
و سپس اکتیوی را finish کنیم

[SEE](https://github.com/pipitsong/androidPRJ/commit/b03267c25a2b74e560dac6467b4d8f31a38cc05d)

```java
setResult(50);
finish();
```

و جوابی که  اکتیویتی فراخوانی شده بر میگردانه در تابع onActivityResult  جاری قابل دریافت است
[این تابع](https://github.com/pipitsong/androidPRJ/commit/b03267c25a2b74e560dac6467b4d8f31a38cc05d#diff-77f8c9ac65585f8b62bc934aafac99ec753920a06e879d0572ec739e93356fa5R61)

همچنین میتوانیم دیتا و سایر اجزا را به اکتیویتی ای که اکتویتی جاری را فراخوانی کرده است برگردانیم

[see](https://github.com/pipitsong/androidPRJ/commit/0e1588e989ccadc65519274821bb13366640627e)

```java
Intent intent = new Intent();
intent.putExtra("DATA","SALAM1");  
setResult(50,intent);
finish();
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

برای اینکه بتوانیم متدهای اجزای سازنده اکتیویتی را تحت کنترل در بیاوریم، باید از geter ها استفاده کنیم

[See](https://github.com/pipitsong/androidPRJ/commit/1d8f2f24997ca1b0b87cb7e6e5dae419fc2831f9)

به وسیله آن میتوانیم رفتار اجزا را تعیین و یا overide کنیم


# OPEN Intent (SMS,PHON) (FILE I)

```java
Intent intent = new Intent( Intent.ACTION_VIEW );
intent.SetData( Uri.parse("sms:+1234456") );
startActivity(intent);
```



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

# animation

[code](https://github.com/pipitsong/androidPRJ/blob/15dde593fda934ede116503d2b20afb42c864fcb/app/src/main/java/com/example/myapplication/MainActivity3.java)

برای اینکه آلفای یک تصویررا به صفر برسانیم و اینکار طی یک مدت زمانی انجام شود

نکته اینکه عدد 0f به معنی 0 در مبنای float هست
اگر 0.0 بزاریم double حساب میشود و خطا میدهد

```java
	iv.animate().alpha(0f).setDuration(2000);
```

حرکت افقی و عمودی
؛ در کد اول حرکت در y نسبی است و در کد دوم میره دقیقا به 50

```java
	iv.animate().translationYBy(50).setDuration(2000);
	//------
	iv.animate().translationY(50).setDuration(2000);
```

چرخش

```java
	iv.animate().rotation(90f).setDuration(2000);
	iv.animate().rotationBy(90f).setDuration(2000);
```

# تغییر عکس
```java
ImageView iv = findbyid(...)
iv.SetImageResource(R.drawable.axname);
```

# والد فرزند

```java
	LinearLayout L = findViewById(R.id.LID);
	L.getChildCount(); // <-- tedad farzand
	L.getChildAt( i ); // <--  farzand i'om
```

# video view

نشان دادن ویدو بدون گزینه های کنترلی

```java
	VideView vv = findById(R.id.videview);
	vv.setVideoPath( "android.resource://"  + getPackageName() + R.raw.videofilename );
	vv.start();
```

اضافه کردن دکمه های کنترلی

```java
	VideView vv = findById(R.id.videview);
	vv.setVideoPath( "android.resource://"  + getPackageName() + R.raw.videofilename );
	
	MediaController c = new MediController(this);
	
	c.setAmchorView(vv);
	vv.SetMediaController( c );	
	
	vv.start();
```

# audio

```java
	MediaPlayer mp = MediaPlayer.create( this, R.raw.audiofile );
	mp.start();
	mp.pause();
	mp.isPlayeing();
	mp.getDuration(); //<- modat zamane ahang 
```

خواندن volume دستگاه

اول یک ابجکت ایجاد میکنیم و سپس بهش میگیم که بمیخواهیم وصل بشیم به volume سیستم

```java
	AudioManager audioManager;
	audioManager = getSystemService(Context.AUDIO_SERVICE);
	int maxVolume = audioManager.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
	int curVolume = audioManager.getStreamVolume(AudioManager.STREAM_MUSIC);
	
	audioManager.setStreamVolume(AudioManager.STREAM_MUSIC, NUMBER , 0); // <-set deviice volume
	
```

در کد پایین از طریق fromUser میتونیم متوجه بشیم اندروید در حال دستکاری در سیک بار هست و یا یوزر داره باهاش بازی میکنه

اگر مقدار true بود یعنی یوزر داره کار میکنه باهاش

# seekBar
```java
	SeekBar sb  = findById(...);
	sb.setProgress(10);
	sb.setMax(100);
	
	sb.setOnSeekBarChangeListener(this);
	sb.setOnSeekBarChangeListener( new  SeekBar.OnSeekBarChangeListener(){
		@Override
		public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
			// change volume
			//progress <- adade seek bar
			
			// audioManager da r bala tashrih shode
			audioManager.setStreamVolume(AudioManager.STREAM_MUSIC, progress, 0); 
		}

		@Override
		public void onStartTrackingTouch(SeekBar seekBar) {}
		@Override
		public void onStopTrackingTouch(SeekBar seekBar) {}
	});
```

# DIALOG

## progress bar

میتوایم به کاربر دیالوگ ها رو نشان دهیم که کاربدهای مختلفی دارد

```java
ProgressDialog pd = new ProgressDialog(this);
```

قابلیت کنسل کردن توسط کاربر را غیر فعال میکنیم، 

```java
pdialog.setCancelable(false);
```

ست کردن متن و عنوان

```java
pdialog.setTitle("progress dialog example");
pdialog.setMessage("please wait ...");
```

ست کردن استایل

```java
pdialog.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
```

نمایش دادن دیالوگ

```java
pdialog.show();
```

بستن دیالوگ

```java
pdialog.dismiss();
```

هنگامی که استایل بصورت افقی ست شده باشد، گزینه های زیر در دسترس هستند:

که میتوانیم نوار پیمایش را کنترل کنیم

```java
pdialog.setProgress(0);
pdialog.getMax()
pdialog.incrementProgressBy(1)
```

نوار هیچ پیشرفتی نمیکند و حالت نا مشخص میگیرد

```java
pdialog.setIndeterminate(true);
```

همچنین یک حالت دیگری هم داریم که بنام پروگرس بار دوم 

که میشه یک progressbar زیر اونیکی؛ مثلا برای مواقعی که فیلم در حال دانلود هست و بافر در حال پر شدن هست ...

```java
pdialog.getSecondaryProgress();
pdialog.incrementSecondaryProgressBy(1);
```

## Alert

برای نشان دادن یک هشدار 

یک هشدار با دکمه های yes و no و cancel نشان میدهد که در صورتی که کاربر yes انتخاب کرد یک پیام نشان میدهد

```java
final AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setTitle("AlertDialog")
		.setMessage("MSG")
		.setCancelable(false)
		.setIcon(android.R.drawable.ic_dialog_info)
		.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
			@Override
			public void onClick(DialogInterface dialogInterface, int i) {
				Toast.makeText(DialogActivity.this, "File Deleted!", Toast.LENGTH_SHORT).show();
			}
		})
		.setNegativeButton("No", null)
		.setNeutralButton("Cancel", null);
```

چند گزینه ای که فقط میشه یک گزینه انتخاب کرد

```java
builder.setTitle("Question ?")
		.setCancelable(false)
		.setSingleChoiceItems(new String[]{"A", "B", "C", "D"}, -1, new DialogInterface.OnClickListener() {
			@Override
			public void onClick(DialogInterface dialogInterface, int i) {
				Toast.makeText(DialogActivity.this, "i = " + i, Toast.LENGTH_SHORT).show();
			}
		})
		.setPositiveButton("OK", null);
```

چند گزینه ای که میشه چندین گزینه انتخاب کرد

```java
builder.setTitle("")
		.setCancelable(true)
		.setMultiChoiceItems(new String[]{"item0", "item1", "item2", "item3", "item4", "item5"},
				new boolean[]{false, true, false, true, true, false},
				new DialogInterface.OnMultiChoiceClickListener() {
					@Override
					public void onClick(DialogInterface dialogInterface, int i, boolean b) {
						Toast.makeText(DialogActivity.this, "item" + i + " : " + b, Toast.LENGTH_SHORT).show();
					}
				})
		.setPositiveButton("Ok", null);



builder.show();
```

و دیالوگی که خودمون طراحی مکنیم و یک اکتیویتی دیگر را نشون میدیم
```java
Dialog dialog = new Dialog(this);
dialog.setContentView(R.layout.play_ground);
dialog.show();
```

# List view

[مثال](https://github.com/pipitsong/androidPRJ/blob/acb689b9b9e945a0fdcc596a2de404bcde7d2b25/app/src/main/java/com/example/myapplication/ListViewAvtivity.java#L22)

برای ساخت لیست یه 3 چیز نیازمندیم

 - لیست آیتم ها
 - لیست ویو اندروید 
 - و اداپتر
 
اول باید لیست را بسیازیم و سپس یک لیست ویو به اکتیویتی اضافه کنیم

در نهایت به وسیله اداپتر به اندروید بگوییم این لیست را به چه شکلی نمایش بده

```java
List<String> items;

items = new ArrayList<>();
items.add("Tehran");
items.add("Mashhad");
items.add("Isfahan");
items.add("Shiraz");

ListView listview;
listview = (ListView) findViewById(R.id.listview);


ArrayAdapter<String> adapter;
adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, items);

listview.setAdapter(adapter);
```

و همچنین میتوانیم برای کلیلک کردن روی هرکدام از آنها یک تابع تعریف کنیم...

```java
listview.setOnItemClickListener(new AdapterView.OnItemClickListener() {
	@Override
	public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
		Toast.makeText(SimpleListActivity.this, items.get(i), Toast.LENGTH_SHORT).show();
	}
});
```

برای اضافه کردن و حذف گزینه ها که بدن شکل میباید که عنصر مورد نظر را از ایتم ها حذف میکنیم و سپس اداپتر را به روز رسانی میکنیم تا ویو را دوباره بسازد

```java
items.add("new item");
adapter.notifyDataSetChanged();
//------------------------------------
items.remove(items.size()-1);
adapter.notifyDataSetChanged();
```

### استفاده از کلاس در لیست ویو

یک کلاس تعریف میکنیم تا اجزای کلاس را بر اساس ان تعریف کنیم

[کد کلاس](https://github.com/pipitsong/androidPRJ/blob/30eccd5bccfb833c04c83db545a6fd8c59ca7c12/app/src/main/java/com/example/myapplication/MyContacts.java)

```javapublic class MyContacts {
    private String name;

    public MyContacts(String name){
        setName(name);
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Hi: " + name;
    }
}
```

سپس لیست و اداپتور را از همین نوع کلاس تعریف میکنیم

[کد](https://github.com/pipitsong/androidPRJ/blob/30eccd5bccfb833c04c83db545a6fd8c59ca7c12/app/src/main/java/com/example/myapplication/ListViewActivity_MyContacts.java#L14)


نکته مهم در تعریف کلا متد toString هست که باید تعریف بشه

[متد toString](https://github.com/pipitsong/androidPRJ/blob/30eccd5bccfb833c04c83db545a6fd8c59ca7c12/app/src/main/java/com/example/myapplication/MyContacts.java#L15)

![listViewContacts-1](/image/android/listViewContacts-1.png)

# handler && timer

یک هندلر باز میکنیم که بعد از زمان مشخصی یه تسک را ران کند

```java
new Handler().postDelayed(new Runnable(){

	@override
	public void run(){
		//process
	}

} , 10000L );
```

توسط تایمر یک فرایند را هی تکرار میکنیم

گزینه Delay یعنی با تاخیر انجام بده

```java
new Timer().scheduleAtFixedRate(new TimerTask() {
	@Override
	public void run() {
		//process
	}
}, /*Delay:*/ 0,  /*duration:*/ 200);
```