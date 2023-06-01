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

# Collections

### you can perform collection manipulation using the Collection class. This class provides a set of convenient methods for working with arrays or iterable data.

-   **filter(callback)**: Filters the collection based on the provided callback function.

```php
use Cake\Collection\Collection;

$data = [1, 2, 3, 4, 5];
$collection = new Collection($data);
$filtered = $collection->filter(function ($value, $key, $iterator) {
    return $value % 2 == 0;
})->toArray();

// Output: [2, 4]
```

-   **map(callback)**: Transforms each element in the collection based on the provided callback function.

```php
use Cake\Collection\Collection;

$data = [1, 2, 3];
$collection = new Collection($data);
$transformed = $collection->map(function ($value, $key, $iterator) {
    return $value * 2;
})->toArray();

// Output: [2, 4, 6]
```

-   **reduce(callback, initial)**: Reduces the collection to a single value based on the provided callback function.

```php
use Cake\Collection\Collection;

$data = [1, 2, 3, 4, 5];
$collection = new Collection($data);
$sum = $collection->reduce(function ($carry, $value, $key, $iterator) {
    return $carry + $value;
}, 0);

// Output: 15
```

-   **sort(callback)**: Sorts the collection based on the provided callback function.

```php
use Cake\Collection\Collection;

$data = [3, 1, 4, 2, 5];
$collection = new Collection($data);
$sorted = $collection->sort(function ($a, $b) {
    return $a <=> $b;
})->toArray();

// Output: [1, 2, 3, 4, 5]
```

-   **groupBy(callback)**: Groups the collection elements based on the provided callback function.

```php
use Cake\Collection\Collection;

$data = ['apple', 'banana', 'avocado'];
$collection = new Collection($data);
$grouped = $collection->groupBy(function ($value, $key, $iterator) {
    return strlen($value);
})->toArray();

// Output: [5 => ['apple'], 6 => ['banana'], 7 => ['avocado']]
```

---

Collection methods can be used on queried data in CakePHP. CakePHP's ORM (Object-Relational Mapping) allows you to retrieve data from a database using queries, and the result of these queries is typically returned as a collection of entities or arrays. You can then use the collection methods to manipulate and process this data.

When you perform a query using CakePHP's ORM, you receive a Query object. You can execute the query and retrieve the result as a collection by calling the all() method on the Query object. Once you have the collection, you can use the collection methods to perform various operations on the queried data.

```php
use Cake\ORM\TableRegistry;

// Assuming you have a "Users" table
$usersTable = TableRegistry::getTableLocator()->get('Users');

// Querying the data
$query = $usersTable->find()
    ->where(['status' => 'active'])
    ->order(['name' => 'asc']);

// Retrieving the result as a collection
$users = $query->all();

// Performing collection operations
$filteredUsers = $users->filter(function ($user, $key, $iterator) {
    return $user->age >= 18;
});

$names = $users->extract('name')->toArray();

$totalAge = $users->reduce(function ($carry, $user, $key, $iterator) {
    return $carry + $user->age;
}, 0);

// ... perform more collection operations as needed

// Output the results
debug($filteredUsers->toArray());
debug($names);
debug($totalAge);
```

In the example above, we perform a query on the "Users" table to retrieve active users ordered by name. The result of the query is obtained using the all() method, which returns a collection. We then use various collection methods like filter(), extract(), and reduce() to manipulate the queried data.

Note that the examples above assume the usage of CakePHP's ORM and the existence of a "Users" table. You may need to adapt the code according to your specific table and entity names.
