# Date Format

-   Format Specifiers for Date Components:

    -   **Y**: Four-digit year (e.g., 2023)
    -   **y**: Two-digit year (e.g., 23)
    -   **m**: Two-digit month (01-12)
    -   **M**: Abbreviated month name (Jan-Dec)
    -   **F**: Full month name (January-December)
    -   **d**: Two-digit day of the month (01-31)
    -   **D**: Abbreviated day of the week (Sun-Sat)
    -   **l**: Full day of the week (Sunday-Saturday)

-   Format Specifiers for Time Components:

    -   **H**: Two-digit hour in 24-hour format (00-23)
    -   **h**: Two-digit hour in 12-hour format (01-12)
    -   **i**: Two-digit minute (00-59)
    -   **s**: Two-digit second (00-59)
    -   **a**: Lowercase Ante meridiem and Post meridiem (am/pm)
    -   **A**: Uppercase Ante meridiem and Post meridiem (AM/PM)

-   Additional Format Specifiers:
    -   **jS**: Day of the month with English ordinal suffix (1st, 2nd, 3rd, ...)
    -   **z**: Day of the year (0-365)
    -   **W**: ISO-8601 week number of year (weeks starting on Monday)
    -   **U**: Unix timestamp (seconds since the Unix Epoch)

```php
$timestamp = time(); // Current timestamp

$formattedDate = date('Y-m-d', $timestamp); // Output: 2023-06-01
$formattedDateTime = date('Y-m-d H:i:s', $timestamp); // Output: 2023-06-01 12:34:56
$formattedDateTimeAMPM = date('Y-m-d h:i:s A', $timestamp); // Output: 2023-06-01 12:34:56 PM
$formattedDayOfWeek = date('l', $timestamp); // Output: Thursday
$formattedOrdinalDay = date('jS', $timestamp); // Output: 1st
$formattedWeekNumber = date('W', $timestamp); // Output: 22
```
