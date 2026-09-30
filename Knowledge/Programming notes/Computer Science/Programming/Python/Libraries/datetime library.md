# **What is the ==datetime== Library?**

The `datetime` library in Python is used to work with dates and times. It allows you to:

- Get the current date and time.
    
- Perform operations like adding or subtracting days or hours.
    
- Format dates and times in different ways.
    
- Compare dates and times.
    

The library provides several classes and methods to help you handle date and time information efficiently.

# **Key Concepts in ==datetime==**

Here are the most important classes and concepts you'll work with in the `datetime` module:

# ==**datetime.date**:==

- Represents a date (year, month, day) without any time information.
    
- You can use it to create or manipulate dates.
    

Example:

```Python
import datetime 
today = datetime.date.today() 
print(today)  # Outputs today's date (e.g., 2025-12-24)
```

# ==**datetime.time**:==

- Represents a time (hour, minute, second, microsecond) without any date information.
    

Example:

```Python
import datetime
t = datetime.time(14, 30, 45)  # 2:30:45 PM 
print(t)
```

# ==**datetime.datetime**:==

- Combines both date and time information. This is one of the most commonly used classes in the `datetime` module.
    

Example:

```Python
import datetime
now = datetime.datetime.now()  # Current date and time 
print(now)  # Outputs something like 2025-12-24 14:30:45.123456
```

# ==**datetime.timedelta**:==

- Represents a duration, the difference between two dates or times. This is useful for adding or subtracting time.
    

Example:

```Python
import datetime
today = datetime.date.today() 
yesterday = today - datetime.timedelta(days=1) 
print(yesterday)  
# Outputs the previous day's date
```

# ==**datetime.strptime()**== **and** ==**datetime.strftime()**:==

- These functions are used for **parsing** and **formatting** dates and times.
    

**strptime()**: Converts a string into a `datetime` object based on a given format.

```Python
date_str = "2025-12-24" 
date_obj = datetime.datetime.strptime(date_str, "%Y-%m-%d") 
print(date_obj)
```

**strftime()**: Converts a `datetime` object into a string with a given format.

```Python
now = datetime.datetime.now() 
formatted_date = now.strftime("%A, %B %d, %Y") 
print(formatted_date)  
# Example: "Tuesday, December 24, 2025"
```

# **Important Functions and Methods**

- **datetime.now()**: Get the current date and time.
    
- **datetime.today()**: Similar to `now()`, but without time-zone support.
    
- **date.today()**: Get today's date (without time).
    
- **date.fromtimestamp()**: Convert a timestamp (seconds since Unix epoch) to a `date`.
    
- **datetime.utcnow()**: Get the current date and time in UTC (Coordinated Universal Time).
    
- **datetime.timestamp()**: Convert a `datetime` object to a timestamp.
    

# **Time Zones (Optional)**

Python's `datetime` also supports working with time zones using `timezone` objects, though it’s more advanced and might require using libraries like `pytz` for handling different time zones.

---

# **A reference of all the legal format codes:**

> **==strftime(arguments)==**

```Python
# main method / function
from datetime import datetime
formatted_date = datetime.now()

weekday = formatted_date.strftime("%A") # Example: Wednesday
```

| **Directive** | Description                                                 | Example                  |
| ------------- | ----------------------------------------------------------- | ------------------------ |
| **%a**        | Weekday, short version                                      | Wed                      |
| **%A**        | Weekday, full version                                       | Wednesday                |
| **%w**        | Weekday as a number 0-6, 0 is Sunday                        | 3                        |
| **%d**        | Day of month 01-31                                          | 31                       |
| **%b**        | Month name, short version                                   | Dec                      |
| **%B**        | Month name, full version                                    | December                 |
| **%m**        | Month as a number 01-12                                     | 12                       |
| **%y**        | Year, short version, without century                        | 18                       |
| **%Y**        | Year, full version                                          | 2018                     |
| **%H**        | Hour 00-23                                                  | 17                       |
| **%I**        | Hour 00-12                                                  | 05                       |
| **%p**        | AM/PM                                                       | PM                       |
| **%M**        | Minute 00-59                                                | 41                       |
| **%S**        | Second 00-59                                                | 08                       |
| **%f**        | Microsecond 000000-999999                                   | 548513                   |
| **%z**        | UTC offset                                                  | +0100                    |
| **%Z**        | Timezone                                                    | CST                      |
| **%j**        | Day number of year 001-366                                  | 365                      |
| **%U**        | Week number of year, Sunday as the first day of week, 00-53 | 52                       |
| **%W**        | Week number of year, Monday as the first day of week, 00-53 | 52                       |
| **%c**        | Local version of date and time                              | Mon Dec 31 17:41:00 2018 |
| **%C**        | Century                                                     | 20                       |
| **%x**        | Local version of date                                       | 12/31/18                 |
| **%X**        | Local version of time                                       | 17:41:00                 |
| **%%**        | A % character                                               | %                        |
| **%G**        | ISO 8601 year                                               | 2018                     |
| **%u**        | ISO 8601 weekday (1-7)                                      | 1                        |
| **%V**        | ISO 8601 weeknumber (01-53)                                 | 01                       |


---

Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  
Learn more? Go to Introduction: [[Python Introduction]]
