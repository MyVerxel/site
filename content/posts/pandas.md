---
title: "Pandas"
date: 1401-03-11T16:14:59
draft: false
---

# Start

ایمپورت کردن :

```python
import pandas as pd
```

تمامی دیتا فریم ها رو با d نشون خواهم داد


در پانداس مبنای کار بر اساس دیتا فریم است؛ در مرحله اول دیتا ها را باید به شکل دیتافریم ایجد کنیم تا بتوانیم توسط پانداس با آنها کار کنیم

دیتاها میتوانند از متغیر ها و یا از فایلها وارد شوند

## read from excel

```python
d = pd.read_excel("file.xls",
	header=[1]
	)
```

توسز پارامتر header تعییرن میکنیم که کدام که سطر اول را به عنوان هدر فیلد ها در نظر بگیرد

## read from csv

```python
d = pd.read_csv("file.csv",
	header = None,
	skiprows = 1,
	usecols=[2,3],
	names=['colA', 'colB'],
	sep=';'
	)
```

دیتا توس فایل csv وارد میشوند؛ در اینجا سطر اول به طور پیش فرض بعنوان هدر در نظر گردفته میشود


توسط header میتوانیم تعیین کنیم سطر چندم بعنوام هدر در نظر گرفته شود

توسط skiprow میتوانیم تعیین کنیم چند سط نادیده گرفته شود

توسط usecols تعییر مکینیم که چه سطر هایی را وارد کند و از بقیه سطر ها صرف نظر میکند

توس names تعیین میکنیم هر ستون چه نامی داشته باشد

توسط sep کاراکتر جدا کننده فیلدها از یکدیگر را مشخص میکنیم


## pct_changes

میزان درصد تغییرات رو نشون میده

```python
d.Close.pct_changes()
```