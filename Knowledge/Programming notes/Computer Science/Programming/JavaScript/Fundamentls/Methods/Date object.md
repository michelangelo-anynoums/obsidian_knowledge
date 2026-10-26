# 📅 JavaScript — Date Object

> [!abstract] Overview The **Date** **object** in JavaScript is used to work with dates and times. It allows us to create dates, retrieve date information, compare dates, and manipulate time.

## 1. Creating a Date

Use `new Date()` to create a Date object.

```js
// Current date and time
const now = new Date();

// Specific date and time
const birthday = new Date("2000-05-15");

// Date using numbers
const date = new Date(2025, 4, 15);
```

> [!tip] Remember Months in numeric Date constructors start at **0**: - `0` → January - `4` → May - `11` → December Therefore, `new Date(2025, 4, 15)` represents May 15, 2025.

## 2. Getting Date Information

JavaScript provides methods to retrieve individual parts of a date.

```js
const date = new Date();

date.getFullYear(); // Year
date.getMonth();    // Month (0–11)
date.getDate();     // Day of the month (1–31)
date.getDay();      // Day of the week (0–6)
date.getHours();    // Hours (0–23)
date.getMinutes();  // Minutes (0–59)
date.getSeconds();  // Seconds (0–59)
```

> [!warning] Two important differences - `getDate()` returns the day of the month. - `getDay()` returns the day of the week: Sunday = `0`, Saturday = `6`.

## 3. Setting Date Information

Use setter methods to change parts of an existing Date object.

```js
const date = new Date();

date.setFullYear(2030);
date.setMonth(5);  // June
date.setDate(20);
date.setHours(12);
```

**Note:** Changing a date can also change other parts of it. For example, setting the day beyond the end of a month can move the date into the next month.

## 4. Converting Dates to Strings

Different methods produce different date formats.

```js
const date = new Date();

date.toString();       // Local date and time
date.toDateString();   // Date only
date.toISOString();    // Standard UTC format
date.toLocaleDateString(); // Localized date
date.toLocaleTimeString(); // Localized time
```

Example:

```js
const date = new Date("2025-05-15T12:30:00Z");

console.log(date.toISOString());
// "2025-05-15T12:30:00.000Z"
```

> [!info] What does `Z` mean? The letter `Z` indicates **UTC time**, the standard reference time used worldwide.

## 5. Getting a Timestamp

A timestamp represents the number of milliseconds since **January 1, 1970, at 00:00:00 UTC**.

```js
const now = new Date();

console.log(now.getTime());
console.log(Date.now());
```

- `getTime()` returns the timestamp of a Date object.
- `Date.now()` returns the current timestamp directly.

Timestamps are useful for measuring elapsed time and comparing dates.

## 6. Comparing Dates

Date objects can be compared using their timestamps.

```js
const first = new Date("2025-01-01");
const second = new Date("2025-12-31");

console.log(first < second); // true
console.log(first > second); // false
```

To check whether two dates represent exactly the same instant:

```js
date1.getTime() === date2.getTime();
```

> [!tip] Best practice Compare timestamps when you need to check whether two dates represent the same instant.

## 7. Date vs. Date.now()

These two expressions serve different purposes.

```js
const date = new Date(); // A Date object

const timestamp = Date.now(); // A number
```

Use `new Date()` when you need to work with a date object. Use `Date.now()` when you only need the current timestamp.

## 8. Important Things to Remember

- JavaScript dates represent a point in time, based on milliseconds since the Unix epoch.
- `getMonth()` starts at `0`, not `1`.
- `getDate()` gives the day of the month; `getDay()` gives the day of the week.
- Local date methods and UTC date methods may return different values.
- Date-only strings such as `"2025-05-15"` are interpreted as UTC, while date-time strings without a time-zone indicator are generally interpreted as local time.
- For reliable date formatting, use `toLocaleDateString()` or `Intl.DateTimeFormat`.

## 9. Quick Reference

|Method|Purpose|
|---|---|
|`new Date()`|Create a Date object|
|`Date.now()`|Get the current timestamp|
|`getFullYear()`|Get the year|
|`getMonth()`|Get the month (0–11)|
|`getDate()`|Get the day of the month|
|`getDay()`|Get the day of the week|
|`getTime()`|Get the timestamp|
|`setFullYear()`|Change the year|
|`toISOString()`|Convert to UTC ISO format|
|`toLocaleDateString()`|Format the date for a locale|

---
