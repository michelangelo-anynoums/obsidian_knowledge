## **1. Importing the calendar module**

```Python
import calendar
```

The `calendar` module helps you work with dates, months, and years—without using `datetime` for the heavy lifting.

---

## **2. Displaying a text calendar**

You can create a **month or year calendar as text**.

### Example: Month Calendar

```Python
import calendar  
  
year = 2026  
month = 3  
```
  
## Create a text calendar  

```Python
cal = calendar.TextCalendar(calendar.SUNDAY)  # Week starts on Sunday  
month_calendar = cal.formatmonth(year, month)  
print(month_calendar)
```

Output looks like this:

```Bash
     March 2026  
Su Mo Tu We Th Fr Sa  
 1  2  3  4  5  6  7  
 8  9 10 11 12 13 14  
15 16 17 18 19 20 21  
22 23 24 25 26 27 28  
29 30 31
```

✅ You can also use `calendar.HTMLCalendar()` if you want HTML output.

---

## **3. Displaying a full year**

```Python
print(calendar.calendar(2026))
```

This prints all 12 months in a text-based calendar format.

---

## **4. Working with weekdays**

You can find out the **day of the week** for a specific date:

## weekday(year, month, day) -> Monday is 0, Sunday is 6  

```Python
day_of_week = calendar.weekday(2026, 3, 21)  
print(day_of_week)  # 5 → Saturday
```

Or get the name of the day:

```Python
print(calendar.day_name[day_of_week])  # 'Saturday'
```

---

## **5. Checking for leap years**

```Python
print(calendar.isleap(2026))  # False  
print(calendar.isleap(2024))  # True

You can also count leap years in a range:

print(calendar.leapdays(2000, 2030))  # Counts leap years from 2000 to 2029
```

---

## **6. Iterating over a month’s days**

You can get all days in a month using `itermonthdays`:

```Python
cal = calendar.Calendar()  
for day in cal.itermonthdays(2026, 3):  
    print(day, end=' ')  # 0 means days outside the month
```

Output:

```Bash
0 0 0 0 0 0 1 2 3 4 5 6 7 8 9 10 ... 31
```

---

## **7. Customizing the first weekday**

By default, Python’s calendar starts with Monday. You can change it:

```Python
cal = calendar.TextCalendar(calendar.SUNDAY)  
print(cal.formatmonth(2026, 3))
```

